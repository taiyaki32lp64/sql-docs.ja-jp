---
title: DDL トリガー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b4647814765225a2c1deeedd05f77bed80d7e992
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056151"
---
# <a name="ddl-triggers"></a>DDL トリガー
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DDL トリガーは、さまざまなデータ定義言語 (DDL) イベントに対応して起動されます。 これらのイベントは主に、CREATE、ALTER、DROP、GRANT、DENY、REVOKE、UPDATE STATISTICS のいずれかのキーワードで始まる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに対応します。 DDL と同様の操作を実行する特定のシステム ストアド プロシージャも DDL トリガーを起動できます。  
  
 DDL トリガーは、次のような場合に使用します。  
  
-   データベース スキーマへの特定の変更を回避する。  
  
-   データベース スキーマの変更に対して、データベース内でなんらかの処理を実行する。  
  
-   データベース スキーマの変更またはイベントを記録する。  
  
> [!IMPORTANT]  
>  DDL トリガーはテストして、実行されているシステム ストアド プロシージャに応答するかどうか、確認してください。 たとえば、CREATE TYPE ステートメントおよび **sp_addtype** ストアド プロシージャはどちらも、CREATE_TYPE イベントで作成される DDL トリガーを起動します。  
  
## <a name="types-of-ddl-triggers"></a>DDL トリガーの種類  
 ### <a name="transact-sql-ddl-trigger"></a>Transact-SQL DDL トリガー  
 サーバー スコープまたはデータベース スコープのイベントに応答して [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント (複数可) を実行する特殊な [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャです。 たとえば、ALTER SERVER CONFIGURATION などのステートメントが実行されたときや、DROP TABLE を使用してテーブルが削除されたときに、DDL トリガーを起動させることができます。  
  
 ### <a name="clr-ddl-trigger"></a>CLR DDL トリガー  
 CLR トリガーは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを実行するのではなく、.NET Framework で作成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアップロードされたアセンブリのメンバーであるマネージド コードに記述されている、1 つ以上のメソッドを実行します。  
  
 DDL トリガーは、起動元の DDL ステートメントが実行されるまで、起動されません。 DDL トリガーを INSTEAD OF トリガーの代わりに使用することはできません。 DDL トリガーは、ローカルまたはグローバルの一時テーブルおよびストアド プロシージャに影響するイベントに応答して起動されることはありません。  
  
 DDL トリガーでは、特殊な **inserted** テーブルや **deleted** テーブルは作成できません。  
  
 DDL トリガーを起動するイベントの情報と、起動したトリガーにより加えられる変更は、EVENTDATA 関数を使用してキャプチャします。  
  
 DDL イベントごとに作成される複数のトリガー。  
  
 DML トリガーと異なり、DDL トリガーのスコープはスキーマに設定されません。 このため、DDL トリガーに関するメタデータのクエリに、OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY、OBJECTPROPERTYEX などの関数を使用することはできません。 代わりに、カタログ ビューを使用してください。  
  
 サーバー スコープの DDL トリガーは、SQL Server Management Studio のオブジェクト エクスプローラーの **[Triggers]** フォルダーに表示されます。 このフォルダーは、 **[Server Objects]** フォルダーにあります。 データベース スコープの DDL トリガーは、 **[データベース トリガー]** フォルダーに表示されます。 このフォルダーは対応するデータベースの **[Programmability]** フォルダーにあります。  
  
> [!IMPORTANT]  
>  上位の特権の下では、トリガー内の悪意のあるコードを実行できます。 この脅威の軽減方法の詳細については、「 [トリガーのセキュリティの管理](../../relational-databases/triggers/manage-trigger-security.md)」を参照してください。  
  
## <a name="ddl-trigger-scope"></a>DDL トリガーのスコープ  
 DDL トリガーは、現在のデータベースまたは現在のサーバーで処理されている [!INCLUDE[tsql](../../includes/tsql-md.md)] イベントに応答して起動されます。 トリガーのスコープは、イベントによって異なります。 たとえば、CREATE_TABLE イベントに応答して起動されるように作成された DDL トリガーは、データベース、またはサーバー インスタンスで CREATE_TABLE イベントが発生するたびに起動されます。 CREATE_LOGIN イベントに応答して起動されるように作成された DDL トリガーは、サーバー インスタンスで CREATE_LOGIN イベントが発生した場合にのみ起動できます。  
  
 次の例では、データベースで `safety` イベントまたは `DROP_TABLE` イベントが発生するたびに、DDL トリガー `ALTER_TABLE` が起動されます。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 次の例では、現在のサーバー インスタンスで `CREATE_DATABASE` イベントが発生した場合に、DDL トリガーによってメッセージが出力されます。 この例では、対応する `EVENTDATA` ステートメントのテキストを取得するために [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を使用します。 DDL トリガーで EVENTDATA を使用する方法の詳細については、「 [EVENTDATA 関数の使用](../../relational-databases/triggers/use-the-eventdata-function.md)」を参照してください。  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに指定できるスコープをそのステートメントに対応付けた一覧については、「DDL トリガーを起動するための、特定の DDL ステートメントの選択」に記載されたリンクを参照してください。  
  
 データベース スコープが設定された DDL トリガーは、DDL トリガーが作成されたデータベースにオブジェクトとして格納されます。 DDL トリガーを **master** データベースに作成することもでき、ユーザーが設計したデータベースで作成されたトリガーと同様に動作します。 **sys.triggers** カタログ ビューにクエリを実行することで、DDL トリガーに関する情報を取得できます。 トリガーが作成されたデータベース コンテキスト内の **sys.triggers** に対してクエリを実行できます。または、識別子 (たとえば、 **master.sys.triggers**) としてデータベース名を指定することもできます。  
  
 サーバー スコープが設定された DDL トリガーは、 **master** データベースにオブジェクトとして格納されます。 ただし、サーバー スコープが設定された DDL トリガーに関する情報は、任意のデータベース コンテキストの **sys.server_triggers** カタログ ビューから取得できます。  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>Transact-SQL ステートメントまたはステートメントのグループの指定  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>DDL トリガーを起動するための、特定の DDL ステートメントの選択  
 DDL トリガーは、1 つ以上の特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが実行された後に起動されるように設計できます。 前の例では、 `safety` イベント、または `DROP_TABLE` イベントの後に `ALTER_TABLE` トリガーが起動されます。 DDL トリガーを起動するために指定できる各 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、および DDL トリガーを起動できるスコープの一覧については、「 [DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>DDL トリガーを起動するための、事前定義済み DDL ステートメントのグループの選択  
 類似したイベントの事前定義済みのグループに所属する [!INCLUDE[tsql](../../includes/tsql-md.md)] イベントを実行した後に、DDL トリガーを起動できます。 たとえば、CREATE TABLE ステートメント、ALTER TABLE ステートメント、または DROP TABLE ステートメントのいずれかの実行後に DDL トリガーを発生させる場合、CREATE TRIGGER ステートメントで FOR DDL_TABLE_EVENTS を指定できます。 CREATE TRIGGER の実行後、イベント グループで対応されるイベントが **sys.trigger_events** カタログ ビューに追加されます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]で、イベント グループに対してトリガーを作成した場合、 **sys.trigger_events** にはイベント グループについての情報が含まれず、 **sys.trigger_events** にはそのグループで対応される個々のイベントについての情報のみが含まれています。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降では、 **sys.trigger_events** が、トリガーが作成されたイベント グループに関するメタデータ、およびイベント グループが対応する個々のイベントに関するメタデータも保持します。 したがって、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のイベント グループで対応されたイベントに変更を加えても、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のイベント グループに対して作成される DDL トリガーには適用されません。  
  
 DDL トリガーで使用できる事前定義済みの DDL ステートメントのグループ、そのグループが対応する特定のステートメント、およびこれらのイベント グループをプログラミングできるスコープの一覧については、「 [DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|トピック|  
|----------|-----------|  
|DDL トリガーを作成、変更、削除、または無効化する方法について説明します。|[DDL トリガーの実装](../../relational-databases/triggers/implement-ddl-triggers.md)|  
|CLR DDL トリガーの作成方法について説明します。|[CLR トリガーの作成](../../relational-databases/triggers/create-clr-triggers.md)|  
|DDL トリガーに関する情報を取得する方法について説明します。|[DDL トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-ddl-triggers.md)|  
|DDL トリガーを起動するイベントの情報を、EVENTDATA 関数を使用して取得する方法について説明します。|[EVENTDATA 関数の使用](../../relational-databases/triggers/use-the-eventdata-function.md)|  
|トリガーのセキュリティを管理する方法について説明します。|[トリガーのセキュリティの管理](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>参照  
 [DML トリガー](../../relational-databases/triggers/dml-triggers.md)   
 [ログオン トリガー](../../relational-databases/triggers/logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
