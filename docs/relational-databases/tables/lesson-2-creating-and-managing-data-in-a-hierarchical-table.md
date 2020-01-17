---
title: レッスン 2:階層テーブルでのデータの作成と管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 657dedcf4944a2540d1237b53fa8ea822c31ae3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031644"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>レッスン 2:階層テーブルでデータを作成して管理する
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
レッスン 1 では、既存のテーブルを変更して **hierarchyid** データ型を使用し、 **hierarchyid** 列に既存のデータ表現でデータを設定しました。 このレッスンでは、まず新しいテーブルを作成し、次に階層的な手法を使用してデータを挿入します。 その後、階層的な手法を使用して、データのクエリおよび操作を実行します。 

## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
- [AdventureWorks2017 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)をダウンロードする。

SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)に関するページをご覧ください。   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>hierarchyid データ型を使用してテーブルを作成する
EmployeeOrg という名前のテーブルを作成する例を次に示します。このテーブルには、従業員データと、それらの従業員のレポート階層が含まれています。 この例では、テーブルを AdventureWorks2017 データベースに作成しますが、これは任意です。 例をわかりやすくするために、このテーブルには 5 つの列のみ含まれています。  
  
-   OrgNode は、階層リレーションシップを格納する **hierarchyid** 列です。   
-   OrgLevel は OrgNode 列に基づく計算列であり、階層内での各ノードのレベルが格納されます。 これは、幅優先のインデックスに使用されます。  
-   EmployeeID には、給与処理などのアプリケーションで使用される通常の従業員識別番号が含まれます。 新しいアプリケーションの開発では、アプリケーションは OrgNode 列を使用でき、この個別の EmployeeID 列は不要です。   
-   EmpName には、従業員の名前が含まれます。    
-   Title には、従業員の役職が含まれます。  

## <a name="create-the-employeeorg-table"></a>EmployeeOrg テーブルを作成する  
  
1.  クエリ エディター ウィンドウで、次のコードを実行し、 `EmployeeOrg` テーブルを作成します。 `OrgNode` 列を、クラスター化インデックスのある主キーとして指定すると、深さ優先のインデックスが作成されます。  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  次のコードを実行して `OrgLevel` 列と `OrgNode` 列に複合インデックスを作成し、効率的な幅優先の検索をサポートします。  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
これでテーブルはデータを受け入れる準備ができました。 次に、階層的な手法を使用してテーブルにデータを入力します。   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>階層的な手法を使用して階層テーブルにデータを入力する
AdventureWorks2017 のマーケティング部門には 8 人の従業員が勤務しています。 従業員の階層は、次のようになります。  
  
**David**( **EmployeeID 6** ) は Marketing Manager です。 **David**には、次の 3 人の Marketing Specialist が直属します。  
  
-   **Sariya**( **EmployeeID 46** )  
  
-   **John**( **EmployeeID 271** )  
  
-   **Jill**( **EmployeeID 119** )  
  
Marketing Assistant の **Wanida** (**EmployeeID** 269) は **Sariya**に直属し、Marketing Assistant の **Mary** (**EmployeeID** 272) は **John**に直属します。  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>階層ツリーのルートを挿入する  
  
1.  次の例では、Marketing Manager である **David** を、階層のルートに位置するテーブルに挿入します。 **OrdLevel** 列は計算列です。 したがって、INSERT ステートメントの一部ではありません。 この最初のレコードでは、 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) メソッドを使用して、この最初のレコードを階層のルートとして挿入します。  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  テーブルの最初の行を調べるには、次のコードを実行します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
前のレッスンと同様、 `ToString()` メソッドを使用して、 **hierarchyid** データ型をよりわかりやすい形式に変換します。  
  
### <a name="insert-a-subordinate-employee"></a>部下を挿入する  
  
1.  **Sariya** は **David**に直属します。 **Sariya** のノードを挿入するには、 **hierarchyid** データ型の適切な **OrgNode**値を作成する必要があります。 次のコードでは、 **hierarchyid** データ型の変数を作成して、テーブルのルート OrgNode 値をその変数に代入します。 次に、その変数を [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) メソッドと共に使用して、部下のノードである行を挿入します。 `GetDescendant` は、2 つの引数を受け取ります。 引数値の次のオプションを確認してください。  
  
    -   parent が NULL の場合、 `GetDescendant` は NULL を返します。  
    -   parent が NULL でなく、child1 と child2 の両方が NULL の場合、 `GetDescendant` は parent の子を返します。  
    -   parent と child1 が NULL でなく、child2 が NULL の場合、 `GetDescendant` は child1 より大きい parent の子を返します。   
    -   parent と child2 が NULL でなく、child1 が NULL の場合、 `GetDescendant` は child2 より小さい parent の子を返します。   
    -   parent、child1、child2 のすべてが NULL でない場合、 `GetDescendant` は child1 より大きく child2 より小さい parent の子を返します。  
  
    テーブルにはルート以外にまだ 1 行もないため、次のコードではルートの `(NULL, NULL)` 引数を使用します。 **Sariya**を挿入するには、次のコードを実行します。  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  テーブルにクエリを実行してエントリがどのように表示されるかを確認するには、最初の手順のクエリを繰り返します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>新しいノードを入力するためのプロシージャを作成する  
  
