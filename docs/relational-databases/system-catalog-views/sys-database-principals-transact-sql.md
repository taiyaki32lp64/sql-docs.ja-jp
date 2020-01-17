---
title: database_principals (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc9dd813736a2cc06f3108a0b3402e4cef99815e
ms.sourcegitcommit: ede04340adbf085e668a2536d4f7114abba14a0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761149"
---
# <a name="sysdatabase_principals-transact-sql"></a>database_principals (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース内のセキュリティプリンシパルごとに1行のデータを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**指定**|**sysname**|プリンシパルの名前。データベース内で一意です。|  
|**principal_id**|**通り**|プリンシパルの ID。データベース内で一意です。|  
|**各種**|**char (1)**|プリンシパルの種類:<br /><br /> A = アプリケーション ロール<br /><br /> C = 証明書にマップされたユーザー<br /><br /> E = Azure Active Directory の外部ユーザー<br /><br /> G = Windows グループ<br /><br /> K = 非対称キーにマップされたユーザー<br /><br /> R = データベース ロール<br /><br /> S = SQL ユーザー<br /><br /> U = Windows ユーザー<br /><br /> X = Azure Active Directory グループまたはアプリケーションからの外部グループ|  
|**type_desc**|**nvarchar (60)**|プリンシパルの種類の説明。<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|SQL 名でスキーマが指定されていない場合に使用される名前です。 型が S、U、またはでないプリンシパルの場合は Null です。|  
|**create_date**|**/**|プリンシパルが作成された日時。|  
|**modify_date**|**/**|プリンシパルが最後に変更された時刻。|  
|**owning_principal_id**|**通り**|このプリンシパルを所有するプリンシパルの ID。 データベースロール以外のすべてのプリンシパルは、 **dbo**によって所有されている必要があります。|  
|**sid**|**varbinary (85)**|プリンシパルの SID (セキュリティ識別子)。  SYS および INFORMATION スキーマの場合は NULL です。|  
|**is_fixed_role**|**bit**|1の場合、この行は固定データベースロールの1つのエントリ (db_owner、db_accessadmin、db_datareader、db_datawriter、db_ddladmin、db_securityadmin、db_backupoperator、db_denydatareader、db_denydatawriter) を表します。|  
|**authentication_type**|**通り**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降。<br /><br /> 認証の種類を示します。 使用可能な値とその説明を次に示します。<br /><br /> 0: 認証なし<br />1: インスタンス認証<br />2: データベース認証<br />3: Windows 認証|  
|**authentication_type_desc**|**nvarchar (60)**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降。<br /><br /> 認証の種類の説明。 使用可能な値とその説明を次に示します。<br /><br /> なし: 認証なし<br />インスタンス: インスタンス認証<br />データベース: データベース認証<br />WINDOWS: Windows 認証|  
|**default_language_name**|**sysname**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降。<br /><br /> このプリンシパルの既定の言語を示します。|  
|**default_language_lcid**|**通り**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降。<br /><br /> このプリンシパルの既定の LCID を示します。|  
|**allow_encrypted_value_modifications**|**bit**|**適用対象**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]以降、 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 一括コピー操作でのサーバーの暗号化メタデータ チェックを抑制します。 これにより、データの暗号化を解除することなく、テーブルまたはデータベース間で Always Encrypted を使用して暗号化されたデータを一括コピーできます。 既定値は OFF です。 |      
  
## <a name="remarks"></a>コメント  
 *PasswordLastSetTime*プロパティは、SQL Server のサポートされているすべての構成で使用できますが、その他のプロパティは SQL Server が Windows Server 2003 以降で実行されており、CHECK_POLICY と CHECK_EXPIRATION の両方が有効になっている場合にのみ使用できます。 詳細については、「[パスワードポリシー](../../relational-databases/security/password-policy.md) 」を参照してください。
Principal_id の値は、プリンシパルが削除された場合に再利用される可能性があるため、常に増加するとは限りません。
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは自分のユーザー名、システム ユーザー、および固定データベース ロールを参照できます。 他のユーザーを参照するには、ALTER ANY USER、またはユーザーに対する権限が必要です。 ユーザー定義ロールを参照するには、ALTER ANY ROLE、またはロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: データベース プリンシパルのすべての権限を一覧表示する  
 次のクエリは、データベースプリンシパルに対して明示的に許可または拒否されている権限を一覧表示します。  
  
> [!IMPORTANT]  
>  固定データベースロールの権限は、sys. database_permissions には表示されません。 そのため、データベースプリンシパルには、ここに記載されていない追加のアクセス許可がある場合があります。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: データベース内のスキーマオブジェクトに対する権限を一覧表示する  
 次のクエリでは、sys. database_principals と sys. database_permissions を、特定のスキーマオブジェクトに対して許可または拒否されている権限を一覧表示するために、sys. オブジェクトと sys スキーマに結合します。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: データベースプリンシパルのすべてのアクセス許可を一覧表示する  
 次のクエリは、データベースプリンシパルに対して明示的に許可または拒否されている権限を一覧表示します。  
  
> [!IMPORTANT]  
>  固定データベースロールの権限は、に`sys.database_permissions`は表示されません。 そのため、データベースプリンシパルには、ここに記載されていない追加のアクセス許可がある場合があります。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: データベース内のスキーマオブジェクトに対する権限を一覧表示する  
 次のクエリで`sys.database_principals`は`sys.database_permissions` 、 `sys.objects`特定`sys.schemas`のスキーマオブジェクトに対して許可または拒否されている権限を、およびと結合して一覧表示します。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>参照  
 [プリンシパル &#40;データベースエンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [server_principals &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [セキュリティカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [包含データベースユーザー-データベースの移植性を高める](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Azure Active Directory 認証を使用した SQL Database への接続](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


