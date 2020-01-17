---
title: DISABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d658b63e8c2b80c277ed9d8c3647717d07c96c48
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982977"
---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  トリガーを無効にします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *schema_name*  
 トリガーが属するスキーマの名前を指定します。 DDL トリガーまたはログオン トリガーでは *schema_name* を指定できません。  
  
 *trigger_name*  
 無効にするトリガーの名前です。  
  
 ALL  
 ON 句の有効範囲で定義されたすべてのトリガーを無効にすることを示します。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、マージ レプリケーション用にパブリッシュされたデータベースにトリガーが作成されます。 パブリッシュされたデータベースで ALL を指定すると、これらのトリガーが無効になり、レプリケーションが中断されます。 現在のデータベースがマージ レプリケーション用にパブリッシュされていないことを確認してから、ALL を指定してください。  
  
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
 既定では、トリガーは作成されたときに有効になります。 トリガーを無効にしてもトリガーは削除されず、 オブジェクトとして現在のデータベースに残りますが、 トリガーがプログラムされた [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行しても、トリガーは起動しません。 トリガーは、[ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md) を使用することにより再度有効にできます。 テーブルに定義された DML トリガーも、[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) を使用して無効または有効にできます。  
  
 **ALTER TRIGGER** ステートメントを使用してトリガーを変更すると、トリガーが有効になります。  
  
## <a name="permissions"></a>アクセス許可  
 DML トリガーを無効にするには、少なくともトリガーが作成されたテーブルまたはビューに対する ALTER 権限が必要です。  
  
 サーバー スコープ (ON ALL SERVER) 付きの DDL トリガーまたはログオン トリガーを無効にするには、サーバーでの CONTROL SERVER 権限が必要です。 データベース スコープ (ON DATABASE) の DDL トリガーを無効にするために、ユーザーには少なくとも、現在のデータベースに対する ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
## <a name="examples"></a>使用例  
次の例は、AdventureWorks2012 データベースで記述されています。
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>A. テーブルの DML トリガーを無効にする  
 次の例では、テーブル `Address` に作成されたトリガー `uAddress` を無効にします。  
  
```sql  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>B. DDL トリガーを無効にする  
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
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 同じスコープに定義されたすべてのトリガーを無効にする  
 次の例では、サーバー スコープで作成された DDL トリガーをすべて無効にします。  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
