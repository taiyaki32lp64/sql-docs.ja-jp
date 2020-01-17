---
title: ENABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 369dd7ec16ee530d7612222ad7e77dd6faf66e14
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73980947"
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

DML トリガー、DDL トリガー、またはログオン トリガーを有効化します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>引数  
*schema_name*  
トリガーが属するスキーマの名前を指定します。 *schema_name* は DDL トリガーやログオン トリガーでは指定できません。  
  
*trigger_name*  
有効化するトリガーの名前です。  
  
ALL  
ON 句のスコープで定義されたすべてのトリガーを有効化することを示します。  
  
*object_name*  
DML トリガー *trigger_name* が実行用に作成されたテーブルまたはビューの名前を指定します。  
  
DATABASE  
DDL トリガーの場合、*trigger_name* が、データベース スコープで実行するために作成または変更されたことを示します。  
  
ALL SERVER  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
DDL トリガーの場合、*trigger_name* が、サーバー スコープで実行するために作成または変更されたことを示します。 ALL SERVER はログオン トリガーにも適用されます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
## <a name="remarks"></a>Remarks  
トリガーを有効化しても、トリガーが再作成されるわけではありません。 無効化されたトリガーは、引き続き現在のデータベースのオブジェクトとして残りますが、起動されることはありません。 トリガーを有効にするには、もともとプログラミングされた [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのいずれかが実行されたときに起動するようにします。 トリガーを無効化するには、[DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) を使います。 テーブルに定義された DML トリガーも、[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) を使用して無効または有効にできます。  
  
## <a name="permissions"></a>アクセス許可  
DML トリガーを有効化するには、少なくとも、そのトリガーが作成されたテーブルまたはビューに対する ALTER 権限が必要です。  
  
サーバー スコープ (ON ALL SERVER) 付きの DDL トリガーまたはログオン トリガーを有効化するには、サーバーに対する CONTROL SERVER 権限が必要です。 DDL トリガーをデータベース スコープ (ON DATABASE) で有効化するには、少なくとも、現在のデータベースに対する ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. テーブル上の DML トリガーを有効化する  
次の例では、AdventureWorks データベースのテーブル `Address` 上に作成されたトリガー `uAddress` を無効化し、次に有効化します。  
  
```sql  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. DDL トリガーを有効化する  
次の例では、データベース スコープの DDL トリガー `safety` を作成し、無効にします。  
  
```sql  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 同じスコープで定義されたすべてのトリガーを有効化する  
次の例では、サーバー スコープで作成されたすべての DDL トリガーを有効化します。  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
```sql  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
