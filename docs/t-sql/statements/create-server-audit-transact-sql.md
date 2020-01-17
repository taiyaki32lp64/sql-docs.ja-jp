---
title: CREATE SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: cc6f7c3ad9dc10e46a7abd1b044bcf70ff86f92d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983000"
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit を使用してサーバーの監査オブジェクトを作成します。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG | URL | EXTERNAL_MONITOR }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = | LIKE } { number | ' string ' }  
```  
  
## <a name="arguments"></a>引数  
 TO { FILE | APPLICATION_LOG | SECURITY_LOG | URL | EXTERNAL_MONITOR } 監査ターゲットの場所を決定します。 オプションは、バイナリ ファイル、Windows アプリケーション ログ、または Windows セキュリティ ログです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、Windows で追加の設定を行わないと Windows セキュリティ ログに書き込むことができません。 詳細については、「 [セキュリティ ログへの SQL サーバー監査イベントの書き込み](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)」を参照してください。  

> [!IMPORTANT]
> Azure SQL Database マネージド インスタンスでは SQL 監査はサーバー レベルで動作します。 場所は `URL` または `EXTERNAL_MONITOR` にのみすることができます。
  
 FILEPATH ='*os_file_path*'  
 監査ログのパス。 ファイル名は、監査名と監査 GUID に基づいて生成されます。  
  
 MAXSIZE = { *max_size }*  
 監査ファイルのサイズの上限を指定します。 *max_size* の値は、整数の後に MB、GB、TB を付けて指定するか、または UNLIMITED を指定します。 *max_size* に指定できる最小サイズは 2 MB、最大サイズは 2,147,483,647 TB です。 UNLIMITED を指定した場合、ファイルはディスクがいっぱいになるまで拡張されます。 0 も UNLIMITED を示します。2 MB 未満の値を指定すると、エラー MSG_MAXSIZE_TOO_SMALL が発生します。 既定値は UNLIMITED です。  
  
 MAX_ROLLOVER_FILES = *{ integer* | UNLIMITED }  
 現在のファイルに加えてファイル システム内に保持するファイルの最大数を指定します。 *MAX_ROLLOVER_FILES* 値には整数値または UNLIMITED を指定してください。 既定値は UNLIMITED です。 監査が再開されるたび ([!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの再起動時や、監査をオフにして再度オンにしたとき)、または MAXSIZE に達して新しいファイルが必要になった場合に、このパラメーターが評価されます。 *MAX_ROLLOVER_FILES* の評価時にファイル数が *MAX_ROLLOVER_FILES* の設定を超えている場合、最も古いファイルが削除されます。 そのため、*MAX_ROLLOVER_FILES* の設定が 0 の場合、*MAX_ROLLOVER_FILES* 設定が評価されるたびに新しいファイルが作成されます。 *MAX_ROLLOVER_FILES* 設定の評価時に自動的に削除されるファイルは 1 つだけです。したがって、*MAX_ROLLOVER_FILES* の値を下げても、古いファイルを手動で削除しない限り、ファイル数は少なくなりません。 指定できるファイルの最大数は 2,147,483,647 です。  
  
 MAX_FILES =*integer*  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 作成できる監査ファイルの最大数を指定します。 制限に達しても、最初のファイルへのロールオーバーは行われません。 MAX_FILES の制限に達すると、追加の監査イベントを生成させるアクションは失敗し、エラーが発生します。  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 このオプションは、ディスク上のファイルを MAXSIZE 値に事前に割り当てます。 MAXSIZE が UNLIMITED でない場合にのみ適用されます。 既定値は OFF です。  
  
 QUEUE_DELAY =*integer*  
 監査アクションの処理が強制されるまでの経過時間 (ミリ秒) を指定します。 値 0 は同期配信を表します。 クエリ遅延に設定可能な最小値は 1000 (1 秒) で、これが既定値です。 最大値は 2,147,483,647 (2,147,483.647 秒、つまり 24 日、20 時間、31 分、23.647 秒) です。 無効な数値を指定すると、MSG_INVALID_QUEUE_DELAY エラーが発生します。  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 ターゲットで監査ログへの書き込みができない場合に、ターゲットへのインスタンスの書き込みをエラーにするか、続行するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止するかを示します。 既定値は CONTINUE です。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作を続行します。 監査レコードは保持されません。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 続行オプションを選択すると、セキュリティ ポリシーに違反する可能性がある、監査されない活動を許可する場合があります。 完全な監査を維持することより、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の操作を続行することの方が重要である場合に、このオプションを使用します。  
  
SHUTDOWN  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がなんらかの理由で監査ターゲットへのデータの書き込みに失敗した場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを強制的にシャットダウンします。 `CREATE SERVER AUDIT` ステートメントを実行しているログインには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内での `SHUTDOWN` 権限が必要です。 実行中のログインから `SHUTDOWN` アクセス許可が後で取り消された場合でも、シャットダウンの動作は継続します。 ユーザーがこのアクセス許可を持っていない場合は、ステートメントが失敗し、監査は作成されません。 監査エラーによってシステムのセキュリティまたは整合性が阻害される可能性がある場合に、このオプションを使用します。 詳細については、「[SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md)」を参照してください。  
  
 FAIL_OPERATION  
 監査イベントを発生させるデータベース アクションを失敗させます。 監査イベントを発生させないアクションは続行できますが、監査イベントを発生させることはできません。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]へのフル アクセスより、完全な監査の維持の方が重要である場合に、このオプションを使用します。  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。

 AUDIT_GUID =*uniqueidentifier*  
 監査には、データベース ミラーリングなどのシナリオをサポートするために、ミラーリングされたデータベースで見つかった GUID と照合する特定の GUID が必要です。 この GUID は、監査が作成されると変更できなくなります。  
  
 predicate_expression  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 イベントを処理する必要があるかどうかを判定するために使用する述語式を指定します。 述語式は 3,000 文字に制限され、これにより文字列引数が制限されます。  
  
 event_field_name  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 述語ソースを識別するイベント フィールドの名前を指定します。 監査フィールドについては、「[sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)」で説明されています。 `file_name`、`audit_file_offset`、`event_time` 以外のすべてのフィールドは監査できます。  

> [!NOTE]  
>  `action_id` および `class_type` フィールドは、型が sys.fn_get_audit_file に示されている **varchar** で、フィルター対象の述語ソースである場合にのみ、数値と共に使用できます。 `class_type` で使用する値のリストを取得するには、次のクエリを実行します。  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 **decimal** を含む任意の数値型です。 制限として、使用可能な物理メモリの不足、または 64 ビット整数として表すのに大きすぎる数字が挙げられます。  
  
 ' string '  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 述語の比較に必要な ANSI 文字列または Unicode 文字列です。 述語比較関数に対しては、暗黙の文字列型変換は行われません。 無効な型を渡すとエラーになります。  
  
## <a name="remarks"></a>Remarks  
 作成されたサーバー監査は無効な状態です。  
  
 CREATE SERVER AUDIT ステートメントはトランザクションのスコープ内にあります。 トランザクションがロールバックされると、ステートメントもロールバックされます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバー監査を作成、変更、または削除する場合、プリンシパルには、ALTER ANY SERVER AUDIT または CONTROL SERVER の権限が必要です。  
  
 改ざんを防止するために監査情報をファイルに保存する場合は、そのファイルの場所へのアクセスを制限します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. ファイル ターゲットを使用するサーバー監査を作成する  
 次の例では、バイナリ ファイルをターゲットとする `HIPAA_Audit` というサーバー監査を、オプションなしで作成します。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. Windows アプリケーション ログ ターゲットを使用するサーバー監査をオプション付きで作成する  
 次の例では、Windows アプリケーション ログをターゲット セットとする `HIPAA_Audit` というサーバー監査を作成します。 キューには 1 秒ごとに書き込みが行われ、失敗時はキューによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンがシャットダウンされます。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. WHERE 句を含むサーバー監査を作成する  
 次の例では、データベース、スキーマ、およびサンプルの 2 つのテーブルを作成します。 `DataSchema.SensitiveData` という名前のテーブルには機密データが含まれ、このテーブルへのアクセスは監査に記録する必要があります。 `DataSchema.GeneralData` という名前のテーブルには、機密データは含まれません。 データベース監査の仕様によって、`DataSchema` スキーマのすべてのオブジェクトへのアクセスが監査されます。 サーバー監査の対象を `SensitiveData` テーブルのみに制限する WHERE 句付きで、サーバー監査が作成されます。 サーバー監査は、監査フォルダーが `C:\SQLAudit` にあることを前提としています。  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
