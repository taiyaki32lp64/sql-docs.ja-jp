---
title: DROP PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ed342f6b73ee596d8429aa4b952c4becf7d41ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044030"
---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  1 つ以上のストアド プロシージャまたはプロシージャ グループを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の現在のデータベースから削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>引数  
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きでは既に存在する場合にのみ、プロシージャを削除します。  
  
 *schema_name*  
 プロシージャが属するスキーマの名前を指定します。 サーバー名またはデータベース名は指定できません。  
  
 *procedure*  
 削除するストアド プロシージャまたはストアド プロシージャ グループの名前です。 番号の付いたプロシージャ グループ内の個々のプロシージャは削除できません。プロシージャ グループ全体が削除されます。  
  
## <a name="best-practices"></a>ベスト プラクティス  
 ストアド プロシージャを削除する前に、依存オブジェクトを確認し、それらのオブジェクトを適切に修正します。 ストアド プロシージャを削除すると、これらのオブジェクトが更新されていない場合、依存オブジェクトとスクリプトがエラーになることがあります。 詳細については、「[ストアド プロシージャの依存関係の表示](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)」を参照してください  
  
## <a name="metadata"></a>メタデータ  
 既存のプロシージャの一覧を表示するには、**sys.objects** カタログ ビューに対してクエリを実行します。 プロシージャの定義を表示するには、**sys.sql_modules** カタログ ビューに対してクエリを実行します。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 プロシージャの **CONTROL** 権限か、プロシージャが属しているスキーマに対する **ALTER** 権限、または **db_ddladmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のデータベースから `dbo.uspMyProc` ストアド プロシージャを削除します。  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 次の例では、現在のデータベースからいくつかのストアド プロシージャを削除します。  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 次の例では、削除、 `dbo.uspMyProc` ストアド プロシージャが存在するが、プロシージャが存在しない場合のエラーは発生しません。 この構文はで新しい [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]です。  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>参照  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [ストアド プロシージャの削除](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  


