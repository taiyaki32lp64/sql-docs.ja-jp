---
title: レッスン 1:テーブルの階層構造への変換 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 05906db66c2bf4948e91dddafa2cdd54aaf936ec
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907298"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>レッスン 1:テーブルの階層構造への変換
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
階層リレーションシップを表すために自己結合を使っているテーブルがある場合、このレッスンの説明に従って、それらのテーブルを階層構造に変換できます。 現在の表示から、 **hierarchyid**を使用した表示に移行するのは比較的簡単です。 移行後は、コンパクトで理解しやすい階層表示が可能になるため、ユーザーはさまざまな方法でインデックスを作成して効率的なクエリを実現できます。  
  
このレッスンでは、既存のテーブルを検証した後、 **hierarchyid** 列を含む新しいテーブルを作成し、そのテーブルにソース テーブルのデータを取り込みます。さらに、3 とおりのインデックス作成方法を紹介します。 このレッスンの内容は次のとおりです。  
 
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
- [AdventureWorks2017 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)をダウンロードする。

SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)に関するページをご覧ください。  

## <a name="examine-the-current-structure-of-the-employee-table"></a>Employee テーブルの現在の構造を確認する
サンプル Adventureworks2017 (以降) データベースには、**HumanResources** スキーマに含まれる **Employee** テーブルがあります。 元のテーブルを変更しないように、この手順では、 **Employee** テーブルのコピーを作成して **EmployeeDemo**という名前を付けます。 例を単純にするために、元のテーブルから 5 列だけをコピーします。 次に、 **HumanResources.EmployeeDemo** テーブルに対してクエリを実行し、 **hierarchyid** データ型が使用されていないテーブル内のデータ構造を確認します。  
  
### <a name="copy-the-employee-table"></a>Employee テーブルをコピーする  
  
1.  クエリ エディターのウィンドウで、次のコードを実行し、 **Employee** テーブルから新しいテーブルの **EmployeeDemo**にテーブル構造とデータをコピーします。 元のテーブルは既に hierarchyid を使用しているため、このクエリは従業員のマネージャーを取得するために必然的に階層をフラット化します。 この階層はこのレッスンの中で後ほど再構築します。

   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>EmployeeDemo テーブルの構造とデータを確認する  
  
-   この新しい **EmployeeDemo** テーブルは、新しい構造に移行可能な、既存のデータベースの一般的なテーブルを表しています。 クエリ エディター ウィンドウで次のコードを実行すると、テーブルで自己結合を使用して従業員と管理者のリレーションシップを示しているようすを確認できます。  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    結果は合計 290 行にわたります。  
  
**ORDER BY** 句を使用していることによって、出力では、各管理レベルの直属の部下がまとめて表示されていることに注意してください。 たとえば、**MgrID** 1 (ken0) の 7 人の直属の部下がすべて左右に並べて表示されています。 実際に **MgrID** 1 に直属するすべての人をグループ化することは、不可能ではありませんが、かなり難しくなります。  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>テーブルに既存の階層データを入力する
ここでは、新しいテーブルを作成して、そのテーブルに **EmployeeDemo** テーブルのデータを設定します。 この作業には、次の手順があります。  
  
-   **hierarchyid** 列を含む新しいテーブルを作成します。 この列を、既存の **EmployeeID** 列や **ManagerID** 列の代わりに使用してもかまいません。 ただし、これらの列は保持する必要があります。 これは、既存のアプリケーションがこれらの列を参照している可能性があるためでもあり、転送後のデータをわかりやすくするためでもあります。 テーブル定義では、 **OrgNode** が主キーであることを指定します。したがって、この列には一意の値を格納する必要があります。 **OrgNode** 列のクラスター化インデックスは、 **OrgNode** シーケンスのデータを格納します。    
-   各管理者に直属する従業員の数を追跡するために使用する一時テーブルを作成します。 
-   新しいテーブルを、 **EmployeeDemo** テーブルのデータを使用して設定します。  
  
### <a name="to-create-a-new-table-named-neworg"></a>NewOrg という名前の新しいテーブルを作成するには  
  
-   クエリ エディター ウィンドウで、次のコードを実行し、 **HumanResources.NewOrg**という名前の新しいテーブルを作成します。  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="create-a-temporary-table-named-children"></a>#Children という名前の一時テーブルを作成する  
  
1.  **Num** という名前の列を持つ **#Children** という名前の一時テーブルを作成します。この列は、各ノードの子の数を格納します。  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  インデックスを作成します。このインデックスによって、 **NewOrg** テーブルを設定するクエリの速度が大幅に向上します。  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>NewOrg テーブルを設定する  
  
