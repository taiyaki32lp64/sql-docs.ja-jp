---
title: フルテキスト インデックスの作成 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 52fc7d3d43c1f0adcf7ab94d78cf301254a9a18d
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903876"
---
# <a name="populate-full-text-indexes"></a>フルテキスト インデックスの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  フルテキスト インデックスの作成と保持では、 *作成* (または *クロール*) と呼ばれるプロセスを使用してインデックスが作成されます。  
  
##  <a name="types"></a> Types of population  
フルテキスト インデックスは次の種類の作成に対応しています。
-   **すべて**のカタログの作成
-   **変更の追跡**に基づく自動または手動作成
-   **タイムスタンプ**に基づく増分作成
  
## <a name="full-population"></a>すべてのカタログの作成  
 すべてのカタログの作成では、テーブルまたはインデックス付きビューのすべての行に対してインデックス エントリが作成されます。 フルテキスト インデックスのすべてのカタログの作成では、ベース テーブルまたはインデックス付きビューのすべての行に対してインデックス エントリが作成されます。  
  
既定では、新しいフルテキスト インデックスが作成されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってすぐにそのカタログが作成されます。
-   一方で、すべてのカタログの作成では大量のリソースが消費される可能性があります。 このため、ピーク期間にフルテキスト インデックスを作成する場合は、すべてのカタログの作成をオフピーク時間まで遅らせることが推奨されています (特にフルテキスト インデックスのベース テーブルが大きい場合)。
-   一方で、インデックスが属するフルテキスト カタログは、そのすべてのフルテキスト インデックスのカタログが作成されるまで使用できません。

すぐに値を入力せずにフルテキスト インデックスを作成するには、`CREATE FULLTEXT INDEX` ステートメントに `CHANGE_TRACKING OFF, NO POPULATION` 句を指定します。 `CHANGE_TRACKING MANUAL` を指定する場合、Full-Text Engine は、`START FULL POPULATION` または `START INCREMENTAL POPULATION` により `ALTER FULLTEXT INDEX` ステートメントが実行されるまで、新しいフルテキスト インデックスに値を入力しません。 

### <a name="example---create-a-full-text-index-without-running-a-full-population"></a>例 - 完全作成を実行せずにフルテキスト インデックスを作成する  
 次の例では、 `Production.Document` サンプル データベースの `AdventureWorks` テーブルにフルテキスト インデックスを作成します。 この例では `WITH CHANGE_TRACKING OFF, NO POPULATION` を利用し、最初の完全作成を遅らせます。  
  
```sql
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="example---run-a-full-population-on-a-table"></a>例 - テーブルで完全作成を実行する  
 次の例では、 `Production.Document` サンプル データベースの `AdventureWorks` テーブルで完全作成を実行します。  
  
```sql
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
   
## <a name="population-based-on-change-tracking"></a>変更の追跡に基づく作成
 必要に応じて、変更の追跡を使用して、完全作成が最初に実行された後のフルテキスト インデックスを保持することができます。 変更の追跡には若干のオーバーヘッドが伴います。これは、前回のカタログ作成以降にベース テーブルに対して行われた変更を追跡するテーブルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で保持されるためです。 変更の追跡を使用すると、ベース テーブルまたはインデックス付きビューで更新、削除、または挿入によって変更された行の記録が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で保持されます。 WRITETEXT や UPDATETEXT によるデータの変更は、フルテキスト インデックスには反映されず、変更の監視でも取得されません。  
  
> [!NOTE]  
>  **timestamp** 列を含んでいるテーブルには、変更の追跡の代わりに増分作成を使用できます。  
  
 インデックス作成時に変更の追跡を有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で新しいフルテキスト インデックスが作成された直後にそのインデックスですべてのカタログの作成が実行されます。 それ以降は、変更が追跡されてフルテキスト インデックスに反映されます。

### <a name="enable-change-tracking"></a>変更の追跡を有効化
変更の追跡には、次の 2 種類があります。
-   自動 (`CHANGE_TRACKING AUTO` オプション)。 既定では自動で変更が追跡されます。
-   手動 (`CHANGE_TRACKING MANUAL` オプション)。   
  
 変更の追跡の種類によって、フルテキスト インデックスのカタログ作成方法が次のように決まります。  
  
