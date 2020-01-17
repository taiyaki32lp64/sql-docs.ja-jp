---
title: sp_control_plan_guide を (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 808d6e9482d293e957a0dc483df128d08b74133c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108762"
---
# <a name="spcontrolplanguide-transact-sql"></a>sp_control_plan_guide を (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  削除を有効にすると、またはプラン ガイドを無効にします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>引数  
 **N'** _plan_guide_name_ **'**  
 削除するか、有効または無効にするプラン ガイドを指定します。 *plan_guide_name*は、現在のデータベースに解決されます。 指定しない場合、 *plan_guide_name*既定値は NULL です。  
  
 DROP  
 指定されたプラン ガイドを削除*plan_guide_name*します。 プラン ガイドを削除した後、プラン ガイドによって一致していたクエリを将来実行プラン ガイドは影響されません。  
  
 DROP ALL  
 現在のデータベースのすべてのプラン ガイドを削除します。 **N'** _plan_guide_name_ DROP ALL が指定されると指定することはできません。  
  
 DISABLE  
 指定したプラン ガイドを無効にします。 *plan_guide_name*します。 プラン ガイドが無効になった後は、そのプラン ガイドに以前一致していたクエリを実行しても、そのプラン ガイドによる影響は受けません。  
  
 DISABLE ALL  
 現在のデータベース内のすべてのプラン ガイドを無効にします。 **N'** _plan_guide_name_ DISABLE ALL が指定されると指定することはできません。  
  
 有効にします。  
 指定したプラン ガイドを有効*plan_guide_name*します。 プラン ガイドが有効になった後は、そのプラン ガイドを適切なクエリと照合できます。 既定では、プラン ガイドは、作成時に有効にします。  
  
 ENABLE ALL  
 現在のデータベース内のすべてのプラン ガイドを有効にします。 **N'** _plan_guide_name_ **'** ENABLE ALL を指定すると指定することはできません。  
  
## <a name="remarks"></a>コメント  
 有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。  
  
 無効なプラン ガイドを無効にする場合や、有効なプラン ガイドを有効にする場合は影響は生じず、エラーなしで実行できます。  
  
 プラン ガイドはすべてのエディションで使用できない[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[Editions and Supported Features for SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」 (SQL Server 2016 のエディションとサポートされる機能) を参照してください。 ただし、実行できます。 **sp_control_plan_guide**の任意のエディションで DROP または DROP ALL オプションを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="permissions"></a>アクセス許可  
 実行する**sp_control_plan_guide** OBJECT 型のプラン ガイドで (指定して作成 **@type ='** オブジェクト **'** ) オブジェクトに対する ALTER 権限が必要ですプラン ガイドによって参照されます。 その他すべてのプラン ガイドでは、ALTER DATABASE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>A. プラン ガイドを無効にし、有効にした後、削除する  
 次の例ではプラン ガイドを作成し、それを無効にし、有効にした後、削除します。  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>B. 現在のデータベース内のすべてのプラン ガイドを無効にします。  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのすべてのプラン ガイドを無効にします。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [プラン ガイド](../../relational-databases/performance/plan-guides.md)  
  
  
