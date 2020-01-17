---
title: DML トリガーの変更または名前の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 824ea1587955884f10a53579865d2029cc63eefc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473223"
---
# <a name="modify-or-rename-dml-triggers"></a>DML トリガーの変更または名前の変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]の DML トリガーを変更したりその名前を変更したりする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **DML トリガーに変更を加えたり名前を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   トリガーの名前を変更する場合、トリガーは現在のデータベース内にある必要があり、新しい名前は [識別子](../databases/database-identifiers.md)に関するルールに従っている必要があります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   [sp_rename](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql) ストアド プロシージャを使用してトリガーの名前を変更しないことをお勧めします。 オブジェクト名の一部または全部を変更すると、スクリプトおよびストアド プロシージャが壊れる可能性があります。 トリガーの名前を変更しても、 [sys.sql_modules](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) カタログ ビューの definition 列にある、対応するオブジェクトの名前は変更されません。 トリガーを削除してから再作成することをお勧めします。  
  
-   DML トリガーで参照されるオブジェクトの名前を変更する際には、新しい名前を反映するようにトリガーを変更する必要があります。 したがって、オブジェクトの名前を変更する前に、まずオブジェクトの依存関係を表示して、オブジェクト名の変更により影響を受けるトリガーがあるかどうかを確認してください。  
  
-   DML トリガーは、定義が暗号化されるように変更することもできます。  
  
-   トリガーの依存関係を表示するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または次の関数およびカタログ ビューを使用できます。  
  
    -   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
    -   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
    -   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 DML トリガーを変更するには、トリガーが定義されているテーブルやビューに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-a-dml-trigger"></a>DML トリガーを変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  目的のデータベースを展開し、 **[テーブル]** を展開します。次に、変更するトリガーが格納されているテーブルを展開します。  
  
3.  **[トリガー]** を展開します。変更するトリガーを右クリックし、 **[変更]** をクリックします。  
  
4.  トリガーを変更し、 **[実行]** をクリックします。  
  
#### <a name="to-rename-a-dml-trigger"></a>DML トリガーの名前を変更するには  
  
1.  名前を変更する[トリガーを削除](../triggers/dml-triggers.md) します。  
  
2.  新しい名前を指定して、[トリガーを再作成](../triggers/create-dml-triggers.md)します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>ALTER TRIGGER を使用してトリガーを変更するには  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーし、クエリに貼り付けます。 1 つ目の例を実行して、ユーザーが `SalesPersonQuotaHistory` テーブルのデータの追加や変更を行おうとしたときにユーザー定義のメッセージを出力する DML トリガーを作成します。 [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) ステートメントを実行して、 `INSERT` アクティビティのときだけトリガーが発生するように変更します。 このトリガーは、テーブルの更新や行の挿入を行うユーザーに対して、 `Compensation` 部門にも変更を知らせる必要があることを連絡できるので有用です。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>DROP TRIGGER と ALTER TRIGGER を使用してトリガーの名前を変更するには  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) ステートメントと [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) ステートメントを使用して、 `Sales.bonus_reminder` トリガーの名前を `Sales.bonus_reminder_2`に変更します。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [DML トリガーに関する情報の取得](../triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