1.  再帰クエリでは、集計を含むサブクエリが禁止されています。 代わりに、 **ROW_NUMBER()** メソッドを使用して [Num](../../t-sql/functions/row-number-transact-sql.md) 列を設定する次のコードによって、 **#Children** テーブルを設定します。  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  **#Children** テーブルを確認します。 **Num** 列に、各管理者の連続する番号がどのように格納されているかに注目してください。  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  **NewOrg** テーブルを設定します。 GetRoot メソッドと ToString メソッドを使用して **Num** 値を **hierarchyid** 形式に連結し、結果の階層値で **OrgNode** 列を更新します。  
  
    ```sql  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   

    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  **hierarchyid** 列は、文字形式に変換すると、よりわかりやすくなります。 次のコードを実行して、 **NewOrg** テーブルのデータを確認します。このコードには、 **OrgNode** 列の 2 つの表記が含まれています。  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    **LogicalNode** 列は、階層を表す読みやすいテキスト形式に **hierarchyid** 列を変換します。 残りの作業では、 `ToString()` メソッドを使用して、 **hierarchyid** 列の論理形式を表示します。  
  
5.  不要になった一時テーブルを削除します。  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>NewOrg テーブルの最適化
「[既存の階層データを使用したテーブルの設定](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)」の作業で作成した **NewOrd** テーブルにはすべての従業員情報が格納されており、その階層構造は **hierarchyid** データ型によって表されています。 ここでは、 **hierarchyid** 列の検索をサポートする新しいインデックスを追加します。  
  

**hierarchyid** 列 (**OrgNode**) は、 **NewOrg** テーブルの主キーです。 **OrgNode** 列に一意性を持たせるため、このテーブルには作成時に **PK_NewOrg_OrgNode** という名前のクラスター化インデックスが格納されています。 このクラスター化インデックスは、テーブルの深さ優先検索もサポートしています。  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>効率的な検索のため NewOrg テーブルにインデックスを付ける  
  
1.  階層の同じレベルでのクエリを容易にするには、 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) メソッドを使用して、階層内のレベルを格納する計算列を作成します。 次に、レベルと **Hierarchyid**に基づく複合インデックスを作成します。 次のコードを実行すると、計算列と幅優先のインデックスが作成されます。  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  **EmployeeID** 列に一意のインデックスを作成します。 これは、 **EmployeeID** の番号によって 1 人の従業員を検索する従来の単一参照です。 次のコードを実行すると、 **EmployeeID**のインデックスが作成されます。  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  次のコードを実行して、3 種類の各インデックスの順にテーブルからデータを取得します。  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  結果セットを比較して、順序がどのように格納されているかをインデックスの種類ごとに確認します。 それぞれの出力の最初の 4 行だけを以下に示します。  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    深さ優先のインデックス:従業員のレコードは、それぞれのマネージャーのレコードに隣接して格納されます。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    **EmployeeID** 優先のインデックス:行は **EmployeeID** の順に格納されます。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> 深さ優先のインデックスと幅優先のインデックスの違いを示す図については、「[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)」を参照してください。  
  
### <a name="drop-the-unnecessary-columns"></a>不要な列を削除する  
  
1.  **ManagerID** 列が表す従業員とマネージャーのリレーションシップは、現在は **OrgNode** 列によって表されるようになっています。 **ManagerID** 列を必要とするアプリケーションが他にない場合は、次のステートメントを使用してこの列を削除することを検討します。  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  **EmployeeID** 列も冗長です。 各従業員は、 **OrgNode** 列によって一意に識別されます。 **EmployeeID** 列を必要とするアプリケーションが他にない場合は、次のコードを使用して、インデックスを削除した後に列を削除することを検討します。  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>元のテーブルを新しいテーブルに置き換える  
  
1.  元のテーブルに追加のインデックスや制約が格納されている場合は、それらを **NewOrg** テーブルに追加します。  
  
2.  古い **EmployeeDemo** テーブルを新しいテーブルに置き換えます。 次のコードを実行すると、古いテーブルが削除され、新しいテーブルの名前がその古い名前に変更されます。  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  次のコードを実行して、最終的なテーブルを確認します。  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>次の手順
次の記事では、階層テーブルでデータを作成して管理する方法を説明します。 

詳細については、次の記事に進んでください
> [!div class="nextstepaction"]
> [次の手順](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)
