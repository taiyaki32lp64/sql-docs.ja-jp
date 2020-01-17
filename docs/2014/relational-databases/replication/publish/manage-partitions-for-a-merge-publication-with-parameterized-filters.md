---
title: パラメーター化されたフィルターによるマージ パブリケーションのパーティションの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- partitions [SQL Server replication]
- merge replication partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], partition management
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a71ac4d6bcc887257ea5bfbc1523e327fc03b16
ms.sourcegitcommit: ea6603e20c723553c89827a6b8731a9e7b560b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479312"
---
# <a name="manage-partitions-for-a-merge-publication-with-parameterized-filters"></a>パラメーター化されたフィルターによるマージ パブリケーションのパーティションの管理
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、パラメーター化されたフィルターを利用し、マージ パブリケーションのパーティションを管理する方法ついて説明します。 パラメーター化された行フィルターを使用して、重複しないパーティションを生成できます。 パーティションを制限することで、特定のパーティションを 1 つのサブスクリプションだけが受け取るようにできます。 このような場合、サブスクリプションの数が多いと多数のパーティションが生成されるため、それと同数のパーティション スナップショットが必要になります。 詳細については、「 [パラメーター化された行フィルター](../merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
-   **パラメーター化されたフィルターを使用してマージパブリケーションのパーティションを管理するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-sql](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Recommendations"></a>推奨事項  
  
-   レプリケーション トポロジをスクリプト化する場合 (推奨)、パブリケーション スクリプトには、データ パーティションを作成するためのストアド プロシージャの呼び出しが含まれます。 このスクリプトによって、作成されたパーティションの参照、および必要に応じて 1 つ以上のパーティションを再作成する方法を利用できます。 詳しくは、「 [Scripting Replication](../scripting-replication.md)」をご覧ください。  
  
-   パブリケーションが、重複しないパーティションを含むサブスクリプションを返すパラメーター化されたフィルターを持つ場合に、特定のサブスクリプションが失われて再作成が必要になったときは、サブスクライブされたパーティションを削除し、サブスクリプションを再作成してから、パーティションを再作成する必要があります。 詳細については、「 [パラメーター化された行フィルター](../merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。 パブリケーション作成スクリプトが生成されると、レプリケーションによって既存のサブスクライバー パーティション用の作成スクリプトが生成されます。 詳しくは、「 [Scripting Replication](../scripting-replication.md)」をご覧ください。  
  
##  <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
 
  **[パブリケーションのプロパティ - **Publication>]** ダイアログ ボックスの \<[データ パーティション]** ページでパーティションを管理します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](view-and-modify-publication-properties.md)」を参照してください。 このページでは、パーティションを作成および削除する、サブスクライバーがスナップショットの生成および配信を開始できるようにする、1 つ以上のパーティションのスナップショットを生成する、スナップショットをクリーンアップするなどの操作を行うことができます。  
  
#### <a name="to-create-a-partition"></a>パーティションを作成するには  
  
1.  
  **[パブリケーションのプロパティ - **Publication>]** ダイアログ ボックスの \<[データ パーティション]** ページで **[追加]** をクリックします。  
  
2.  
  **[データ パーティションの追加]** ダイアログ ボックスで、作成するパーティションに関連する **HOST_NAME()** 値または **SUSER_SNAME()** 値、あるいはその両方を入力します。  
  
3.  オプションでスナップショットの更新スケジュールを指定します。  
  
    1.  
  **[以下のスケジュールでこのパーティションのスナップショット エージェントを実行する]** を選択します。  
  
    2.  スナップショットの既定の更新スケジュールをそのまま使用するか、または **[変更]** をクリックして別のスケジュールを指定します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-partition"></a>パーティションを削除するには  
  
1.  
  **[データ パーティション]** ページのグリッドでパーティションを選択します。  
  
2.  
  **[削除]** をクリックします。  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>サブスクライバーにスナップショットの生成と配信を許可するには  
  
1.  
  **[データ パーティション]** ページで、 **[新規サブスクライバーで同期を行うとき、パーティションを自動的に定義し、必要に応じてスナップショットを生成する]** を選択します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-generate-a-snapshot-for-a-partition"></a>パーティションのスナップショットを生成するには  
  
1.  
  **[データ パーティション]** ページのグリッドでパーティションを選択します。  
  
2.  
  **[今すぐ選択したスナップショットを生成する]** をクリックします。  
  
#### <a name="to-clean-up-a-snapshot-for-a-partition"></a>パーティションのスナップショットをクリーンアップするには  
  
1.  
  **[データ パーティション]** ページのグリッドでパーティションを選択します。  
  
2.  
  **[既存のスナップショットをクリーンアップする]** をクリックします。  
  
##  <a name="TsqlProcedure"></a>Transact-sql の使用  
 パラメーター化されたフィルターを使ってパブリケーションをより詳細に管理するために、プログラムからレプリケーション ストアド プロシージャを使用して既存のパーティションを列挙できます。 既存のパーティションの作成と削除も行えます。 既存パーティションに関する次の情報も取得できます。  
  
-   パーティションのフィルター方法 ([SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) または [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) を使用)。  
  
-   パーティション スナップショットを生成するジョブの名前  
  
-   パーティション スナップショット ジョブが最後に実行された時刻  
  
 新しいサブスクリプションが初期化されたときに、2 つの部分から構成されるスナップショットの 2 番目の部分は要求時に生成できますが、下記の手順を実行することで、このスナップショットの生成方法を制御し、都合のよいときにこのスナップショットをあらかじめ生成できます。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)」をご覧ください。  
  
