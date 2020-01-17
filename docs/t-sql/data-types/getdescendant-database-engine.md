---
title: GetDescendant (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3d015602e944416435c95aba6aaea1ead84b834a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077971"
---
# <a name="getdescendant-database-engine"></a>GetDescendant (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

親の子ノードを返します。
  
## <a name="syntax"></a>構文  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>引数  
*child1*  
NULL または現在のノードの子の **hierarchyid**。
  
*child2*  
NULL または現在のノードの子の **hierarchyid**。
  
## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: hierarchyid**
  
**CLR 戻り値の型:SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
親の子孫である 1 つの子ノードを返します。
-   parent が NULL の場合、NULL を返します。  
-   parent が NULL でなく、child1 と child2 の両方が NULL の場合、parent の子を返します。  
-   parent と child1 が NULL でなく、child2 が NULL の場合、child1 より大きい parent の子を返します。  
-   parent と child2 が NULL でなく、child1 が NULL の場合、child2 より小さい parent の子を返します。  
-   parent、child1、child2 が NULL でない場合、child1 より大きく child2 より小さい parent の子を返します。  
-   child1 が NULL でなく parent の子でない場合、例外が発生します。  
-   child2 が NULL でなく parent の子でない場合、例外が発生します。  
-   child1 >= child2 の場合は、例外が発生します。  
  
GetDescendant は決定的です。 そのため場合、 GetDescendant と呼ばれるは、同じ入力でが同じ出力常に生成されます。 ただし、生成された子の正確な ID は、例 C に示されているように、他のノードとの関係によって異なります。
  
## <a name="examples"></a>使用例  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. 最も小さい子孫ノードとして行を挿入  
ノード `/3/1/` の既存の従業員の部下として新しい従業員が採用されました。 使用して、新しい行を挿入するには、次のコードの実行、 GetDescendant メソッドとして、新しい行のノードを指定する引数を指定しないで /3 1/1/:`/3/1/1/`
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. 大きい子孫ノードとして行を挿入  
別の新しい従業員を雇用すると、次のコードを使用して、新しい行を挿入することを A. の実行例と同じ上司に報告、 GetDescendant メソッドは、child 1 引数を使用して、新しい行のノードが例 A でノードを従うことを指定するになる /3 1/2/:`/3/1/2/`
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. 既存の 2 つのノードの間に行を挿入  
例 A と同じ上司の部下として 3 人目の従業員が採用されました。この例では、例 A の `FirstNewEmployee` より大きく例 B の `SecondNewEmployee` より小さいノードに新しい行を挿入します。GetDescendant メソッドを使用して次のコードを実行します。 このコードでは、child1 引数と child2 引数の両方を使用して、新しい行のノードがノード `/3/1/1.1/` になるように指定しています。
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
A、B、および C# の例を完了すると、テーブルに追加されたノード ピアになります次 **hierarchyid** 値。
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
ノード `/3/1/1.1/` は、ノード `/3/1/1/` より大きいノードですが、階層のレベルは同じです。
  
### <a name="d-scalar-examples"></a>D. スカラーの例  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自由に挿入および削除のいずれかをサポートしている **hierarchyid** ノードです。 使用して GetDescendant(), 、任意の 2 つの間のノードを生成することは常に **hierarchyid** ノードです。 次のコードを実行すると、`GetDescendant` を使用してサンプル ノードが生成されます。
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. CLR の例  
次のコード例では `GetDescendant()` メソッドを呼び出します。
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
