---
title: Kubernetes でのデータ永続化
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 ビック データ クラスターでのデータ永続化のしくみについて説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4671bc07dd21a769746257339ea7903e3dda4701
ms.sourcegitcommit: 385a907ed1de8fa7ada76260ea3f92583eb09238
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74063973"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes 上の SQL Server ビッグ データ クラスターでのデータ永続化

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永続ボリューム](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)では、Kubernetes 内にあるストレージ向けのプラグイン モデルを提供します。 ストレージの提供方法は、その使用方法から抽象化されます。 そのため、独自の高可用性ストレージを利用して、SQL Server ビッグ データ クラスターに接続できます。 これにより、必要としているストレージの種類、可用性、およびパフォーマンスを完全に制御できます。 Kubernetes では、Azure ディスク/ファイル、NFS、ローカル ストレージなどのさまざまな種類のストレージ ソリューションがサポートされます。

## <a name="configure-persistent-volumes"></a>永続ボリュームを構成する

SQL Server ビッグ データ クラスターがこれらの永続ボリュームを使用する方法は、[ストレージ クラス](https://kubernetes.io/docs/concepts/storage/storage-classes/)を利用することです。 異なるストレージの種類に対しては異なるストレージ クラスを作成し、ビッグ データ クラスターの展開時に指定できます。 プール レベルでの目的に使用するためのストレージ クラスと永続ボリューム要求のサイズを構成できます。 SQL Server ビッグ データ クラスターでは、永続ボリュームを必要とするコンポーネントごとに指定したストレージ クラス名を使って、[永続ボリューム要求](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)が作成されます。 その後、ポッド内で該当の永続ボリュームがマウントされます。 

ここでは、ビッグ データ クラスターのストレージ構成を計画する際に考慮する重要な事項について説明します。

- ビッグ データ クラスターの展開を成功させるには、必要な数の永続ボリュームが使用可能であることを確認する必要があります。 AKS クラスターに展開していて、組み込みのストレージ クラス (`default` または `managed-premium`) のいずれかを使用している場合は、永続ボリュームの動的プロビジョニングがサポートされます。 つまり、永続ボリュームを事前に作成する必要はありませんが、AKS クラスター内で使用可能なワーカー ノードが、展開に必要な永続ボリュームと同じ数のディスクを接続できることを確認する必要があります。 ワーカー ノードに対して指定されている [VM サイズ](/azure/virtual-machines/linux/sizes/)によっては、各ノードが特定の数のディスクを接続できます。 既定のサイズのクラスター (高可用性なし) の場合は、少なくとも 24 個のディスクが必要です。 高可用性を有効にする場合、またはプールをスケール アップする場合は、スケール アップするリソースに関係なく、追加のレプリカごとに少なくとも 2 つの永続化ボリュームを確保する必要があります。

- 構成内で指定しているストレージ クラスのストレージ プロビジョナーによって動的プロビジョニングがサポートされていない場合は、永続化されたボリュームを事前に作成する必要があります。 たとえば、`local-storage` プロビジョナーでは動的プロビジョニングが有効になりません。 `kubeadm` を使用して展開された Kubernetes クラスター内でこれを行う方法については、この[サンプル スクリプト](https://github.com/microsoft/sql-server-samples/tree/cu1-bdc/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)を参照してください。

- ビッグ データ クラスターを展開するときに、クラスター内のすべてのコンポーネントで使用される同一ストレージ クラスを構成することができます。 ただし、運用環境での展開のベスト プラクティスとして、さまざまなコンポーネントでは、サイズやスループットに関してさまざまなワークロードに対応するために、異なるストレージ構成が必要になります。 コントローラーで指定されている既定のストレージ構成は、SQL Server マスター インスタンス、データ、および記憶域プールごとに上書きできます。 この記事では、これを行う方法の例を示します。

- SQL Server 2019 CU1 リリース時点では、展開後のストレージ構成設定は変更できません。 これには、各インスタンスの永続ボリューム要求のサイズの変更が含まれるだけでなく、展開後のスケーリング操作もサポートされていません。 このため、ビッグ データ クラスターより前にストレージ レイアウトを計画することがとても重要です。

- Kubernetes をコンテナー化されたアプリケーションとして展開し、ステートフル セットや永続ストレージなどの機能を使用するという性質上、Kubernetes では、正常性の問題が発生した場合にポッドが再起動され、同じ永続ストレージに接続されることが確実です。 ただし、ノードで障害が発生し、ポッドを別のノードで再起動する必要がある場合は、ストレージが障害ノードに対してローカルであると、使用できなくなるリスクが高くなります。 このリスクを克服するには、追加の冗長性を構成し、[高可用性機能](deployment-high-availability.md)を有効にするか、リモート冗長ストレージを使用する必要があります。 ここでは、ビッグ データ クラスター内のさまざまなコンポーネントのストレージ オプションの概要について説明します。

| リソース | データのストレージの種類 | ログのストレージの種類 |  注 |
|---|---|---|--|
| SQL Server マスター インスタンス | ローカル (レプリカ > = 3) またはリモート冗長ストレージ (レプリカ = 1) | ローカル ストレージ | ポッドがノードに対して維持されるステートフル セット ベースの実装では、再起動と一時的なエラーによってデータ損失が発生することはありません。 |
| 計算プール | ローカル ストレージ* | ローカル ストレージ | ユーザー データが格納されていません。 |
| データ プール | ローカル/リモート冗長ストレージ | ローカル ストレージ | データ プールを他のデータ ソースから再構築できない場合は、リモート冗長ストレージを使用します。  |
| 記憶域プール (HDFS) | ローカル/リモート冗長ストレージ | ローカル ストレージ | HDFS レプリケーションが有効になっている場合。 |
| Spark プール | ローカル ストレージ* | ローカル ストレージ | ユーザー データが格納されていません。 |
| コントロール (controldb、metricsdb、logsdb)| リモート冗長ストレージ | ローカル ストレージ | ビッグ データ クラスターのメタデータにストレージ レベルの冗長性を使用することが重要です。 |

> [!IMPORTANT]
> 制御関連コンポーネントがリモート冗長ストレージ上にあることを確認する必要があります。 `controldb-0` ポッドは、クラスター サービスの状態やさまざまな設定などに関するすべてのメタデータを格納するデータベースを使用して、SQL Server インスタンスをホストします。このインスタンスが使用できなくなると、クラスター内の他の依存サービスに正常性の問題が生じます。

## <a name="configure-big-data-cluster-storage-settings"></a>ビッグ データ クラスターのストレージ設定を構成する

他のカスタマイズと同様に、`bdc.json` 構成ファイル内の各プールと `control.json` ファイル内のコントロール サービスに対して、展開時にクラスター構成ファイル内にストレージの設定を指定できます。 プールの仕様にストレージ構成設定がない場合は、SQL Server マスター (`master` リソース)、HDFS (`storage-0` リソース)、データ プールなど、他のすべてのコンポーネントに対してコントロールのストレージ設定が使用されます。 これは、仕様に含めることができるストレージ構成セクションのサンプルです。

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

ビッグ データ クラスターの展開では、永続ストレージを使用して、さまざまなコンポーネントに対するデータ、メタデータ、およびログが格納されます。 展開の一部として作成された永続ボリューム要求のサイズをカスタマイズできます。 ベスト プラクティスとして、ストレージ クラスは、*Retain* [再要求ポリシー](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)によってストレージ クラスを使用することをお勧めします。

> [!WARNING]
> 永続ストレージを使用せずに実行すると、テスト環境内では動作しますが、クラスターが機能しなくなる可能性があります。 ポッドの再起動時には、クラスターのメタデータやユーザー データが完全に失われます。 この構成では実行しないことをお勧めします。 

[ストレージの構成](#config-samples)に関するセクションで、SQL Server ビッグ データ クラスターの展開に対するストレージ設定の構成方法の例をさらに紹介しています。

## <a name="aks-storage-classes"></a>AKS のストレージ クラス

AKS には、対応する動的プロビジョナーを備えた [2 つの組み込みのストレージ クラス](/azure/aks/azure-disks-dynamic-pv/)である `default` と `managed-premium` が付属しています。 永続ストレージが有効になったビッグ データ クラスターを展開する場合、それらのうちどちらかを指定するか、または、独自のストレージ クラスを作成することができます。 既定では、aks の `aks-dev-test` に対する組み込みのクラスター構成ファイルは、`default` ストレージ クラスを使用する永続ストレージ構成を備えています。

> [!WARNING]
> 組み込みのストレージ クラスである `default` および `managed-premium` によって作成された永続ボリュームには、*Delete* の再要求ポリシーが用意されています。 そのため、SQL Server ビッグ データ クラスターを削除すると、永続ボリューム要求が削除された後、永続ボリュームも削除されます。 [こちら](/azure/aks/concepts-storage/#storage-classes)の記事に示すように、`Retain` 再要求ポリシーによって `azure-disk` プロビジョナーを使用して、カスタム ストレージ クラスを作成できます。

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` クラスターのストレージ クラス 

`kubeadm` を使用して展開された Kubernetes クラスターには、組み込みのストレージ クラスはありません。 ローカル ストレージまたは [Rook](https://github.com/rook/rook) などの推奨のプロビジョナーを使用して、独自のストレージ クラスと永続ボリュームを作成する必要があります。 その場合は、構成したストレージ クラスを `className` に設定します。 

> [!IMPORTANT]
>  kubeadm 用の組み込みの展開構成ファイル (`kubeadm-dev-test` または `kubeadm-prod`) では、データおよびログのストレージ用のストレージ クラス名は指定されていません。 展開の前に、構成ファイルをカスタマイズして `className` に値を設定する必要があります。そうしないと、展開前の検証でエラーになります。 また、展開には、ストレージ クラスの存在について確認する検証手順が含まれますが、必要な永続ボリュームについては含まれません。 クラスターのスケールに応じた十分なボリュームを確実に作成しておく必要があります。 既定の最小クラスター サイズ (既定のスケール、高可用性なし) では、少なくとも 24 個の永続ボリュームを作成する必要があります。
>
>「[Kubernetes クラスターを作成する](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)」には、ローカル プロビジョナーを利用した永続ボリューム作成の例があります。 この例では、Kubernetes ストレージが利用されています。


## <a name="customize-storage-configurations-for-each-pool"></a>各プール用のストレージ構成をカスタマイズする

すべてのカスタマイズにおいて、使用する組み込みの構成ファイルのコピーを最初に作成しておく必要があります。 たとえば、次のコマンドでは、`aks-dev-test` 展開構成ファイルのコピーが `custom` という名前のサブディレクトリに作成されます。

```bash
azdata bdc config init --source aks-dev-test --target custom
```

これにより、`bdc.json` および `control.json` という 2 つのファイルが作成され、手動で編集するか、または `azdata bdc config` コマンドを使用してカスタマイズすることができます。 jsonpath および jsonpatch ライブラリを組み合わせて使用すると、構成ファイルを編集する手段を提供できます。


### <a id="config-samples"></a>ストレージ クラス名および要求サイズを構成する

既定では、クラスター内にプロビジョニングされた各ポッドに対応する、プロビジョニングされた永続ボリューム要求のサイズは、10 GB です。 この値は、クラスターの展開前にカスタム構成ファイル内で実行しているワークロードに合わせて更新できます。

次の例では、`control.json` 内で永続ボリューム要求のサイズを 32Gi に更新しています。 プール レベルで上書きされない場合、この設定はすべてのプールに適用されます。

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

次の例は、`control.json` ファイルでのストレージ クラスの変更方法を示しています。

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

別のオプションとして、カスタム構成ファイルを手動で編集するか、次の例にあるように json パッチを使用して Storage プールに対するストレージ クラスを変更することもできます。 次のコンテンツを含む `patch.json` ファイルを作成します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

パッチ ファイルを適用します。 `azdata bdc config patch` コマンドを使用して、JSON 修正プログラム ファイル内の変更を適用します。 次の例では、`patch.json` ファイルをターゲットの展開構成ファイルである `custom.json` に適用します。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>次の手順

Kubernetes でのボリュームに関する詳細なドキュメントについては、[ボリュームに関する Kubernetes ドキュメント](https://kubernetes.io/docs/concepts/storage/volumes/)を参照してください。

SQL Server ビッグ データ クラスターの展開の詳細については、「[Kubernetes に SQL Server ビッグ データ クラスターを展開する方法](deployment-guidance.md)」を参照してください。