#### <a name="to-view-information-on-existing-partitions"></a>既存のパーティションに関する情報を表示するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_helpmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql) を実行します。 パブリケーションのパブリケーションの名前を指定します。 ** \@** Optional1つのフィルター条件に基づいて情報のみを返すには、 ** \@suser_sname**または** \@host_name**を指定します。  
  
#### <a name="to-define-a-new-partition-and-generate-a-new-partitioned-snapshot"></a>新しいパーティションを定義して、新しいパーティション スナップショットを生成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql) を実行します。 パブリケーションの名前と、次のいずれかのパーティションを定義するパラメーター化された値を指定します。 ** \@**  
  
    -   suser_sname-パラメーター化されたフィルターが SUSER_SNAME によって返される値によって定義されている場合[&#40;transact-sql&#41;](/sql/t-sql/functions/suser-sname-transact-sql)。 ** \@**  
  
    -   host_name-パラメーター化されたフィルターが HOST_NAME によって返される値によって定義されている場合[&#40;transact-sql&#41;](/sql/t-sql/functions/host-name-transact-sql)。 ** \@**  
  
2.  この新しいパーティションのパラメーター化スナップショットを作成し、初期化します。 詳しくは、「 [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
#### <a name="to-delete-a-partition"></a>パーティションを削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_dropmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql) を実行します。 パブリケーションのパブリケーションの名前と、次のいずれかのパーティションを定義するパラメーター化された値を指定します。 ** \@**  
  
    -   suser_sname-パラメーター化されたフィルターが SUSER_SNAME によって返される値によって定義されている場合[&#40;transact-sql&#41;](/sql/t-sql/functions/suser-sname-transact-sql)。 ** \@**  
  
    -   host_name-パラメーター化されたフィルターが HOST_NAME によって返される値によって定義されている場合[&#40;transact-sql&#41;](/sql/t-sql/functions/host-name-transact-sql)。 ** \@**  
  
     これにより、そのパーティションのスナップショット ジョブおよびすべてのスナップショット ファイルも削除されます。  
  
##  <a name="RMOProcedure"></a>レプリケーション管理オブジェクト (RMO) の使用  
 パラメーター化されたフィルターを使ってパブリケーションをより適切に管理するために、レプリケーション管理オブジェクト (RMO) を使用して、新しいサブスクライバー パーティションの作成、既存のサブスクライバー パーティションの列挙、およびサブスクライバーの削除をプログラムで行うことができます。 サブスクライバー パーティションを作成する方法の詳細については、「 [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」を参照してください。 既存のパーティションに関する次の情報を取得できます。  
  
-   パーティションの基になる値およびフィルター関数。  
  
-   サブスクライバーのパラメーター化されたスナップショットを生成するジョブの名前。  
  
-   パラメーター化されたスナップショット ジョブが最後に実行された日時。  
  
#### <a name="to-view-information-on-existing-partitions"></a>既存のパーティションに関する情報を表示するには  
  
1.  
  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  
  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を設定します。  
  
3.  
  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  
  <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> メソッドを呼び出して、結果を <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトの配列に渡します。  
  
5.  配列内の各 <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトに対して、必要なプロパティを取得します。  
  
#### <a name="to-delete-existing-partitions"></a>既存のパーティションを削除するには  
  
1.  
  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  
  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を設定します。  
  
3.  
  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  
  <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> メソッドを呼び出して、結果を <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトの配列に渡します。  
  
5.  配列内の各 <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトに対して、パーティションを削除するかどうかを決定します。 この決定は、通常、 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> プロパティまたは <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> プロパティの値に基づいて行います。  
  
6.  手順 2. の <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> オブジェクトで、 <xref:Microsoft.SqlServer.Replication.MergePublication> メソッドを呼び出します。 手順 5. の <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトを渡します。  
  
7.  削除する各パーティションに対して手順 6. を繰り返します。  
  
## <a name="see-also"></a>参照  
 [パラメーター化された行フィルター](../merge/parameterized-filters-parameterized-row-filters.md)   
 [パラメーター化されたフィルターを使用したマージパブリケーションのスナップショット](../snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
