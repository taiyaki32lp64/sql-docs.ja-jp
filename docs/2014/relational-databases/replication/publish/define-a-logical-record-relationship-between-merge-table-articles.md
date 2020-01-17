---
title: マージ テーブル アーティクル間に論理レコード リレーションシップを定義する | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c1c5be804f60fa57b677a418c19d8aadee23f22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691659"
---
# <a name="define-a-logical-record-relationship-between-merge-table-articles"></a>マージ テーブル アーティクル間に論理レコード リレーションシップを定義する
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、マージ テーブル アーティクル間に論理レコード リレーションシップを定義する方法について説明します。  
  
 マージ レプリケーションでは、さまざまなテーブルの関連する行の間にリレーションシップを定義できます。 これらの行は、同期の際にトランザクション単位として処理できます。 論理レコードは、2 つのアーティクルの間に定義できます。結合フィルター リレーションシップの有無は関係ありません。 詳細については、「[Group Changes to Related Rows with Logical Records](../merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **マージ テーブル アーティクル間に論理レコード リレーションシップを定義するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションに対するサブスクリプションが初期化された後に、論理レコードを追加、変更、または削除した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **[結合の追加]** ダイアログ ボックスで論理レコードを定義します。このダイアログ ボックスは、パブリケーションの新規作成ウィザードと **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
 **[結合の追加]** ダイアログ ボックスで論理レコードを定義できるのは、マージ パブリケーションの結合フィルターに論理レコードが適用されている場合だけです。また、パブリケーションが、事前計算済みパーティションを使用するための要件を満たしている必要もあります。 結合フィルターに適用されていない論理レコードを定義して、論理レコード レベルでの競合の検出と解決を設定するには、ストアド プロシージャを使用する必要があります。  
  
#### <a name="to-define-a-logical-record-relationship"></a>論理レコード リレーションシップを定義するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内の行フィルターを選択します。  
  
     論理レコード リレーションシップは、行フィルターを拡張する結合フィルターに関連付けられます。 したがって、先に行フィルターが定義されていないと、行フィルターを結合で拡張して論理レコード リレーションシップを適用することはできません。 1 つの結合フィルターが定義されると、この結合フィルターを別の結合フィルターを使用して拡張できます。 結合フィルターの定義の詳細については、「 [マージ アーティクル間の結合フィルターの定義および変更](define-and-modify-a-join-filter-between-merge-articles.md)」を参照してください。  
  
2.  **[追加]** をクリックし、 **[選択したフィルターを拡張するために結合を追加する]** をクリックします。  
  
3.  **[結合の追加]** ダイアログ ボックスで結合フィルターを定義してから、 **[論理レコード]** チェック ボックスをオンにします。  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
#### <a name="to-delete-a-logical-record-relationship"></a>論理レコード リレーションシップを削除するには  
  
-   論理レコード リレーションシップのみを削除するか、または論理レコード リレーションシップとそれに関連付けられている結合フィルターを削除します。  
  
     論理レコード リレーションシップのみを削除するには  
  
    1.  パブリケーションの新規作成ウィザードの **[行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内の論理レコード リレーションシップに関連付けられている結合フィルターを選択し、 **[編集]** をクリックします。  
  
    2.  **[結合の編集]** ダイアログ ボックスで、 **[論理レコード]** チェック ボックスをオフにします。  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     論理レコード リレーションシップとそれに関連付けられている結合フィルターを削除するには  
  
    -   パブリケーションの新規作成ウィザードの **[行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[削除]** をクリックします。 削除する結合フィルター自体が他の結合によって拡張されている場合は、それらの結合も削除されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 プログラムでレプリケーション ストアド プロシージャを使用して、アーティクル間に論理レコード リレーションシップを指定できます。  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>関連する結合フィルターを使用せずに論理レコード リレーションシップを定義するには  
  
1.  フィルター選択されたアーティクルがパブリケーションに含まれている場合、 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)を実行して、結果セットの **use_partition_groups** の値を確認します。  
  
    -   値が **1**の場合、事前計算済みパーティションが既に使用されています。  
  
    -   値が **0**の場合、パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) を実行します。 **@property** に **use_partition_groups** を指定し、 **@value** に **true** を指定します。  
  
        > [!NOTE]  
        >  パブリケーションで事前計算済みパーティションがサポートされない場合、論理レコードは使用できません。 詳細については、[事前計算済みパーティションによるパラメーター化されたフィルター パフォーマンスの最適化](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)に関するページで、事前計算済みパーティションを使用するための要件をご覧ください。  
  
    -   この値が NULL の場合、パブリケーションの初期スナップショットを生成するためにスナップショット エージェントを実行する必要があります。  
  
2.  論理レコードを構成するアーティクルが存在しない場合は、パブリッシャー側のパブリケーション データベースに対して [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行します。 論理レコードの競合の検出と解決に関するオプションを次の中から 1 つ指定します。  
  
    -   論理レコードの関連する行で発生する競合を検出し、解決するには、 **@value** には **@logical_record_level_conflict_detection** 」および「 **@logical_record_level_conflict_resolution** 」をご覧ください。  
  
    -   標準的な行または列レベルの競合の検出と解決を使用するには、値を指定`false`の **@logical_record_level_conflict_detection** と **@logical_record_level_conflict_resolution** 、既定値します。  
  
3.  論理レコードを構成する各アーティクルに対して、手順 2. を実行します。 論理レコード内の各アーティクルに使用する競合の検出および解決のオプションは、すべて同じである必要があります。 詳しくは、「 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)」をご覧ください。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)を実行します。 **@publication** を指定します。リレーションシップの 1 つのアーティクルの名前を **@article** に、もう 1 つのアーティクルの名前を **@join_articlename** に指定します。リレーションシップの名前を **@filtername** に、2 つのアーティクル間のリレーションシップを定義する句を **@join_filterclause** に、結合の種類を **@join_unique_key** に指定します。次のいずれかの値を **@filter_type** に指定します。  
  
    -   **2** - 論理リレーションシップを定義します。  
  
    -   **3** - 結合フィルターを使用した論理リレーションシップを定義します。  
  
    > [!NOTE]  
    >  結合フィルターを使用しない場合、2 つのアーティクル間のリレーションシップの方向はあまり重要でなくなります。  
  
