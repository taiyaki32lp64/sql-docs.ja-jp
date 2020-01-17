---
title: SET FORCEPLAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 84060374e3d46dde985e32a549180d8492c72892
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929002"
---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FORCEPLAN を ON に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーは、クエリの FROM 句のテーブルと同じ順序で結合を処理します。 また、FORCEPLAN を ON に設定すると、クエリのプランの構築に他の種類の結合が必要とされる場合や、結合ヒントまたはクエリ ヒントで他の種類の結合が要求された場合を除き、入れ子になったループ結合が強制的に使用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET FORCEPLAN は基本的に、クエリ オプティマイザーが [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントの処理で使用するロジックをオーバーライドします。 SELECT ステートメントから返されるデータは、この設定とは関係なく同じです。 唯一の違いは、クエリの要求を満たすために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がテーブルをどのように処理するかという点です。  
  
 クエリ内でクエリ オプティマイザー ヒントを使用することによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SELECT ステートメントの処理方法を変更することもできます。  
  
 SET FORCEPLAN は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 SET FORCEPLAN の実行権限は、既定ですべてのユーザーに与えられます。  
  
## <a name="examples"></a>使用例  
 次の例では、4 つのテーブルの結合を実行します。 `SHOWPLAN_TEXT` が ON に設定されているので、`SET FORCE_PLAN` が ON に設定された後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、クエリの処理方法がどのように変更されたかに関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