-   **自動でのカタログ作成**  
  
     既定では、あるいは `CHANGE_TRACKING AUTO` を指定した場合、Full-Text Engine によってフルテキスト インデックスに自動的にカタログが作成されます。 すべてのカタログの作成が最初に実行された後に、ベース テーブルでデータが変更されると変更が追跡され、追跡された変更が自動的に反映されます。 ただし、フルテキスト インデックスはバックグラウンドで更新されるため、変更が直ちにインデックスに反映されないこともあります。  
  
     **自動でのカタログ作成を指定して変更の追跡を開始するには**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ...WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ...SET CHANGE_TRACKING AUTO  
  
    **例 - 自動で変更が追跡されるようにフルテキスト インデックスを変更する**  
    次の例では、 `HumanResources.JobCandidate` サンプル データベースの `AdventureWorks` テーブルで、自動作成に変更の追跡を使用するようにフルテキスト インデックスを変更します。  
  
    ```sql  
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
    GO   
    ```  
  
-   **手動でのカタログ作成**  
  
     CHANGE_TRACKING MANUAL を指定すると、Full-Text Engine ではフルテキスト インデックスに対して手動作成が使用されます。 完全作成が最初に実行された後に、ベース テーブルでデータが変更されると変更が追跡されます。 ただしその変更は、ALTER FULLTEXT INDEX ...START UPDATE POPULATION ステートメントを実行するまで反映されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用すると、この [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを定期的に呼び出すことができます。  
  
     **手動でのカタログ作成を指定して変更の追跡を開始するには**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ...WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ...SET CHANGE_TRACKING MANUAL  
  
    **例 - 手動で変更を追跡するようにフルテキスト インデックスを作成する**  
    次の例では、 `HumanResources.JobCandidate` サンプル データベースの `AdventureWorks` テーブルで、手動でのカタログ作成を指定した変更の追跡を使用するフルテキスト インデックスを作成します。  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
    CREATE FULLTEXT CATALOG ft AS DEFAULT;  
    CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
       KEY INDEX ui_ukJobCand   
       WITH CHANGE_TRACKING=MANUAL;  
    GO  
    ```  
  
    **例 - 手動作成を実行する**  
    次の例では、 `HumanResources.JobCandidate` サンプル データベースの `AdventureWorks` テーブルで、変更が追跡されるフルテキスト インデックスに対して手動でのカタログ作成を実行します。  
  
    ```sql 
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
    GO  
    ```
   
### <a name="disable-change-tracking"></a>変更の追跡を無効化 
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ...WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ...SET CHANGE_TRACKING OFF  
   
  
## <a name="incremental-population-based-on-a-timestamp"></a>タイムスタンプに基づく増分作成  
 増分作成は、フルテキスト インデックスに手動でカタログを作成するためのもう 1 つのメカニズムです。 テーブルで大量の挿入が行われた場合は、手動でのカタログ作成よりも増分作成を使用した方が効率的です。
 
 増分作成は、CHANGE_TRACKING が MANUAL または OFF に設定されているフルテキスト インデックスに対して実行できます。 
  
 増分作成では、インデックスが設定されたテーブルに **timestamp** データ型の列が存在する必要があります。 **timestamp** 型の列が存在しない場合には、増分作成を実行できません。   

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**timestamp** 列を使用して前回の作成後に変更された行が識別されます。 増分作成では、前回のカタログ作成後、または作成中に追加、削除、または変更された行のフルテキスト インデックスが更新されます。 作成が終わると、Full-Text Engine は新しい **timestamp** 型の値を記録します。 この値は、SQL Gatherer が検出した **timestamp** 型の最大値です。 次回、増分作成を開始するとき、この値が使用されます。  
 
増分作成が要求された結果、完全作成が行われることもあります。
-   **timestamp** 型の列を含んでいないテーブルで増分作成を要求すると、完全作成が実行されます。
-   フルテキスト インデックスの最初のカタログ作成が増分作成の場合、すべての行にインデックスが付けられるため、完全作成と同じになります。 
-   前回のカタログ作成後にテーブルのフルテキスト インデックスに影響するようなメタデータの変更があった場合、増分作成の要求はすべてのカタログの作成として実行されます。 これには、列、インデックス、またはフルテキスト インデックスの定義を変更したことによるメタデータの変更が含まれます。 

### <a name="run-an-incremental-population"></a>増分作成を実行する
  
 増分作成を実行するには、`START INCREMENTAL POPULATION` 句を利用して `ALTER FULLTEXT INDEX` ステートメントを実行します。  
  
###  <a name="create"></a> 増分作成のスケジュールを作成または変更する   
  
1.  Management Studio で、オブジェクト エクスプローラーでサーバーを展開します。  
  
2.  **[データベース]** を展開し、フルテキスト インデックスを含むデータベースを展開します。  
  
3.  **[テーブル]** を展開します。  
  
    フルテキスト インデックスが定義されているテーブルを右クリックし、 **[フルテキスト インデックス]** コンテキスト メニューの **[フルテキスト インデックス]** をクリックして、 **[プロパティ]** をクリックします。 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスが表示されます。  

    > [!IMPORTANT]  
    >  ベース テーブルまたはビューに **timestamp** データ型の列が含まれていない場合は、増分作成はできません。
      
1.  **[ページの選択]** ペインで **[スケジュール]** をクリックします。  
  
     このページでは、フルテキスト インデックスのベース テーブルまたはインデックス付きビューの増分作成を開始する SQL Server エージェント ジョブのスケジュールを作成または管理できます。  

     次のオプションがあります。  
  
    -   新しいスケジュールを**作成**するには、 **[新規作成]** をクリックします。  
  
        スケジュールを作成できる **[新しいフルテキスト インデックス テーブルのスケジュール]** ダイアログ ボックスが表示されます。 スケジュールを保存するには、 **[OK]** をクリックします。  
  
        > [!IMPORTANT]  
        >  *[フルテキスト インデックスのプロパティ]* ダイアログ ボックスを閉じると、新しいスケジュールが SQL Server エージェント ジョブ (*database_name*. **table_name** でテーブルの増分作成を開始) に関連付けられます。 同じフルテキスト インデックスのスケジュールを複数作成した場合、すべてのスケジュールで同じジョブが使用されます。  
  
    -   既存のスケジュールを**変更**するには、それを選択し、 **[編集]** をクリックします。  
  
         スケジュールを変更できる **[新しいフルテキスト インデックス テーブルのスケジュール]** ダイアログ ボックスが表示されます。  
  
        > [!NOTE]  
        >  SQL Server エージェント ジョブの変更については、「[ジョブの変更](../../ssms/agent/modify-a-job.md)」を参照してください。  
  
    -   既存のスケジュールを**削除**するには、それを選択し、 **[削除]** をクリックします。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   

##  <a name="crawl"></a> フルテキスト作成 (クロール) で発生したエラーのトラブルシューティング  
クロール時にエラーが発生すると、フルテキスト検索クロール ログ記録機能によってクロール ログが作成および保持されます。このログはプレーンテキスト ファイルです。 各クロール ログは特定のフルテキスト カタログに対応します。 既定では、所与のインスタンス (この例では、既定のインスタンス) のクロール ログは `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG` フォルダーにあります。
 
クロール ログは次のような規則に従って命名されます。  
  
`SQLFT<DatabaseID><FullTextCatalogID>.LOG[<n>]`
  
クロール ログ ファイルの可変部分は次のようになります。
-   <**DatabaseID**> - データベースの ID。 \<**dbid**> は、ゼロで始まる 5 桁の数字です。  
-   <**FullTextCatalogID**> - フルテキスト カタログ ID。 \<**catid**> は、ゼロで始まる 5 桁の数字です。  
-   <**n**> - 同じフルテキスト カタログに 1 つ以上のクロール ログが存在することを示す整数です。  
  
 たとえば、`SQLFT0000500008.2` はデータベース ID が 5 で、フルテキスト カタログ ID が 8 のクロール ログ ファイルです。 ファイル名の最後の 2 は、このデータベースとカタログのペアに 2 つのクロール ログ ファイルが存在することを示しています。  

## <a name="see-also"></a>参照  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [フルテキスト検索の概要](../../relational-databases/search/get-started-with-full-text-search.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
