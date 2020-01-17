---
title: ALTER SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c4649a591f7261943d2d5393678f63888930c01f
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982035"
---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 機能を使用して、サーバー監査オブジェクトを変更します。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } | URL]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>引数  
 TO { FILE | APPLICATION_LOG | SECURITY |URL}  
 監査ターゲットの場所を指定します。 オプションは、バイナリ ファイル、Windows アプリケーション ログ、または Windows セキュリティ ログです。  

> [!IMPORTANT]
> Azure SQL Database マネージド インスタンスでは SQL 監査はサーバー レベルで動作し、Azure Blob Storage に `.xel` ファイルを格納します。
  
 FILEPATH **= '** _os\_file\_path_ **'**  
 監査記録のパス。 ファイル名は、監査名と監査 GUID に基づいて生成されます。  
  
 MAXSIZE **=** _max\_size_  
 監査ファイルのサイズの上限を指定します。 *max_size* の値は、整数の後に **MB**、**GB**、**TB** を付けて指定するか、または **UNLIMITED** を指定します。 *max_size* に指定できる最小サイズは 2 **MB**、最大サイズは 2,147,483,647 **TB** です。 **UNLIMITED** を指定した場合、ファイルはディスクがいっぱいになるまで拡張されます。 2 MB 未満の値を指定すると、MSG_MAXSIZE_TOO_SMALL エラーが発生します。 既定値は **UNLIMITED** です。  
  
 MAX_ROLLOVER_FILES **=** _integer_ | **UNLIMITED**  
 ファイル システム内に保持するファイルの最大数を指定します。 MAX_ROLLOVER_FILES=0 が設定されている場合、作成されるロールオーバー ファイルの数は制限されません。 既定値は 0 です。 指定できるファイルの最大数は 2,147,483,647 です。  
  
 MAX_FILES =*integer*  
 作成できる監査ファイルの最大数を指定します。 制限に達しても、最初のファイルへのロールオーバーは行われません。 MAX_FILES の制限に達すると、追加の監査イベントを生成させるアクションは失敗し、エラーが発生します。  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 RESERVE_DISK_SPACE **=** { ON | OFF }  
 このオプションは、ディスク上のファイルを MAXSIZE 値に事前に割り当てます。 MAXSIZE が UNLIMITED でない場合にのみ適用されます。 既定値は OFF です。  
  
 QUEUE_DELAY **=** _integer_  
 監査アクションの処理が強制されるまでの経過時間 (ミリ秒) を指定します。 値 0 は同期配信を表します。 クエリ遅延に設定可能な最小値は 1000 (1 秒) で、これが既定値です。 最大値は 2,147,483,647 (2,147,483.647 秒、つまり 24 日、20 時間、31 分、23.647 秒) です。 無効な数値を指定すると、MSG_INVALID_QUEUE_DELAY エラーが発生します。  
  
 ON_FAILURE **=** { CONTINUE | SHUTDOWN | FAIL_OPERATION}  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が監査ログに書き込むことができない場合に、ターゲットへのインスタンスの書き込みをエラーにするか、続行するか、停止するかを示します。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作を続行します。 監査レコードは保持されません。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 続行オプションを選択すると、セキュリティ ポリシーに違反する可能性がある、監査されない活動を許可する場合があります。 完全な監査を維持することより、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の操作を続行することの方が重要である場合に、このオプションを使用します。  
  
SHUTDOWN  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がなんらかの理由で監査ターゲットへのデータの書き込みに失敗した場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを強制的にシャットダウンします。 `ALTER` ステートメントを実行しているログインには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内での `SHUTDOWN` 権限が必要です。 実行中のログインから `SHUTDOWN` 権限が後で取り消された場合でも、シャットダウンの動作は継続します。 ユーザーがこの権限を持っていない場合は、ステートメントが失敗し、監査は変更されません。 監査エラーによってシステムのセキュリティまたは整合性が阻害される可能性がある場合に、このオプションを使用します。 詳細については、「[SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md)」を参照してください。 
  
 FAIL_OPERATION  
 監査イベントを発生させるデータベース アクションを失敗させます。 監査イベントを発生させないアクションは続行できますが、監査イベントを発生させることはできません。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]へのフル アクセスより、完全な監査の維持の方が重要である場合に、このオプションを使用します。  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。   
  
 STATE **=** { ON | OFF }  
 監査によるレコードの収集を有効または無効にします。 実行中の監査の状態を (ON から OFF に) 変更すると、監査が停止されたこと示す監査エントリ、監査を停止したプリンシパル、および監査が停止された時間が作成されます。  
  
 MODIFY NAME = *new_audit_name*  
 監査の名前を変更します。 他のオプションと組み合わせて使用することはできません。  
  
 predicate_expression  
 イベントを処理する必要があるかどうかを判定するために使用する述語式を指定します。 述語式は 3,000 文字に制限され、これにより文字列引数が制限されます。  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 event_field_name  
 述語ソースを識別するイベント フィールドの名前を指定します。 監査フィールドについては、「[sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)」で説明されています。 `file_name` と `audit_file_offset` 以外のすべてのフィールドは、監査できます。  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 number  
 **decimal** を含む任意の数値型です。 制限として、使用可能な物理メモリの不足、または 64 ビット整数として表すのに大きすぎる数字が挙げられます。  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 ' string '  
 述語の比較に必要な ANSI 文字列または Unicode 文字列です。 述語比較関数に対しては、暗黙の文字列型変換は行われません。 無効な型を渡すとエラーになります。  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
## <a name="remarks"></a>Remarks  
 ALTER AUDIT を呼び出すときは、TO 句、WITH 句、MODIFY NAME 句のうち少なくとも 1 つを指定する必要があります。  
  
 監査を変更する場合は、監査の状態を OFF オプションに設定する必要があります。 STATE=OFF 以外のオプションを使用して監査を有効にしているときに ALTER AUDIT を実行すると、MSG_NEED_AUDIT_DISABLED エラー メッセージが表示されます。  
  
 監査仕様の追加、変更、および削除は、監査を停止せずに実行できます。  
  
 監査を作成した後で、監査の GUID を変更することはできません。  
 
 **ALTER SERVER AUDIT** ステートメントはユーザー トランザクション内では使用できません。
 
## <a name="permissions"></a>アクセス許可  
 サーバー監査のプリンシパルを作成、変更、または削除するには、ALTER ANY SERVER AUDIT 権限または CONTROL SERVER 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-a-server-audit-name"></a>A. サーバー監査の名前を変更する  
 次の例では、サーバー監査 `HIPAA_Audit` の名前を `HIPAA_Audit_Old` に変更します。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. サーバー監査のターゲットを変更する  
 次の例では、`HIPAA_Audit` というサーバー監査を、ファイル ターゲットに変更します。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. サーバー監査 WHERE 句を変更する  
 次の例は、「[CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)」の例 C で作成した WHERE 句を変更します。 新しい WHERE 句は、ユーザー定義イベントを 27 でフィルター選択します。  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. WHERE 句を削除する  
 次の例では、WHERE 句の述語式を削除します。  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. サーバー監査の名前を変更する  
 次の例では、サーバー監査の名前を `FilterForSensitiveData` から `AuditDataAccess` に変更します。  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>参照  
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
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
