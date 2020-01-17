---
title: IsDescendantOf (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f38ee0e89201a1ecc0a8faa145167ad58601c133
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077820"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

場合は true を返します。 *この* 親の子孫であります。
  
## <a name="syntax"></a>構文  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>引数  
*parent*  
IsDescendantOf テストを実行する必要がある **hierarchyid** ノード。
  
## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: ビット**
  
**CLR の戻り値の型:SqlBoolean**
  
## <a name="remarks"></a>Remarks  
親をルートとするサブツリー内のすべてのノードには true、それ以外のノードには false を返します。
  
親はそれ自身の子孫と見なされます。
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. WHERE 句で IsDescendantOf を使用する  
次の例では、マネージャーと、そのマネージャーに直属の従業員を返します。
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. IsDescendantOf を使用してリレーションシップを評価する  
次のコードでは、3 つの変数を宣言して値を設定します。 その後に階層リレーションシップを評価し、比較を基に 2 つの出力結果のいずれかを返します。
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. 共通言語ランタイム メソッドを呼び出す  
次のコード例では `IsDescendantOf()` メソッドを呼び出します。
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
