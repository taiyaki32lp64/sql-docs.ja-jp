---
title: EVENTDATA 関数の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aef51bd94bf7cffb3e9481b409477a3830fabffb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058601"
---
# <a name="use-the-eventdata-function"></a>EVENTDATA 関数の使用
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DDL トリガーを起動するイベントに関する情報は、EVENTDATA 関数を使用してキャプチャされます。 この関数は、 **xml** 値を返します。 XML スキーマには、次の項目に関する情報が含まれています。  
  
-   イベントの時刻。  
  
-   トリガーが実行されたときの接続のシステム プロセス ID (SPID)。  
  
-   トリガーを起動したイベントの種類。  
  
 イベントの種類に応じて、イベントが発生したデータベース、イベントが発生したオブジェクト、イベントの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントなどの追加情報がスキーマに含まれます。 詳細については、「 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)」を参照してください。  
  
 たとえば、次の DDL トリガーが [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースに作成されたとします。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 次に、以下の `CREATE TABLE` ステートメントが実行されます。  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 DDL トリガーの `EVENTDATA()` ステートメントにより、 `CREATE TABLE` ステートメントでは許可されないテキストがキャプチャされます。 これは、EVENTDATA によって生成された **xml** データに対して XQuery ステートメントを使用して、\<CommandText> 要素を取得することによって行われます。 詳細については、「[XQuery 言語リファレンス &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)」を参照してください。  
  
> [!CAUTION]  
>  EVENTDATA は、CREATE_SCHEMA イベントのデータをキャプチャします。対応する CREATE SCHEMA 定義の <schema_element> がある場合にはそれもキャプチャします。 さらに、EVENTDATA は <schema_element> 定義を別のイベントとして認識します。 したがって、CREATE_SCHEMA イベント、および CREATE SCHEMA 定義の <schema_element> によって表されるイベントの両方で作成される DDL トリガーは、`TSQLCommand` データのように同じイベント データを 2 回返す場合があります。 たとえば、CREATE_SCHEMA イベントと CREATE_TABLE イベントの両方で DDL トリガーが作成され、次のバッチを実行するとします。  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  アプリケーションで CREATE_TABLE イベントの `TSQLCommand` データを取得する場合は、このデータが 2 回発生する可能性があることに注意してください。つまり、CREATE_SCHEMA イベントの発生時と、CREATE_TABLE イベントの発生時です。 CREATE_SCHEMA イベントと、対応する CREATE SCHEMA 定義の <schema_element> テキストの両方で DDL トリガーを作成しないようにするか、または同じイベントを 2 回処理しないようにアプリケーションのロジックを作成します。  
  
## <a name="alter-table-and-alter-database-events"></a>ALTER TABLE イベントと ALTER DATABASE イベント  
 ALTER_TABLE および ALTER_DATABASE イベントのイベント データには、DDL ステートメントの影響を受けた他のオブジェクトの名前と種類、およびそれらのオブジェクトで実行されたアクションも含まれます。 ALTER_TABLE イベント データには、ALTER TABLE ステートメントの影響を受けた列、制約、またはトリガーの名前と、それらのオブジェクトで実行されたアクション (作成、変更、削除、有効化、または無効化) が含まれます。 ALTER_DATABASE イベント データには、ALTER DATABASE ステートメントの影響を受けたファイルまたはファイル グループの名前と、それらのオブジェクトで実行されたアクション (作成、変更、または削除) が含まれます。  
  
 たとえば、次の DDL トリガーを AdventureWorks サンプル データベースに作成します。  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 次に、制約に違反する次の ALTER TABLE ステートメントを実行します。  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 DDL トリガーの EVENTDATA() ステートメントにより、 `ALTER TABLE` ステートメントでは許可されないテキストがキャプチャされます。  
  
## <a name="example"></a>例  
 EVENTDATA 関数を使用して、イベントのログを作成できます。 次の例では、イベント情報を格納するためのテーブルが作成されます。 次に、現在のデータベースに DDL トリガーが作成されます。この DDL トリガーにより、データベース レベルの DDL イベントが発生するたびに、次の情報がテーブルに設定されます。  
  
-   イベントの時刻 (GETDATE 関数を使用)。  
  
-   イベントが発生したセッションのデータベース ユーザー (CURRENT_USER 関数を使用)。  
  
-   イベントの種類。  
  
-   イベントが含まれる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。  
  
 最後の 2 つの項目は、EVENTDATA によって生成された **xml** データに対して XQuery を使用することによってキャプチャされます。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  イベント データを返す場合は、 **query()** メソッドの代わりに XQuery の **value()** を使用してください。 **query()** メソッドでは、XML およびアンパサンドでエスケープされる復帰と改行 (CRLF) インスタンスが出力に返されます。一方 **value()** メソッドでは、CRLF インスタンスが出力に返されますが、表示はされません。  
  
 同様の DDL トリガーの例を、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースで提供しています。 この例を入手するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して Database Triggers フォルダーを探します。 このフォルダーは **データベースの** [プログラミング] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] フォルダーにあります。 **ddlDatabaseTriggerLog** を右クリックし、 **[データベース トリガーをスクリプト化]** を選択します。 既定では、DDL トリガー **ddlDatabaseTriggerLog** は無効になっています。  
  
## <a name="see-also"></a>参照  
 [DDL イベント](../../relational-databases/triggers/ddl-events.md)   
 [DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
