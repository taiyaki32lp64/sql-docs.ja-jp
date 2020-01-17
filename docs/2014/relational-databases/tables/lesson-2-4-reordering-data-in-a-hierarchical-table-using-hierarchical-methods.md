---
title: 階層的な手法を使用した階層テーブルのデータの並べ替え Methods | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 7b8064c7-62c6-488d-84d2-57a5828fb907
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f289257d64a691a93d44d63d2a30991227802e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110110"
---
# <a name="reordering-data-in-a-hierarchical-table-using-hierarchical-methods"></a>階層的な手法を使用した階層テーブルのデータの並べ替え
  階層の再編成は、一般的なメンテナンス タスクです。 ここでは、UPDATE ステートメントを [GetReparentedValue](/sql/t-sql/data-types/getreparentedvalue-database-engine) メソッドと共に使用して、まず 1 つの行を階層内の新しい位置に移動します。 次に、サブツリー全体を新しい場所に移動します。  
  
 `GetReparentedValue` メソッドは 2 つの引数を受け取ります。 最初の引数は、変更する階層の一部を表します。 たとえば、階層が **/1/4/2/3/** の場合に、最後の 2 つのノード ( **2/3/** ) はそのままで、 **/1/4/** セクションを変更して階層を **/2/1/2/3/** にするときは、変更するノード ( **/1/4/** ) を最初の引数として指定する必要があります。 2 番目の引数には、新しい階層レベルを指定します。この例では、 **/2/1/** です。 2 つの引数には、異なるレベル数を指定することもできます。  
  
### <a name="to-move-a-single-row-to-a-new-location-in-the-hierarchy"></a>1 つの行を階層内の新しい位置に移動するには  
  
1.  現在、Wanida は Sariya に直属しています。 この手順では、Wanida を現在のノード **/1/1/** から移動して、Jill に直属するようにします。 Wanida の新しいノードは **/3/1/** になるので、最初の引数は **/1/** 、2 番目の引数は **/3/** になります。 これらは、Sariya と Jill の **OrgNode** 値に相当します。 Wanida を Sariya の組織から Jill の組織に移動するには、次のコードを実行します。  
  
    ```  
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
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
     Wanida がノード **/3/1/** に移動しています。  
  
### <a name="to-reorganize-a-section-of-a-hierarchy"></a>階層のセクションを再編成するには  
  
1.  多数の人員を一度に移動する方法を示すため、まず次のコードを実行して Wanida に直属するインターンを追加します。  
  
    ```  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Kevin が Wanida に直属するようになりました。Wanida は Jill に直属し、Jill は David に直属します。 したがって、Kevin のレベルは **/3/1/1/** です。 Jill の部下をすべて新しい管理者に移動するには、 **OrgNode** として **/3/** を持つすべてのノードを新しい値に更新します。 Kevin を Wanida に直属させたまま、Wanida を Sariya に直属するように更新するには、次のコードを実行します。  
  
    ```  
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
  
    ```  
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
/1/1//2      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
 Jill に直属していた組織のツリー全体 (Wanida と Kevin の両方) が Sariya に直属するようになりました。  
  
 階層のセクションを再編成するストアド プロシージャについては、「 [サブツリーの移動](../hierarchical-data-sql-server.md#BKMK_MovingSubtrees)」の「サブツリーの移動」を参照してください。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [概要:階層テーブルでデータを管理します。](lesson-2-5-summary-managing-data-in-a-hierarchical-table.md)  
  
  