5.  パブリケーションの他の論理レコード リレーションシップについても、手順 2. をそれぞれ実行します。  
  
#### <a name="to-change-conflict-detection-and-resolution-for-logical-records"></a>論理レコードにおける競合の検出と解決の方法を変更するには  
  
1.  論理レコードの関連する行で発生する競合を検出し、解決するには、次の手順を実行します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 **@property** に **logical_record_level_conflict_detection** を指定し、 **@value** に **true** を指定します。 **@force_invalidate_snapshot** と **@force_reinit_subscription** に **1** を指定します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 **@property** に **logical_record_level_conflict_resolution** を指定し、 **@value** に **true** を指定します。 **@force_invalidate_snapshot** と **@force_reinit_subscription** に **1** を指定します。  
  
2.  標準の行レベルまたは列レベルの競合の検出と解決を使用するには、次の手順を実行します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 値を指定**logical_record_level_conflict_detection**の **@property** の値と`false`の **@value** します。 **@force_invalidate_snapshot** と **@force_reinit_subscription** に **1** を指定します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 値を指定**logical_record_level_conflict_resolution**の **@property** の値と`false`の **@value** します。 **@force_invalidate_snapshot** と **@force_reinit_subscription** に **1** を指定します。  
  
#### <a name="to-remove-a-logical-record-relationship"></a>論理レコード リレーションシップを削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して次のクエリを実行し、指定されたパブリケーションに対して定義されているすべての論理レコード リレーションシップに関する情報を返します。  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../snippets/tsql/SQL15/replication/howto/tsql/createlogicalrecordpub.sql#sp_returnmergelogicalrecords)]  
  
     結果セット内の `filtername` 列で削除されている論理レコード リレーションシップの名前を確認します。  
  
    > [!NOTE]  
    >  このクエリは、 [sp_helpmergefilter](/sql/relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql)と同じ情報を返します。ただし、このシステム ストアド プロシージャは、結合フィルターでもある論理レコード リレーションシップに関する情報のみ返します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_dropmergefilter](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql)を実行します。 **@publication** を指定し、リレーションシップ内の 1 つのアーティクルの名前を **@article** に、手順 1 のリレーションシップの名前を **@filtername** に指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、既存のパブリケーションで事前計算済みパーティションを有効にし、 `SalesOrderHeader` テーブルと `SalesOrderDetail` テーブルの 2 つの新しいアーティクルを含む論理レコードを作成しています。  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../snippets/tsql/SQL15/replication/howto/tsql/createlogicalrecordpub.sql#sp_addmergelogicalrecord)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
