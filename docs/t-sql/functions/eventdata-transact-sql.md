---
title: EVENTDATA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status information
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 73e0c8737a65b040552029717bf6848e1fc0cb63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094575"
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、サーバーまたはデータベースのイベントに関する情報を返します。 イベント通知が発生し、指定されたサービス ブローカーが結果を受け取ると、`EVENTDATA` が呼び出されます。 DDL またはログオン トリガーも、`EVENTDATA` の内部使用をサポートしています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Remarks  
`EVENTDATA` は、DDL トリガーまたはログオン トリガーの内部で直接参照された場合のみ、データを返します。 他のルーチンから呼び出された場合は、たとえ DDL トリガーまたはログオン トリガーがそのルーチンを呼びだした場合であっても、`EVENTDATA` は null を返します。
  
`EVENTDATA` によって返されるデータは、以下のトランザクションの後で無効になります。

+ `EVENTDATA` を明示的に呼び出した
+ `EVENTDATA` を暗黙的に呼び出した
+ コミットした
+ ロールバックされた  
  
> [!CAUTION]  
>  `EVENTDATA` が返す XML データは、1 文字に 2 バイトを使用する Unicode としてクライアントに送信されます。 `EVENTDATA` は、次の Unicode コード ポイントを表す XML を返します。  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  XML は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の識別子およびデータで使用できる一部の文字を表現できず、したがって許可しません。 上記の一覧に含まれていないコード ポイントを含んでいる文字やデータは、疑問符 (?) にマップされます。  
  
`CREATE LOGIN` または `ALTER LOGIN` ステートメントを実行したとき、パスワードは表示されません。 こにより、ログイン セキュリティが保護されます。  
  
## <a name="schemas-returned"></a>返されるスキーマ  
EVENTDATA は、**xml** データ型の値を返します。 既定では、すべてのイベントのスキーマ定義は、次のディレクトリにインストールされます:[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd。  
  
「[Microsoft SQL Server XML Schemas](https://go.microsoft.com/fwlink/?LinkID=31850)」(Microsoft SQL Server の XML スキーマ) Web ページにもイベント スキーマがあります。  
  
特定のイベントのスキーマを抽出するには、複合型 `EVENT_INSTANCE_<event_type>` のスキーマを検索します。 たとえば、`DROP_TABLE` イベントのスキーマを抽出するには、`EVENT_INSTANCE_DROP_TABLE` のスキーマを検索します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. DDL トリガーでイベント データをクエリする  
この例では、新しいデータベース テーブルが作成されないようにする DDL トリガーを作成します。 `EVENTDATA` によって生成された XML データに対して XQuery を使用して、トリガーを発生させる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをキャプチャします。 詳しくは、「[XQuery 言語リファレンス &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)」をご覧ください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で **[結果をグリッドに表示]** を使用して `<TSQLCommand>` 要素をクエリすると、コマンド テキストに改行が表示されません。 代わりに、 **[結果をテキストで表示]** を使用してください。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  イベント データを返す場合は、**query()** メソッドの代わりに XQuery の **value()** を使います。 **query()** メソッドでは、XML およびアンパサンドでエスケープされる復帰と改行 (CR/LF) インスタンスが出力に返されます。一方 **value()** メソッドでは、CR/LF インスタンスが出力に返されますが、表示はされません。  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. DDL トリガーでイベント データを含んだログ テーブルを作成する  
この例では、データベース レベルのすべてのイベントに関する情報ストレージのテーブルを作成し、DDL トリガーでそのテーブルにデータを設定します。 `EVENTDATA` によって生成された XML データに対して XQuery を使用して、イベントの種類と [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをキャプチャします。  
  
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
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [EVENTDATA 関数の使用](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)   
 [イベント通知](../../relational-databases/service-broker/event-notifications.md)   
 [ログオン トリガー](../../relational-databases/triggers/logon-triggers.md)  
  
  
