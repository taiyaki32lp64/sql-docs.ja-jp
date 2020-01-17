---
title: DML トリガーに関する情報の取得 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- metadata [SQL Server], triggers
- viewing DML triggers
- DML triggers, metadata
- displaying DML triggers
- status information [SQL Server], triggers
- DML triggers, viewing
ms.assetid: 37574aac-181d-4aca-a2cc-8abff64237dc
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64ad4f4ac71b88966f3ff9a963332619d7663917
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909286"
---
# <a name="get-information-about-dml-triggers"></a>DML トリガーに関する情報の取得
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して DML トリガーに関する情報を取得する方法について説明します。 この情報には、テーブルに設定されたトリガーの種類、名前、所有者、および作成日または変更日を確認できます。 トリガーが作成時に暗号化されていない場合は、トリガーの定義を取得します。 定義は、トリガーを定義しているテーブルに対してそのトリガーがどのように作用するかを理解するのに役立ちます。 また、特定のトリガーが使用しているオブジェクトを見つけることもできます。 この情報を使用すると、データベースで変更または削除された場合にトリガーに影響を及ぼすオブジェクトを確認できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **DML トリガーに関する情報を取得するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sys.sql.modules**、 **sys.object**、 **sys.triggers**、 **sys.events**、 **sys.trigger_events**  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
 OBJECT_DEFINITION、OBJECTPROPERTY、 **sp_helptext**  
 ロール **public** のメンバーシップが必要です。 ユーザー オブジェクトの定義は、オブジェクトの所有者、または次のいずれかの権限を許可された人が表示できます。ALTER、CONTROL、TAKE OWNERSHIP、VIEW DEFINITION。 これらの権限は **db_owner**、 **db_ddladmin**、および **db_securityadmin** 固定データベース ロールのメンバーが暗黙的に保有します。  
  
 **sys.sql_expression_dependencies**  
 データベースに対する VIEW DEFINITION 権限およびデータベースの **sys.sql_expression_dependencies** に対する SELECT 権限が必要です。 既定では、SELECT 権限は **db_owner** 固定データベース ロールのメンバーだけに与えられます。 SELECT 権限と VIEW DEFINITION 権限が別のユーザーに与えられている場合、権限が許可されているユーザーはデータベース内のすべての依存関係を表示できます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>DML トリガーの定義を表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  目的のデータベースを展開し、 **[テーブル]** を展開します。次に、定義を表示するトリガーが格納されているテーブルを展開します。  
  
3.  **[トリガー]** を展開します。目的のトリガーを右クリックし、 **[変更]** をクリックします。 DML トリガーの定義がクエリ ウィンドウに表示されます。  

#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>DML トリガーの依存関係を表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  目的のデータベースを展開し、 **[テーブル]** を展開します。次に、表示するトリガーとその依存関係が格納されているテーブルを展開します。  
  
3.  **[トリガー]** を展開します。目的のトリガーを右クリックし、 **[依存関係の表示]** をクリックします。  
  
4.  **[オブジェクトの依存関係]** ウィンドウで DML トリガーに依存するオブジェクトを表示するには、 **[\<DML トリガー名 に依存するオブジェクト]** を選択します。 オブジェクトが **[依存関係]** 領域に表示されます。  
  
     DML が依存するオブジェクトを表示するには、 **[\<DML トリガー名 が依存するオブジェクト]** を選択します。 オブジェクトが **[依存関係]** 領域に表示されます。 すべてのオブジェクトを表示するには、各ノードを展開します。  
  
5.  **[依存関係]** 領域に表示されたオブジェクトに関する情報を取得するには、そのオブジェクトをクリックします。 **[選択したオブジェクト]** フィールドの **[名前]** 、 **[種類]** 、および **[依存関係の種類]** の各ボックスに情報が表示されます。  
  
6.  **[オブジェクトの依存関係]** ウィンドウを閉じるには、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>DML トリガーの定義を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次のいずれかの例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 それぞれの例は、 `iuPerson` トリガーの定義を表示する方法を示します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT definition   
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID(N'Person.iuPerson');   
GO  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.iuPerson')) AS ObjectDefinition;   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
EXEC sp_helptext 'Person.iuPerson'  
GO  
  
```  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>DML トリガーの依存関係を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次のいずれかの例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 それぞれの例は、 `iuPerson` トリガーの依存関係を表示する方法を示します。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,   
    referenced_server_name, referenced_database_name, referenced_schema_name,   
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,   
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Person.iuPerson');   
GO  
  
```  
  
#### <a name="to-view-information-about-dml-triggers-in-the-database"></a>データベース内の DML トリガーに関する情報を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次のいずれかの例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 それぞれの例は、データベース内の DML トリガー (`TR`) に関する情報を表示する方法を示します。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT  name, parent_id, create_date, modify_date, is_instead_of_trigger  
FROM sys.triggers  
WHERE type = 'TR';   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT  name, object_id, schema_id, parent_object_id, type_desc, create_date, modify_date, is_published  
FROM sys.objects  
WHERE type = 'TR';   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'Person.iuPerson'), 'ExecIsInsteadOfTrigger');   
GO  
  
```  
  
#### <a name="to-view-information-about-events-that-fire-a-dml-trigger"></a>DML トリガーを起動するイベントに関する情報を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次のいずれかの例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 それぞれの例は、 `iuPerson` トリガーを起動するイベントを表示する方法を示します。  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT object_id, type, type_desc, is_trigger_event, event_group_type, event_group_type_desc   
FROM sys.events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
```sql  
USE AdventureWorks2012;   
GO   
SELECT object_id, type,is_first, is_last  
FROM sys.trigger_events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
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
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
  