1.  データの入力を簡略化するには、次のストアド プロシージャを作成して、 **EmployeeOrg** テーブルに従業員を追加します。 このプロシージャは、追加される従業員に関する入力値を受け取ります。 これには、新しい従業員の管理者の **EmployeeID** 、新しい従業員の **EmployeeID** 番号、従業員の名と役職が含まれます。 このプロシージャでは、 `GetDescendant()` と [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) メソッドも使用します。 プロシージャを作成するには、次のコードを実行します。  
  
    ```sql  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  次の例では、 **David**の直接または間接的な部下である残り 4 人の従業員を追加します。  
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  **EmployeeOrg** テーブルの行を調べるには、再び次のクエリを実行します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    /1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
テーブルに、マーケティング組織が完全に作成されました。  

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>階層的な手法を使用して階層テーブルをクエリする
HumanResources.EmployeeOrg テーブルに完全にデータが設定されたので、ここでは階層的な手法のいくつかを使用して階層をクエリする方法を示します。  
  
### <a name="find-subordinate-nodes"></a>下位ノードを検索する  
  
1.  Sariya には 1 人の部下がいます。 Sariya の部下に対するクエリを実行するには、 [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) メソッドを使用する次のクエリを実行します。  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    結果には、Sariya と Wanida の両方が表示されます。 Sariya は、0 レべルの子孫であるために表示されています。 Wanida は 1 レベルの子孫です。  
  
2.  [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) メソッドを使用してこの情報に対してクエリを実行することもできます。 `GetAncestor` 返そうとしているレベルの引数を受け取ります。 Wanida は Sariya よりも 1 つ下のレベルであるため、次のコードに示すように `GetAncestor(1)` を使用します。  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    この場合、結果には Wanida のみが表示されます。  
  
3.  次に、 `@CurrentEmployee` を David (EmployeeID 6) に、レベルを 2 にそれぞれ変更します。 次のコードを実行した場合も Wanida が返されます。  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    この場合は、David に直属する 2 つ下のレベルの Mary も返されます。  
  
## <a name="use-getroot-and-getlevel"></a>GetRoot と GetLevel を使用する  
  
1.  階層が大きくなるにつれ、メンバーが階層内のどこに位置するのかを確認するのが難しくなります。 各行が階層内の何レベル下にあるかを検索するには、 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) メソッドを使用します。 すべての行のレベルを表示するには次のコードを実行します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  階層内のルート ノードを検索するには、 [GetRoot](../../t-sql/data-types/getroot-database-engine.md) メソッドを使用します。 次のコードは、ルートである 1 つの行を返します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>階層的な手法を使用して階層テーブルのデータを並べ替える
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
階層の再編成は、一般的なメンテナンス タスクです。 ここでは、UPDATE ステートメントを [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) メソッドと共に使用して、まず 1 つの行を階層内の新しい位置に移動します。 次に、サブツリー全体を新しい場所に移動します。  
  
`GetReparentedValue` メソッドは 2 つの引数を受け取ります。 最初の引数は、変更する階層の一部を表します。 たとえば、階層が **/1/4/2/3/** の場合に、最後の 2 つのノード ( **2/3/** ) はそのままで、 **/1/4/** セクションを変更して階層を **/2/1/2/3/** にするときは、変更するノード ( **/1/4/** ) を最初の引数として指定する必要があります。 2 番目の引数には、新しい階層レベルを指定します。この例では、 **/2/1/** です。 2 つの引数には、異なるレベル数を指定することもできます。  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>単一行を階層内の新しい位置に移動する  
  
1.  現在、Wanida は Sariya に直属しています。 この手順では、Wanida を現在のノード **/1/1/** から移動して、Jill に直属するようにします。 Wanida の新しいノードは **/3/1/** になるので、最初の引数は **/1/** 、2 番目の引数は **/3/** になります。 これらは、Sariya と Jill の **OrgNode** 値に相当します。 Wanida を Sariya の組織から Jill の組織に移動するには、次のコードを実行します。  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  結果を表示するには、次のコードを実行します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    Wanida がノード **/3/1/** に移動しています。  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>階層のセクションを再編成する  
  
1.  多数の人員を一度に移動する方法を示すため、まず次のコードを実行して Wanida に直属するインターンを追加します。  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Kevin が Wanida に直属するようになりました。Wanida は Jill に直属し、Jill は David に直属します。 したがって、Kevin のレベルは **/3/1/1/** です。 Jill の部下をすべて新しい管理者に移動するには、 **OrgNode** として **/3/** を持つすべてのノードを新しい値に更新します。 Kevin を Wanida に直属させたまま、Wanida を Sariya に直属するように更新するには、次のコードを実行します。  
  
    ```sql  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  結果を表示するには、次のコードを実行します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
Jill に直属していた組織のツリー全体 (Wanida と Kevin の両方) が Sariya に直属するようになりました。  
  
階層のセクションを再編成するストアド プロシージャについては、「 [サブツリーの移動](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees)」の「サブツリーの移動」を参照してください。  
  
