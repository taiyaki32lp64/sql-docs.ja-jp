---
title: ALTER TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER TRIGGER
- ALTER_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, modifying
- triggers [SQL Server], modifying
- modifying triggers
- ALTER TRIGGER statement
- DML triggers, modifying
ms.assetid: 2a99c7c1-ac2f-4637-aa7c-3d1bf514e500
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e8523831fd181c17bd8fcff1698d85f46c824e2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983316"
---
# <a name="alter-trigger-transact-sql"></a>ALTER TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  以前に CREATE TRIGGER ステートメントで作成された DML トリガー、DDL トリガー、またはログオン トリガーの定義を変更します。 トリガーは、CREATE TRIGGER を使用して作成します。 これらのトリガーは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントから直接作成することも、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) 内に作成したアセンブリのメソッドから作成し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアップロードすることもできます。 ALTER TRIGGER ステートメントで使用されるパラメーターの詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table | view )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
[ NOT FOR REPLICATION ]   
AS { sql_statement [ ; ] [ ...n ] | EXTERNAL NAME <method specifier>   
[ ; ] }   
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table 
-- (DML Trigger on memory-optimized tables)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table  )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [ ...n ] }   
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ <EXECUTE AS Clause> ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, 
-- or UPDATE statement (DDL Trigger)  
  
ALTER TRIGGER trigger_name   
ON { DATABASE | ALL SERVER }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement [ ; ] | EXTERNAL NAME <method specifier>   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on a LOGON event (Logon Trigger)  

ALTER TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  
  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
```  
  
```  
-- Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)   
  
ALTER TRIGGER schema_name. trigger_name   
ON (table | view )   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [...n ] }   
  
<dml_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]   
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE statement (DDL Trigger)   
  
