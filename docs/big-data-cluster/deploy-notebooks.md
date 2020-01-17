---
title: Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを展開する
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio からノートブックを使用して、ビッグ データ クラスターを展開します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dfdf7dfd2ca5521bd80c4fdbf81e7b5c45d58b8d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594242"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを展開する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、展開ノートブックを含む Azure Data Studio の拡張機能が提供されています。 展開ノートブックには、SQL Server ビッグ データ クラスターを作成するために Azure Data Studio 内で使用できるドキュメントとコードが含まれています。

もともとは、オープン ソース プロジェクトとして実装され、[ノートブック](notebooks-guidance.md)は [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download) 内に実装されていました。 テキスト セル内のテキストに対してはマークダウンを、また、コード セル内にコードを記述するには利用可能なカーネルの 1 つを使用できます。

ノートブックを使用して、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] に対してビッグ データ クラスターを展開できます。

## <a name="prerequisites"></a>Prerequisites

ノートブックも起動するには、次の前提条件が要件です。

* [Azure Data Studio Insiders ビルド](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)の最新バージョンがインストールされていること

上記に加えて、SQL Server 2019 ビッグ データ クラスターを展開するには、以下も必要になります。

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI (Azure に展開する場合)](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)

## <a name="launch-the-notebook"></a>ノートブックを起動する

1. Azure Data Studio を起動します。

2. **[接続]** タブで、省略記号 **[...]** を選択し、**[Deploy SQL Server...]\(SQL Server の展開...\)** を選択します。

   ![SQL Server を展開する](media/deploy-notebooks/deploy-notebooks.png)

3. 展開のオプションで、**[SQL Server Big Data Cluster]\(SQL Server ビッグ データ クラスター\)** を選択します。

4. **[オプション]** 下にある **[展開ターゲット]** から、**[New Azure Kubernetes Cluster]\(新しい Azure Kubernetes クラスター\)** または **[Existing Azure Kubernetes Service cluster]\(既存の Azure Kubernetes Service クラスター\)** のどちらかを選択します。

5. プライバシーとライセンス条項に同意する

6. このダイアログでは、選択した種類の SQL 展開に必要なツールがホストに存在するかどうかも確認されます。 ツールの確認が成功するまで、**[選択]** ボタンは有効になりません。

7. **[選択]** ボタンを選択します。 この操作により、展開エクスペリエンスが起動されます。

## <a name="set-deployment-configuration-template"></a>展開構成テンプレートを設定する

以下の手順のようにして、展開プロファイルの設定をカスタマイズできます。

### <a name="target-configuration-template"></a>対象の構成テンプレート

使用可能なテンプレートから対象の構成テンプレートを選択します。 使用可能なプロファイルは、前のダイアログで選択した展開ターゲットの種類に応じてフィルター処理されています。

   ![展開構成テンプレート ステップ 1](media/deploy-notebooks/deployment-configuration-template.png)

### <a name="azure-settings"></a>Azure の設定

展開ターゲットが新しい AKS の場合、AKS クラスターを作成するには、Azure サブスクリプション ID、リソース グループ、AKS クラスター名、VM 数、サイズ、その他の追加情報が必要です。

   ![Azure の設定](media/deploy-notebooks/azure-settings.png)

展開ターゲットが既存の Kubernetes クラスターの場合は、ウィザードによって、Kubernetes クラスターの設定をインポートするための *kube* 構成ファイルへのパスを入力するように求められます。 SQL Server 2019 ビッグ データ クラスターを展開できる、適切なクラスター コンテキストが選択されていることを確認します。

   ![ターゲット クラスターのコンテキスト](media/deploy-notebooks/target-cluster-context.png)

### <a name="cluster-docker-and-ad-settings"></a>クラスター、Docker、AD の設定

1. SQL Server 2019 BDC のクラスター名、管理者のユーザー名、パスワードを入力します。
注:コントローラーと SQL Server に同じアカウントが使用されます。

   ![クラスターの設定](media/deploy-notebooks/cluster-settings.png)

2. 必要に応じて Docker の設定を入力します

   ![Docker の設定](media/deploy-notebooks/docker-settings.png)

3. AD 認証が使用可能な場合は、AD の設定を入力します

   ![Active Directory の設定](media/deploy-notebooks/active-directory-settings.png)

### <a name="service-settings"></a>サービスの設定

この画面には、**スケール**、**エンドポイント**、**ストレージ**、その他の**詳細なストレージ設定**など、さまざまな設定の入力があります。 適切な値を入力し、**[次へ]** を選択してください。

#### <a name="scale-settings"></a>スケールの設定

ビッグ データ クラスター内の各コンポーネントのインスタンス数を入力します。

Spark インスタンスは HDFS に含めることができます。 それは、記憶域プールに含まれるか、または専用の Spark プールに含まれます。

   ![サービスの設定](media/deploy-notebooks/service-settings.png)

これらの各コンポーネントの詳細については、[マスター インスタンス](concept-master-instance.md)、[データ プール](concept-data-pool.md)、[記憶域プール](concept-storage-pool.md)、[コンピューティング プール](concept-compute-pool.md)を参照してください。

#### <a name="endpoint-settings"></a>エンドポイントの設定

既定のエンドポイントがあらかじめ入力されています。 ただし、必要に応じて変更できます。

   ![エンドポイントの設定](media/deploy-notebooks/endpoint-settings.png)

#### <a name="storage-settings"></a>ストレージ設定

ストレージの設定には、データとログのストレージ クラスおよび要求サイズが含まれます。 設定は、ストレージ、データ、および SQL Server のマスター プール全体に適用できます。

   ![ストレージ設定](media/deploy-notebooks/storage-settings.png)

#### <a name="advanced-storage-settings"></a>詳細なストレージ設定

**[Advanced storage settings]\(詳細なストレージ設定\)** では、その他のストレージ設定を追加できます

* 記憶域プール (HDFS)
* データ プール
* SQL Server マスター

   ![詳細なストレージ設定](media/deploy-notebooks/advanced-storage-settings.png)

### <a name="summary"></a>まとめ

この画面には、SQL Server 2019 ビッグ データ クラスターを展開するために指定したすべての入力がまとめられています。 **[Save config files]\(構成ファイルの保存\)** ボタンを使用して、構成ファイルをダウンロードできます。 展開の構成全体をノートブックにスクリプト化するには、**[Script to Notebook]\(ノートブックにスクリプト化\)** を選択します。 ノートブックを開き、**[Run Cells]\(セルの実行\)** を選択して、選択したターゲットへの SQL Server 2019 BDC の展開を始めます。

   ![まとめ](media/deploy-notebooks/deploy-sql-server-big-data-cluster-on-a-new-AKS-cluster.png)

## <a name="next-steps"></a>次の手順

展開の詳細については、[SQL Server ビッグ データ クラスターの展開ガイダンス](deployment-guidance.md)に関するページを参照してください。
