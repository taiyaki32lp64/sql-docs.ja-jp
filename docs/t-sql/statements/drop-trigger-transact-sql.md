---
title: DROP TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP TRIGGER
- DROP_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- renaming triggers
- triggers [SQL Server], removing
- DDL triggers, removing
- DROP TRIGGER statement
- deleting triggers
- dropping triggers
- removing triggers
- DML triggers, removing
ms.assetid: 092d0d71-9f1e-4e38-a1c4-2487adfa5b4e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 810367b817aec0688a2bc5168be10c7ff073affc
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73980993"
---
# <a name="drop-trigger-transact-sql"></a>DROP TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  1 つ以上の DML トリガーまたは DDL トリガーを現在のデータベースから削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
DROP TRIGGER [ IF EXISTS ] [schema_name.]trigger_name [ ,...n ] [ ; ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE or UPDATE statement (DDL Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON { DATABASE | ALL SERVER }   
[ ; ]  
  
-- Trigger on a LOGON event (Logon Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON ALL SERVER  
```  

  
## <a name="arguments"></a>引数  
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで、[!INCLUDE[sssds](../../includes/sssds-md.md)])。  
  
 条件付きでは既に存在する場合にのみ、トリガーを削除します。  
  
 *schema_name*  
 DML トリガーが属しているスキーマの名前を指定します。 DML トリガーのスコープは、そのトリガーが作成されたテーブルまたはビューのスキーマです。 DDL トリガーまたはログオン トリガーでは *schema_name* を指定できません。  
  
 *trigger_name*  
 削除するトリガーの名前を指定します。 現在作成されているトリガーの一覧を表示するには、[sys.server_assembly_modules](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) または [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) を使います。  
  
 DATABASE  
 DDL トリガーのスコープが現在のデータベースに適用されることを示します。 トリガーを作成または変更したときに DATABASE を指定した場合は、同じく DATABASE を指定する必要があります。  
  
 ALL SERVER  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 DDL トリガーのスコープが現在のサーバーに適用されることを示します。 トリガーを作成または変更したときに ALL SERVER を指定した場合は、同じく ALL SERVER を指定する必要があります。 ALL SERVER はログオン トリガーにも適用されます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
## <a name="remarks"></a>Remarks  
 DML トリガーを削除するには、DML トリガー自体またはトリガー テーブルを削除します。 テーブルを削除した場合、関係付けられているすべてのトリガーも削除されます。  
  
 トリガーが削除されると、トリガーに関する情報が **sys.objects**、**sys.triggers**、および **sys.sql_modules** カタログ ビューから削除されます。  
  
 すべてのトリガーが同一の ON 句で作成されている場合のみ、DROP TRIGGER ステートメントごとに複数の DDL トリガーを削除できます。  
  
 トリガーの名前を変更するには、DROP TRIGGER と CREATE TRIGGER を使用します。 トリガーの定義を変更するには、ALTER TRIGGER を使用します。  
  
 特定のトリガーの依存関係を確認する方法について詳しくは、「[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)」、「[sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)」、および「[sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)」をご覧ください。  
  
 トリガーのテキストの表示について詳しくは、「[sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)」および「[sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)」をご覧ください。  
  
 既存トリガーのリストの表示について詳しくは、「[sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)」および「[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 DML トリガーを削除するには、トリガーが定義されているテーブルやビューに対する ALTER 権限が必要です。  
  
 サーバー スコープ (ON ALL SERVER) で定義されている DDL トリガー、またはログオン トリガーを削除するには、サーバーでの CONTROL SERVER 権限が必要です。 データベース スコープ (ON DATABASE) で定義されている DDL トリガーを削除するには、現在のデータベースでの ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-dropping-a-dml-trigger"></a>A. DML トリガーを削除する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースにある `employee_insupd` トリガーを削除します ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、DROP TRIGGER IF EXISTS 構文を使うことができます)。  
  
```  
IF OBJECT_ID ('employee_insupd', 'TR') IS NOT NULL  
   DROP TRIGGER employee_insupd;  
```  
  
### <a name="b-dropping-a-ddl-trigger"></a>B. DDL トリガーを削除する  
 次の例では、DDL トリガー `safety` を削除します。  
  
> [!IMPORTANT]  
>  DDL トリガーはスキーマ スコープではないため、**sys.objects** カタログ ビューには表示されません。そのため、それらのトリガーがデータベース内に存在するかどうかを、OBJECT_ID 関数を使用してクエリすることはできません。 スキーマ スコープでないオブジェクトをクエリするには、適切なカタログ ビューを使用する必要があります。 DDL トリガーの場合は、**sys.triggers** を使ってください。  
  
```  
DROP TRIGGER safety  
ON DATABASE;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [DML トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
