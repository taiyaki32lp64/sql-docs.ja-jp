---
title: GetReparentedValue (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reparent_TSQL
- Reparent
dev_langs:
- TSQL
helpviewer_keywords:
- Reparent [Database Engine]
ms.assetid: f47f8e25-08ef-498b-84f4-a317aca1f358
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8ff469d92165d12bac6d10bed6682d29ea162eb7
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278360"
---
# <a name="getreparentedvalue-database-engine"></a>GetReparentedValue (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

ルートからのパスが _newRoot_ のパスで、_oldRoot_ からのパスが続くノードを返します。
  
## <a name="syntax"></a>構文  
  
```sql
-- Transact-SQL syntax  
node. GetReparentedValue ( oldRoot, newRoot )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetReparentedValue ( SqlHierarchyId oldRoot , SqlHierarchyId newRoot )  
```  
  
## <a name="arguments"></a>引数  
_oldRoot_  
変更される階層のレベルを表すノードである **hierarchyid**。
  
_newRoot_  
ノードを表す **hierarchyid** です。 現在のノードの _oldRoot_ セクションを置換し、ノードを移動します。
  
## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: hierarchyid**
  
**CLR 戻り値の型:SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
_oldRoot_ から _newRoot_ にノードを移動することでツリーを変更するために使用されます。 GetReparentedValue は、階層内の新しい場所に階層ノードを移動するために使用されます。 **hierarchyid** データ型を表しますが、階層構造は強制されません。 ユーザーは、hierarchyid 新しい位置に対して正しく構成されていることを確認する必要があります。 一意のインデックス、 **hierarchyid** エントリの重複を防止のデータ型に役立ちます。 サブツリー全体の移動例については、「[階層データ &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)」を参照してください。
  
## <a name="examples"></a>使用例  
  
### <a name="a-comparing-two-node-locations"></a>A. 2 つのノードの位置の比較  
次の例は、ノードの現在の hierarchyid と、 移動されたノードが **\@NewParent** ノードの子孫になる場合のノードの **hierarchyid** も示します。 この例では、`ToString()` メソッドを使用して階層関係を表示しています。
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ;  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- who is /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- who is /2/3/  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
(@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) ).ToString() AS Proposed_OrgNode_AS_Text,  
OrgNode AS Current_OrgNode,  
@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) AS Proposed_OrgNode,  
*  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = @SubjectEmployee ;  
GO  
```  
  
### <a name="b-updating-a-node-to-a-new-location"></a>B. 新しい位置へのノードの更新  
次の例では、UPDATE ステートメントで `GetReparentedValue()` を使用して、ノードを階層内の古い位置から新しい位置に移動しています。
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ; -- Node /1/1/2/  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- Node /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- Node /2/3/  
  
UPDATE HumanResources.EmployeeDemo  
SET OrgNode = @SubjectEmployee. GetReparentedValue(@OldParent, @NewParent)   
WHERE OrgNode = @SubjectEmployee ;  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
*  
FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\gail0' ; -- Now node /2/3/2/  
```  
  
### <a name="c-clr-example"></a>C. CLR の例  
次のコード スニペットの呼び出し、 GetReparentedValue () メソッド。
  
```sql
this. GetReparentedValue(oldParent, newParent)  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
