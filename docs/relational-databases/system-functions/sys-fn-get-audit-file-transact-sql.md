---
title: fn_get_audit_file (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25d4aa1e82097dcc4027809c7292587a20862d75
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981874"
---
# <a name="sysfn_get_audit_file-transact-sql"></a>fn_get_audit_file (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサーバー監査で作成された監査ファイルからの情報を返します。 詳細については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>引数  
 *file_pattern*  
 読み取り対象に設定する監査ファイルのディレクトリまたはパスとファイル名を指定します。 種類は**nvarchar (260)** です。 
 
 - **SQL Server**:
    
    この引数には、パス (ドライブ文字またはネットワーク共有) とファイル名の両方を含める必要があります。ファイル名にはワイルドカードを使用できます。 1つのアスタリスク (*) を使用して、監査ファイルセットから複数のファイルを収集できます。 例 :  
  
    -   **\<path>\\ \*** 収集 - すべての監査ファイルが指定された場所にします。  
  
    -   **\<path> \LoginsAudit_{GUID}** 収集 - すべての監査を指定した名前と GUID のペアを持つファイル。  
  
    -   **\<path>\LoginsAudit_{GUID}_00_29384.sqlaudit** - Collect a specific audit file.  
  
 - **Azure SQL Database または Azure SQL Data Warehouse**:
 
    この引数は、blob の URL (ストレージエンドポイントとコンテナーを含む) を指定するために使用されます。 アスタリスクのワイルドカードはサポートされていませんが、完全な blob 名ではなく、部分的なファイル (blob) 名プレフィックスを使用して、このプレフィックスで始まる複数のファイル (blob) を収集できます。 例 :
 
      - **\<Storage_endpoint\>/\<Container\>/\<ServerName\>/\<DatabaseName\>/** -特定のデータベースのすべての監査ファイル (blob) を収集します。    
      
      - **\<Storage_endpoint\>/\<\<Container\>\>/\<ServerName\>/\<DatabaseName\> / \<AuditName\>/\<CreationDate\>/\<FileName\>.xel** -特定の監査ファイル (blob) を収集します。
  
> [!NOTE]  
>  ファイル名のパターンがないパスを渡すとエラーが発生します。  
  
 *initial_file_name*  
 監査レコードの読み取りを開始する監査ファイルセット内の特定のファイルのパスと名前を指定します。 種類は**nvarchar (260)** です。  
  
> [!NOTE]  
>  *Initial_file_name*引数には、有効なエントリが含まれているか、または default | を含んでいる必要があります。NULL 値。  
  
 *audit_record_offset*  
 Initial_file_name に対して指定されたファイルを持つ既知の場所を指定します。 この引数を使用した場合、関数は、指定されたオフセットの直後にあるバッファーの最初のレコードから読み取りを開始します。  
  
> [!NOTE]  
>  *Audit_record_offset*引数には、有効なエントリが含まれているか、または default | を含んでいる必要があります。NULL 値。 型は**bigint**です。  
  
## <a name="tables-returned"></a>返されるテーブル  
 次の表に、この関数から返される監査ファイルの内容を示します。  
  
| 列名 | [型] | [説明] |  
|-------------|------|-------------|  
| action_id | **varchar (4)** | アクションの ID。 Null 値は許容されません。 |  
| additional_information | **nvarchar (4000)** | 単一のイベントに対してだけ適用される固有の情報が XML として返されます。 少数の監査可能なアクションには、この種の情報が含まれています。<br /><br /> Tsql スタックが関連付けられているアクションに対して、1レベルの TSQL スタックが XML 形式で表示されます。 XML 形式は次のようになります。<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> frame nest_level は、フレームの現在の入れ子レベルを示します。 モジュール名は、3つの部分形式 (database_name、schema_name と object_name) で表されます。  モジュール名は、`'\<'`、`'>'`、`'/'`、`'_x'`などの無効な xml 文字をエスケープするために解析されます。 これらは `_xHHHH\_`としてエスケープされます。 HHHH は、文字の4桁の16進数の UCS 2 コードを表します。<br /><br /> NULL 値が許可されます。 イベントから追加情報が報告されない場合は NULL を返します。 |
| affected_rows | **bigint** | **適用対象**: AZURE SQL DB のみ<br /><br /> 実行されたステートメントの影響を受けた行の数。 |  
| application_name | **nvarchar(128)** | **適用対象**: AZURE SQL DB + SQL Server (2017 以降)<br /><br /> 監査イベントの原因となったステートメントを実行したクライアントアプリケーションの名前 |  
| audit_file_offset | **bigint** | **適用対象**: SQL Server のみ<br /><br /> 監査レコードを格納しているファイル内のバッファーオフセット。 NULL 値は許可されません。 |  
| audit_schema_version | **int** | 常に1 |  
| class_type | **varchar(2)** | 監査が発生する監査可能なエンティティの種類。 NULL 値は許可されません。 |  
| client_ip | **nvarchar(128)** | **適用対象**: AZURE SQL DB + SQL Server (2017 以降)<br /><br />    クライアントアプリケーションのソース IP |  
| connection_id | GUID | **適用対象**: AZURE SQL DB とマネージインスタンス<br /><br /> サーバー内の接続の ID |
| data_sensitivity_information | nvarchar (4000) | **適用対象**: AZURE SQL DB のみ<br /><br /> データベース内の分類済みの列に基づいて、監査対象のクエリによって返される情報の種類と機密ラベル。 [Azure SQL Database データの検出と分類](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification)に関する詳細情報 |
| database_name | **sysname** | アクションが発生したデータベース コンテキスト。 NULL 値が許可されます。 サーバーレベルで発生する監査の場合は NULL を返します。 |  
| database_principal_id | **int** |アクションが実行されるデータベース ユーザー コンテキストの ID。 NULL 値は許可されません。 この値が適用されない場合は0を返します。 たとえば、サーバー操作などの場合です。|
| database_principal_name | **sysname** | 現在のユーザー。 NULL 値が許可されます。 使用できない場合は NULL を返します。 |  
| duration_milliseconds | **bigint** | **適用対象**: AZURE SQL DB とマネージインスタンス<br /><br /> クエリ実行時間 (ミリ秒) |
| event_time | **datetime2** | 監査可能なアクションが発生した日時。 NULL 値は許可されません。 |  
| file_name | **varchar(260)** | レコードの送信元の監査ログファイルのパスと名前。 NULL 値は許可されません。 |
| is_column_permission | **bit** | 列レベルの権限かどうかを示すフラグ。 NULL 値は許可されません。 Permission_bitmask が0の場合は0を返します。<br /> 1 = true<br /> 0 = false |
| object_id | **int** | 監査が発生したエンティティの ID。 これには、次の内容が含まれます。<br /> サーバーオブジェクト<br /> データベース<br /> データベース オブジェクト<br /> スキーマ オブジェクト<br /> NULL 値は許可されません。 エンティティがサーバー自体である場合、または監査がオブジェクト レベルで実行されない場合は 0 を返します。 たとえば、認証などの場合です。 |  
| object_name | **sysname** | 監査が発生したエンティティの名前。 これには、次の内容が含まれます。<br /> サーバーオブジェクト<br /> データベース<br /> データベース オブジェクト<br /> スキーマ オブジェクト<br /> NULL 値が許可されます。 エンティティがサーバー自体である場合、または監査がオブジェクト レベルで実行されない場合は NULL を返します。 たとえば、認証などの場合です。 |
| permission_bitmask | **varbinary(16)** | 一部のアクションでは、権限の許可、拒否、または取り消しを示します。 |
| response_rows | **bigint** | **適用対象**: AZURE SQL DB とマネージインスタンス<br /><br /> 結果セットで返される行の数。 |  
| schema_name | **sysname** | アクションが発生したスキーマ コンテキスト。 NULL 値が許可されます。 スキーマの外部で発生する監査の場合は NULL を返します。 |  
| sequence_group_id | **varbinary** | **適用対象**: SQL Server のみ (2016 以降)<br /><br />  一意識別子 |  
| sequence_number | **int** | 大きすぎて監査の書き込みバッファーに収まらなかった 1 つの監査レコード内のレコードの順序を追跡します。 NULL 値は許可されません。 |  
| server_instance_name | **sysname** | 監査が発生したサーバー インスタンスの名前。 標準の server\instance 形式が使用されます。 |  
| server_principal_id | **int** | アクションが実行されるログイン コンテキストの ID。 NULL 値は許可されません。 |  
| server_principal_name | **sysname** | 現在のログイン。 NULL 値が許可されます。 |  
| server_principal_sid | **varbinary** | 現在のログイン SID。 NULL 値が許可されます。 |  
| session_id | **smallint** | イベントが発生したセッションの ID。 NULL 値は許可されません。 |  
| session_server_principal_name | **sysname** | セッションのサーバープリンシパル。 NULL 値が許可されます。 |  
| statement | **nvarchar (4000)** | TSQL ステートメント (存在する場合)。 NULL 値が許可されます。 該当しない場合は NULL を返します。 |  
| succeeded | **bit** | イベントをトリガーしたアクションが成功したかどうかを示します。 NULL 値は許可されません。 ログイン イベント以外のすべてのイベントで、操作ではなく、権限チェックが成功したか失敗したかのみを報告します。<br /> 1 = 成功<br /> 0 = 失敗 |
| target_database_principal_id | **int** | GRANT/DENY/REVOKE 操作が実行されるデータベースプリンシパル。 NULL 値は許可されません。 該当しない場合は0を返します。 |  
| target_database_principal_name | **sysname** | アクションの対象ユーザー。 NULL 値が許可されます。 該当しない場合は NULL を返します。 |  
| target_server_principal_id | **int** | GRANT/DENY/REVOKE 操作が実行されるサーバー プリンシパル。 NULL 値は許可されません。 該当しない場合は0を返します。 |  
| target_server_principal_name | **sysname** | アクションの対象ログイン。 NULL 値が許可されます。 該当しない場合は NULL を返します。 |  
| target_server_principal_sid | **varbinary** | ターゲットログインの SID。 NULL 値が許可されます。 該当しない場合は NULL を返します。 |  
| transaction_id | **bigint** | **適用対象**: SQL Server のみ (2016 以降)<br /><br /> 1つのトランザクションで複数の監査イベントを識別するための一意の識別子 |  
| user_defined_event_id | **smallint** | **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降、AZURE SQL DB、マネージインスタンス<br /><br /> **Sp_audit_write**に引数として渡されたユーザー定義イベント id。 システムイベント (既定値) の場合は**NULL** 、ユーザー定義イベントの場合は0以外。 詳細については、「 [transact-sql &#40;&#41;の sp_audit_write](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md)」を参照してください。 |  
| user_defined_information | **nvarchar (4000)** | **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降、AZURE SQL DB、マネージインスタンス<br /><br /> **Sp_audit_write**ストアドプロシージャを使用して、監査ログに記録する必要のある追加情報を記録するために使用します。 |  

  
## <a name="remarks"></a>Remarks  
 **Fn_get_audit_file**に渡された*file_pattern*引数が、存在しないパスまたはファイルを参照している場合、またはファイルが監査ファイルでない場合は、 **MSG_INVALID_AUDIT_FILE**エラーメッセージが返されます。  
  
## <a name="permissions"></a>アクセス許可

- **SQL Server**: **CONTROL Server**権限が必要です。  
- **AZURE SQL DB**: **CONTROL DATABASE**権限が必要です。     
  - サーバー管理者は、サーバー上のすべてのデータベースの監査ログにアクセスできます。
  - 非サーバー管理者は、現在のデータベースからの監査ログにのみアクセスできます。
  - 上記の条件を満たしていない blob はスキップされます (スキップされた blob の一覧がクエリ出力メッセージに表示されます)。関数は、アクセスが許可されている blob からのログのみを返します。  
  
## <a name="examples"></a>使用例

- **SQL Server**

  この例では、`\\serverName\Audit\HIPAA_AUDIT.sqlaudit` という名前のファイルから読み取ります。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL データベース**

  この例では、`ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`という名前のファイルを読み取ります。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  この例で、追加の T-SQL 句を使用した前述のように、同じファイルから読み取ります (**TOP**、 **ORDER BY**、および**WHERE**句によって返される監査レコードをフィルター処理するため、関数の場合):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  この例では、`Sh`で始まるサーバーからすべての監査ログを読み取ります。 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

監査を作成する方法の完全な例については、「[SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」をご覧ください。

Azure SQL Database 監査の設定の詳細については、「 [SQL Database 監査の概要](https://docs.microsoft.com/azure/sql-database/sql-database-auditing)」を参照してください。
  
## <a name="see-also"></a>参照  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する方法](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