ALTER TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]  
```  
  
## <a name="arguments"></a>引数  
 *schema_name*  
 DML トリガーが属しているスキーマの名前を指定します。 DML トリガーのスコープは、そのトリガーが作成されたテーブルまたはビューのスキーマです。 *schema**_name* は、DML トリガーと、トリガーに対応するテーブルまたはビューが既定のスキーマに属している場合にのみ、省略可能です。 DDL トリガーまたはログオン トリガーでは *schema_name* を指定できません。  
  
 *trigger_name*  
 変更する既存のトリガーです。  
  
 *table* | *view*  
 DML トリガーが実行されるテーブルまたはビューです。 テーブルまたはビューの完全修飾名の指定は省略可能です。  
  
 DATABASE  
 DDL トリガーのスコープを現在のデータベースに適用します。 これを指定すると、現在のデータベースで *event_type* または *event_group* が発生するたびにトリガーが起動します。  
  
 ALL SERVER  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 DDL トリガーまたはログオン トリガーのスコープを現在のサーバーに適用します。 これを指定すると、現在のサーバーの任意の場所で *event_type* または *event_group* が発生するたびにトリガーが起動します。  
  
 WITH ENCRYPTION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 ALTER TRIGGER ステートメントのテキストを含む sys.syscommentssys.sql_modules エントリを暗号化します。 WITH ENCRYPTION を使用すると、そのトリガーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションの一部としてパブリッシュできなくなります。 WITH ENCRYPTION は、CLR トリガーに対しては指定できません。  
  
> [!NOTE]  
>  トリガーが WITH ENCRYPTION を使用して作成されている場合、それを有効なままにするには、ALTER TRIGGER ステートメントで WITH ENCRYPTION を再度指定する必要があります。  
  
 EXECUTE AS  
 トリガーを実行するセキュリティ コンテキストを指定します。 このオプションを使用することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが使用するユーザー アカウントを制御することができます。このアカウントは、トリガーが参照するデータベース オブジェクトに対する権限を検証するために使用されます。  
  
 詳細については、「[EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。  
  
 NATIVE_COMPILATION  
 トリガーをネイティブでコンパイルすることを示します。  
  
 このオプションは、メモリ最適化テーブルのトリガーに必要です。  
  
 SCHEMABINDING  
 トリガーによって参照されているテーブルを削除または変更できないことを確認します。  
  
 このオプションは、メモリ最適化テーブルでのトリガーに必要であり、従来のテーブルでのトリガーにはサポートされません。  
  
 AFTER  
 トリガーをアクティブにする SQL ステートメントが正常に実行された後にのみ、そのトリガーを起動することを指定します。 このトリガーが起動される前に、すべての連鎖参照操作および制約チェックも正常に終了している必要があります。  
  
 FOR キーワードのみが指定されている場合は、AFTER が既定値です。  
  
 DML AFTER トリガーは、テーブルでのみ定義できます。  
  
 INSTEAD OF  
 SQL ステートメントを起動する代わりに DML トリガーの実行を指定します。したがって、ステートメントのトリガーの操作はオーバーライドされます。 DDL トリガーまたはログオン トリガーでは INSTEAD OF を指定できません。  
  
 テーブルまたはビューでは、INSERT、UPDATE、または DELETE の各ステートメントに定義できる INSTEAD OF トリガーは 1 つだけですが、 個々のビューに独自の INSTEAD OF トリガーがある複数のビューに対してビューを定義することはできます。  
  
 INSTEAD OF トリガーは、WITH CHECK OPTION を使用して作成したビューでは使用できません。 WITH CHECK OPTION が指定されているビューに対して INSTEAD OF トリガーを追加すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でエラーが発生します。 ユーザーは、INSTEAD OF トリガーを定義する前に、ALTER VIEW を使用して WITH CHECK OPTION を削除する必要があります。  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] } | { [INSERT ] [ , ] [ UPDATE ] }  
 このテーブルまたはビューに対して実行したときに DML トリガーをアクティブにするデータ変更ステートメントを指定します。 少なくとも 1 つのオプションを指定する必要があります。 トリガー定義では、このキーワードを指定する順序や組み合わせを問いません。 複数のオプションを指定するときは、オプションをコンマで区切ります。  
  
 INSTEAD OF トリガーの場合、目的のテーブルに連鎖的な ON DELETE 参照操作を指定している参照関係があるときは、DELETE オプションを指定できません。 同様に、目的のテーブルに ON UPDATE 連鎖参照操作を指定している参照関係があるときは、UPDATE オプションを指定できません。 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
 *event_type*  
 実行後に DDL トリガーが起動される [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの名前です。 DDL トリガーで使用できるイベントの一覧については、「[DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの定義済みグループの名前を指定します。 DDL トリガーは、*event_group* に属する [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの実行後に起動します。 DDL トリガーで使用できるイベント グループの一覧については、「[DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)」を参照してください。 対応するイベントの種類を sys.trigger_events カタログ ビューに追加すると、*event_group* は、ALTER TRIGGER の実行が終了した後、マクロとしても機能します。  
  
 NOT FOR REPLICATION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 トリガーに関係するテーブルをレプリケーション エージェントが変更するときに、トリガーを実行してはいけないことを示します。  
  
 *sql_statement*  
 トリガー条件とトリガー動作です。  
  
 メモリ最適化テーブルのトリガーの場合、最上位レベルで許可される唯一の *sql_statement* は ATOMIC ブロックです。 ATOMIC ブロック内で使用できる T-SQL は、ネイティブ プロシージャ内で使用できる T-SQL によって制限されます。  
  
 EXTERNAL NAME \<method_specifier>  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 トリガーにバインドするアセンブリのメソッドを指定します。 このメソッドは引数を受け取らず、void を返す必要があります。 *class_name* は有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子であり、アセンブリ内にアセンブリで可視のクラスとして存在している必要があります。 入れ子にされたクラスは使用できません。  
  
## <a name="remarks"></a>Remarks  
 ALTER TRIGGER の詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」の「解説」を参照してください。  
  
> [!NOTE]  
>  EXTERNAL_NAME オプションおよび ON_ALL_SERVER オプションは、包含データベースでは使用できません。  
  
## <a name="dml-triggers"></a>DML トリガー  
 ALTER TRIGGER では、テーブルおよびビューに対する INSTEAD OF トリガーを利用することで、更新可能なビューを手動で使用できるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ALTER TRIGGER を、他のすべての種類のトリガー (AFTER、INSTEAD-OF) と同様に適用します。  
  
 テーブルで実行される最初と最後の AFTER トリガーを、sp_settriggerorder を使用して指定できます。 1 つのテーブルにつき、最初と最後の AFTER トリガーはそれぞれ 1 つだけ指定できます。 同じテーブルに他の AFTER トリガーが指定されている場合、トリガーはランダムに実行されます。  
  
 ALTER TRIGGER ステートメントを使って最初と最後のトリガーを変更し、変更したトリガーに設定されていた最初と最後を示す属性を削除した場合は、sp_settriggerorder を使用して順序の値を再設定する必要があります。  
  
 AFTER トリガーは、トリガーを起動する SQL ステートメントが正常に実行された後にのみ実行されます。 このステートメントの実行には、更新または削除されるオブジェクトに関連付けられている連鎖的なすべての参照操作と制約チェックの実行も含まれます。 AFTER トリガー操作は、トリガーをアクティブにするステートメントの結果、およびそのステートメントによって発生するすべての UPDATE および DELETE 連鎖参照操作の結果を調べます。  
  
 子テーブルまたは参照元テーブルへの DELETE 操作が、親テーブルでの DELETE による CASCADE の結果として発生し、その子テーブルの中で DELETE での INSTEAD OF トリガーが定義されている場合、そのトリガーは無視され、DELETE 操作が実行されます。  
  
## <a name="ddl-triggers"></a>DDL トリガー  
 DML トリガーと異なり、DDL トリガーのスコープはスキーマに設定されません。 そのため、DDL トリガーについてメタデータに問い合わせる際に、OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY、および OBJECTPROPERTY(EX) は使用できません。 代わりに、カタログ ビューを使用してください。 詳しくは、「[DDL トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-ddl-triggers.md)」をご覧ください。  
  
## <a name="logon-triggers"></a>ログオン トリガー  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] は、ログオン イベントによるトリガーをサポートしません。  
  
## <a name="permissions"></a>アクセス許可  
 DML トリガーを変更するには、トリガーが定義されているテーブルやビューに対する ALTER 権限が必要です。  
  
 サーバー スコープ (ON ALL SERVER) で定義されている DDL トリガー、またはログオン トリガーを変更するには、サーバーに対する CONTROL SERVER 権限が必要です。 データベース スコープ (ON DATABASE) で定義されている DDL トリガーを変更するには、現在のデータベースでの ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ユーザーが `SalesPersonQuotaHistory` テーブルにデータを追加したり、データを変更したりしようとすると、クライアントに対してユーザー定義のメッセージを出力する、AdventureWorks 2012 データベースの DML トリガーを作成します。 次に `ALTER TRIGGER` を使用してトリガーを変更し、トリガーを `INSERT` 操作だけに適用します。 このトリガーは、テーブルの更新や行の挿入を行うユーザーに対して、 `Compensation` 部門にも変更を知らせる必要があることを連絡できるので有用です。  
  
```  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  

-- Now, change the trigger.  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [ストアド プロシージャの作成](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [トランザクション](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [DML トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [DDL トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)   
 [パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
