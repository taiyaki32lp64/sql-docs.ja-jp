---
title: SQL Server ビッグ データ クラスターのリリース ノート
titleSuffix: SQL Server big data clusters
description: この記事では、SQL Server ビッグ データ クラスターの最新の更新プログラムと既知の問題について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bc5928a7e3015545d36900b52ef01a42d9694cc0
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706168"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>SQL Server ビッグ データ クラスターのリリース ノート

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] では、機械学習機能や AI 機能など、大量のデータ セットを処理する完全な環境が与えられ、あらゆるデータから分析情報をほぼリアルタイムに取得できます。

この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) の最新リリースに関する更新プログラムと既知の問題を一覧表示します。

## <a id="rtm"></a> SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] では、SQL Server ビッグ データ クラスターについて説明しています。

SQL Server ビッグ データ クラスターを使用して次のことを行います。

- Kubernetes で実行している SQL Server、Spark、HDFS コンテナーの[スケーラブルなクラスターを展開](../big-data-cluster/deploy-get-started.md)します。 
- Transact-SQL または Spark からビッグ データの読み取り、書き込み、処理を行います。
- 大量のビッグ データを使用して、価値の高いリレーショナル データを簡単に組み合わせて分析します。
- 外部データ ソースを照会します。
- SQL Server によって管理される HDFS にビッグ データを格納します。
- クラスターを介して複数の外部データ ソースからデータを照会します。
- AI、機械学習、その他の分析タスクにデータを使用します。
- [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] に[アプリケーションを展開して実行](../big-data-cluster/concept-application-deployment.md)します。
- [PolyBase](../relational-databases/polybase/polybase-guide.md) を使用してデータを仮想化します。 外部テーブルを使用して、外部の SQL Server、Oracle、Teradata、MongoDB、ODBC データ ソースからデータを照会します。
- Always On 可用性グループ テクノロジを使用して、SQL Server マスター インスタンスとすべてのデータベースの高可用性を実現します。

## <a name="sql-server-version"></a>SQL Server のバージョン

SQL Server の最新バージョンは `15.0.2070.34` です。

## <a name="image-tags"></a>イメージ タグ

このリリースのイメージ タグは `2019-GDR1-ubuntu-16.04` です。

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>サポート性

このセクションでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) でサポートされているプラットフォームについて説明します。

### <a name="kubernetes-platforms"></a>Kubernetes プラットフォーム

|プラットフォーム|サポートされるバージョン|
|---------|---------|
|Kubernetes|BDC に必要な Kubernetes の最小バージョンは 1.13 です。 Kubernetes バージョンのサポート ポリシーについては、[Kubernetes バージョンとバージョン スキュー サポート](https://kubernetes.io/docs/setup/release/version-skew-policy/)に関するページを参照してください。|
|Azure Kubernetes Service (AKS)|BDC に必要な AKS の最小バージョンは 1.13 です。<br/>バージョンのサポート ポリシーについては、[AKS でサポートされている Kubernetes のバージョン](/azure/aks/supported-kubernetes-versions)に関するページを参照してください。|

### <a name="host-os-for-kubernetes"></a>Kubernetes のホスト OS

|プラットフォーム|サポートされるバージョン|
|---------|---------|
|Red Hat Enterprise Linux|7.3、7.4、7.5、7.6|
|Ubuntu|16.04|

### <a name="tools"></a>ツール

|プラットフォーム|サポートされるバージョン|
|---------|---------|
|`azdata`|サーバーと同じマイナー バージョンを指定する必要があります (SQL Server マスター インスタンスと同様)。<br/>`azdata –-version` を実行して、バージョンを検証します。 現時点では、このバージョンは `15.0.2070` です。|
|Azure Data Studio|[Azure Data Studio](https://aka.ms/getazuredatastudio) の最新のビルドを取得します。|

### <a name="sql-server-editions"></a>SQL Server のエディション

|Edition|注|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| ビッグ データ クラスターのエディションは、SQL Server マスター インスタンスのエディションによって決まります。 展開時に、Developer エディションが既定で展開されます。 エディションは、展開後に変更できます。 [SQL Server マスター インスタンスの構成](../big-data-cluster/configure-sql-server-master-instance.md)に関するページを参照してください。 |

## <a name="known-issues"></a>既知の問題

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>Azure Data Studio (ADS) または curl からの Livy ジョブの送信が 500 エラーで失敗する

**問題およびユーザーへの影響**:HA 構成では、Spark 共有リソース (sparkhead) が複数のレプリカで構成されます。 この場合、Azure Data Studio (ADS) または `curl` からの Livy ジョブの送信でエラーが発生する可能性があります。 確認するには、sparkhead ポッドに `curl` を実行すると、接続が拒否されます。 たとえば、`curl https://sparkhead-0:8998/` または `curl https://sparkhead-1:8998` によって 500 エラーが返されます。

これは、次のシナリオで発生します。

- 各 Zookeeper インスタンスの Zookeeper ポッドまたはプロセスが数回再起動します。
- Sparkhead ポッドと Zookeeper ポッド間のネットワーク接続が信頼できない場合。

**回避策**:両方の Livy サーバーを再起動します。

```bash
kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

```bash
kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>可用性グループのマスター インスタンスの場合にメモリ最適化テーブルを作成する

- **問題およびユーザーへの影響**:可用性グループ データベース (リスナー) に接続するために公開されているプライマリ エンドポイントを使用して、メモリ最適化テーブルを作成することはできません。

- **回避策**:SQL Server マスター インスタンスが可用性グループの構成である場合にメモリ最適化テーブルを作成するには、新しい接続で作成されたセッションで、[SQL Server インスタンスに接続](deployment-high-availability.md#instance-connect)し、エンドポイントを公開し、SQL Server データベースに接続して、メモリ最適化テーブルを作成します。

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>外部テーブルの Active Directory 認証モードに挿入する

- **問題およびユーザーへの影響**:SQL Server マスター インスタンスが Active Directory 認証モードになっている場合、外部テーブルのうち少なくとも 1 つがストレージプール内にある場合に外部テーブルからのみ選択され、別の外部テーブルに挿入されるクエリでは、次のように返されます。

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **回避策**:次のいずれかの方法でクエリを変更します。 ストレージ プール テーブルをローカル テーブルに結合するか、最初にローカル テーブルに挿入し、ローカル テーブルからデータを読み取ってデータ プールに挿入します。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)に関するページを参照してください。