> [!NOTE]  
>  マージ レプリケーションを使用して、論理レコード レベルで追跡および解決する競合を指定できますが、これらのオプションは RMO を使用して設定できません。  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>関連する結合フィルターを使用せずに論理レコード リレーションシップを定義するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成し、パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティと <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定して、手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> プロパティが <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>に設定されている場合、これを <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>に設定します。  
  
5.  論理レコードを構成するアーティクルが存在しない場合は、 <xref:Microsoft.SqlServer.Replication.MergeArticle> クラスのインスタンスを作成し、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.Name%2A>にアーティクル名を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>にパブリケーション名を指定します。  
  
    -   (省略可) アーティクルが行方向にフィルター選択される場合、 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> プロパティに行フィルター句を指定します。 このプロパティを使用して、静的行フィルターまたはパラメーター化された行フィルターを指定します。 詳しくは、「 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
     詳しくは、「 [Define an Article](define-an-article.md)」をご覧ください。  
  
6.  <xref:Microsoft.SqlServer.Replication.Article.Create%2A> メソッドを呼び出します。  
  
7.  論理レコードを構成するアーティクルごとに、手順 5. と 6. を繰り返します。  
  
8.  <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> クラスのインスタンスを作成して、アーティクル間の論理レコード リレーションシップを定義します。 その後、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> プロパティに論理レコード リレーションシップの子アーティクルの名前を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> プロパティに論理レコード リレーションシップの既存の親アーティクルの名前を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> プロパティに論理レコード リレーションシップの名前を指定します。  
  
    -   リレーションシップを定義する式を <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> プロパティに指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> の値を <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> プロパティに指定します。 論理レコード リレーションシップが結合フィルターでもある場合は、このプロパティに <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> の値を指定します。 詳細については、「[Group Changes to Related Rows with Logical Records](../merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
9. リレーションシップ内の子アーティクルを表すオブジェクトに対して <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> メソッドを呼び出します。 手順 8. の <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> オブジェクトを渡して、リレーションシップを定義します。  
  
10. パブリケーションの他の論理レコード リレーションシップについても、手順 8. と 9. をそれぞれ実行します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 この例では、 `SalesOrderHeader` テーブルと `SalesOrderDetail` テーブルの 2 つの新しいアーティクルを含む論理レコードを作成しています。  
  
 [!code-csharp[HowTo#rmo_CreateLogicalRecord](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## <a name="see-also"></a>関連項目  
 [マージ アーティクル間の結合フィルターの定義および変更](define-and-modify-a-join-filter-between-merge-articles.md)   
 [マージ アーティクルのパラメーター化された行フィルターの定義と変更](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [静的行フィルターの定義と変更](define-and-modify-a-static-row-filter.md)   
 [論理レコードによる関連行への変更のグループ化](../merge/group-changes-to-related-rows-with-logical-records.md)   
 [事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)   
 [論理レコードによる関連行への変更のグループ化](../merge/group-changes-to-related-rows-with-logical-records.md)  
  
  
