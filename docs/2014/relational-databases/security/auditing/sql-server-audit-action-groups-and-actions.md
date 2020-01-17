---
title: SQL Server 監査のアクション グループとアクション | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e204a1865c2a928079fcd9b32b31a8ae0c0bd0a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238132"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>SQL Server 監査のアクション グループとアクション
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 機能を使用すると、サーバー レベルおよびデータベース レベルのイベントのグループおよび個別のイベントを監査することができます。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](sql-server-audit-database-engine.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の監査は、0 個以上の監査アクション項目で構成されます。 これらの監査アクション項目には、アクションのグループ (Server_Object_Change_Group など) を使用することも、個別のアクション (テーブルに対する SELECT 操作など) を使用することもできます。  
  
> [!NOTE]  
>  Server_Object_Change_Group には、任意のサーバー オブジェクト (データベースまたはエンドポイント) に対する CREATE、ALTER、および DROP が含まれます。  
  
 監査には次のカテゴリのアクションが含まれます。  
  
-   サーバー レベル。 これらのアクションには、管理の変更やログオンおよびログオフの操作などのサーバーの操作が含まれます。  
  
-   データベース レベル。 これらのアクションには、データ操作言語 (DML) とデータ定義言語 (DDL) の操作が含まれます。  
  
-   監査レベル。 これらのアクションには、監査プロセス内のアクションが含まれます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の監査コンポーネントに対して実行されるアクションが、特定の監査でもともと監査されている場合もあります。そのような場合は、親オブジェクトで監査イベントが発生するため、監査イベントが自動的に発生します。  
  
 もともと監査されているアクションを以下に示します。  
  
-   Server Audit の状態の変更 (状態を ON または OFF に設定)  
  
 もともと監査されていないイベントを以下に示します。  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 監査はすべて、最初の作成時には無効になります。  
  
## <a name="server-level-audit-action-groups"></a>サーバー レベルの監査アクション グループ  
 サーバー レベルの監査アクション グループは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティ監査イベント クラスに似ています。 詳しくは、「 [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md)」をご覧ください。  
  
 サーバー レベルの監査アクション グループと、同等の SQL Server イベント クラス (存在する場合) を次の表に示します。  
  
|アクション グループ名|説明|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|このイベントは、アプリケーション ロールのパスワードが変更されるたびに発生します。 [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md)と同じです。|  
|AUDIT_CHANGE_GROUP|このイベントは、任意の監査が作成、変更、または削除されるたびに発生します。 このイベントは、任意の監査の仕様が作成、変更、または削除されるたびに発生します。 監査に対する変更はすべてその監査内で監査されます。 [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md)と同じです。|  
|BACKUP_RESTORE_GROUP|このイベントは、バックアップまたは復元のコマンドが実行されるたびに発生します。 [Audit Backup/Restore イベント クラス](../../event-classes/audit-backup-and-restore-event-class.md)と同じです。|  
|BROKER_LOGIN_GROUP|このイベントは、Service Broker トランスポート セキュリティに関する監査メッセージを報告するために発生します。 [Audit Broker Login Event Class](../../event-classes/audit-broker-login-event-class.md)と同じです。|  
|DATABASE_CHANGE_GROUP|このイベントは、データベースが作成、変更、または削除されるときに発生します。 このイベントは、任意のデータベースが作成、変更、または削除されるたびに発生します。 [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md)と同じです。|  
|DATABASE_LOGOUT_GROUP|このイベントは、包含データベースのユーザーがデータベースをログアウトするときに発生します。 Database Logout Event Class と同じです。|  
|DATABASE_MIRRORING_LOGIN_GROUP|このイベントは、データベース ミラーリングのトランスポート セキュリティに関する監査メッセージを報告するために発生します。 [Audit Database Mirroring Login Event Class](../../event-classes/audit-database-mirroring-login-event-class.md)と同じです。|  
|DATABASE_OBJECT_ACCESS_GROUP|このイベントは、メッセージ型、アセンブリ、コントラクトなどのデータベース オブジェクトへのアクセスが行われるたびに発生します。<br /><br /> このイベントは、任意のデータベースへの任意のアクセスに対して発生します。 **注:** 大量の監査レコードにこの可能性があること。 <br /><br /> [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md)と同じです。|  
|DATABASE_OBJECT_CHANGE_GROUP|このイベントは、スキーマなどのデータベース オブジェクトで、CREATE、ALTER、または DROP ステートメントが実行されたときに発生します。 このイベントは、任意のデータベース オブジェクトが作成、変更、または削除されるたびに発生します。 **注:** 非常に大量の監査レコードにこの可能性があります。 <br /><br /> [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md)と同じです。|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|このイベントは、データベース スコープ内のオブジェクトの所有者が変更されたときに発生します。 このイベントは、サーバー上の任意のデータベースの任意のオブジェクト所有権の変更に対して発生します。 [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md)と同じです。|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|このイベントは、アセンブリやスキーマなどのデータベース オブジェクトに対して GRANT、REVOKE、または DENY が実行された場合に発生します。 このイベントは、サーバー上の任意のデータベースの任意のオブジェクト権限の変更に対して発生します。 [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md)と同じです。|  
|DATABASE_OPERATION_GROUP|このイベントは、チェックポイントやクエリ通知のサブスクライブなど、データベースの操作が行われたときに発生します。 このイベントは、任意のデータベースの任意のデータベース操作に対して発生します。 [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md)と同じです。|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|このイベントは、ALTER AUTHORIZATION ステートメントを使用してデータベースの所有者を変更した場合に、この動作に必要な権限の確認が行われる際に発生します。 このイベントは、サーバー上の任意のデータベースの、任意のデータベース所有権の変更に対して発生します。 [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md)と同じです。|  
|DATABASE_PERMISSION_CHANGE_GROUP|このイベントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の任意のプリンシパルによって、ステートメント権限に対して GRANT、REVOKE、または DENY が実行されるたびに発生します (データベースに対する権限の許可などのデータベース限定のイベントに適用されます)。<br /><br /> このイベントは、サーバー上の任意のデータベースの、任意のデータベース権限の変更 (GDR) に対して発生します。 [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md)と同じです。|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|このイベントは、ユーザーなどのプリンシパルがデータベースで作成、変更、または削除されるときに発生します。 [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md)と同じです。 (Audit Add DB Principal イベント クラスとも同じです。このイベント クラスは、非推奨の sp_grantdbaccess、sp_revokedbaccess、sp_addPrincipal、および sp_dropPrincipal の各ストアド プロシージャに対して発生します)。<br /><br /> このイベントは、sp_addrole ストアド プロシージャまたは sp_droprole ストアド プロシージャを使用してデータベース ロールが追加または削除されるたびに発生します。 このイベントは、任意のデータベースで任意のデータベース プリンシパルが作成、変更、または削除されるたびに発生します。 [Audit Add Role イベント クラス](../../event-classes/audit-add-role-event-class.md)と同じです。|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|このイベントは、データベースのスコープ内に、EXECUTE AS \<principal> や SETPRINCIPAL などの権限借用の操作が存在するときに発生します。 このイベントは、任意のデータベースで行われた権限の借用に対して発生します。 [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md)と同じです。|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|このイベントは、データベース ロールにログインが追加または削除されるたびに発生します。 このイベント クラスは、sp_addrolemember、sp_changegroup、および sp_droprolemember の各ストアド プロシージャに対して発生します。 このイベントは、任意のデータベースの任意のデータベース ロール メンバーの変更に対して発生します。 [Audit Add Member to DB Role イベント クラス](../../event-classes/audit-add-member-to-db-role-event-class.md)と同じです。|  
|DBCC_GROUP|このイベントは、プリンシパルが任意の DBCC コマンドを実行するたびに発生します。 [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md)と同じです。|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|プリンシパルが包含データベースにログオンしようとして失敗したことを示します。 このクラスのイベントは、新しい接続によって生じることも、接続プールから再利用された接続によって生じることもあります。 [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md)と同じです。|  
|FAILED_LOGIN_GROUP|プリンシパルが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] へのログインを試みて失敗したことを示します。 このクラスのイベントは、新しい接続によって生じることも、接続プールから再利用された接続によって生じることもあります。 [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md)と同じです。|  
|FULLTEXT_GROUP|フルテキスト イベントが発生したことを示します。 [Audit Fulltext Event Class](../../event-classes/audit-fulltext-event-class.md)と同じです。|  
|LOGIN_CHANGE_PASSWORD_GROUP|このイベントは、ALTER LOGIN ステートメントまたは sp_password ストアド プロシージャを使用してログインのパスワードが変更されるたびに発生します。 [Audit Login Change Password Event Class](../../event-classes/audit-login-change-password-event-class.md)と同じです。|  
|LOGOUT_GROUP|プリンシパルが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]からログアウトしたことを示します。 このクラスのイベントは、新しい接続によって生じることも、接続プールから再利用された接続によって生じることもあります。 [Audit Logout Event Class](../../event-classes/audit-logout-event-class.md)と同じです。|  
|SCHEMA_OBJECT_ACCESS_GROUP|このイベントは、スキーマでオブジェクト権限が使用されるたびに発生します。 [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md)と同じです。|  
|SCHEMA_OBJECT_CHANGE_GROUP|このイベントは、スキーマに対して CREATE、ALTER、または DROP の各操作が実行されたときに発生します。 [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md)と同じです。<br /><br /> このイベントはスキーマ オブジェクトで発生します。 [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md)と同じです。<br /><br /> このイベントは、任意のデータベースの任意のスキーマが変更されるたびに発生します。 [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md)と同じです。|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|このイベントは、スキーマ オブジェクト (テーブル、プロシージャ、関数など) の所有者を変更する権限について確認が行われる際に発生します。 この確認動作は、ALTER AUTHORIZATION ステートメントを使用してオブジェクトに所有者を割り当てたときに行われます。 このイベントは、サーバー上の任意のデータベースの任意のスキーマ所有権の変更に対して発生します。 [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md)と同じです。|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|このイベントは、スキーマ オブジェクトに対して GRANT、DENY、または REVOKE が実行されるたびに発生します。 [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md)と同じです。|  
|SERVER_OBJECT_CHANGE_GROUP|このイベントは、サーバー オブジェクトに対して CREATE、ALTER、または DROP の各操作が実行されたときに発生します。 [Audit Server Object Management Event Class](../../event-classes/audit-server-object-management-event-class.md)と同じです。|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|このイベントは、サーバー スコープ内のオブジェクトの所有者が変更されたときに発生します。 [Audit Server Object Take Ownership Event Class](../../event-classes/audit-server-object-take-ownership-event-class.md)と同じです。|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|このイベントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の任意のプリンシパルによって、サーバー オブジェクトの権限に対して GRANT、REVOKE、または DENY が実行されるたびに発生します。 [Audit Server Object GDR Event Class](../../event-classes/audit-server-object-gdr-event-class.md)と同じです。|  
|SERVER_OPERATION_GROUP|このイベントは、設定、リソース、外部アクセス、承認の変更などのセキュリティ監査操作が使用されるときに発生します。 [Audit Server Operation Event Class](../../event-classes/audit-server-operation-event-class.md)と同じです。|  
|SERVER_PERMISSION_CHANGE_GROUP|このイベントは、ログインの作成など、サーバー スコープでの権限に対して GRANT、REVOKE、または DENY が実行されているときに発生します。 [Audit Server Scope GDR Event Class](../../event-classes/audit-server-scope-gdr-event-class.md)と同じです。|  
|SERVER_PRINCIPAL_CHANGE_GROUP|このイベントは、サーバー プリンシパルが作成、変更、または削除されるときに発生します。 [Audit Server Principal Management Event Class](../../event-classes/audit-server-principal-management-event-class.md)と同じです。<br /><br /> このイベントは、プリンシパルが sp_defaultdb ストアド プロシージャ、sp_defaultlanguage ストアド プロシージャ、または ALTER LOGIN ステートメントを実行したときに発生します。 [Audit Addlogin Event Class](../../event-classes/audit-addlogin-event-class.md)と同じです。<br /><br /> このイベントは、sp_addlogin ストアド プロシージャおよび sp_droplogin ストアド プロシージャに対して発生します。 [Audit Login Change Property Event Class](../../event-classes/audit-login-change-property-event-class.md)とも同じです。<br /><br /> このイベントは、sp_grantlogin または sp_revokelogin のストアド プロシージャ。 [Audit Login GDR Event Class](../../event-classes/audit-login-gdr-event-class.md)と同じです。|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|このイベントは、サーバーのスコープ内に、EXECUTE AS \<login> などの権限の借用が存在するときに発生します。 [Audit Server Principal Impersonation Event Class](../../event-classes/audit-server-principal-impersonation-event-class.md)と同じです。|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|このイベントは、固定サーバー ロールにログインが追加または削除されるたびに発生します。 このイベントは sp_addsrvrolemember ストアド プロシージャと sp_dropsrvrolemember ストアド プロシージャに対して発生します。 [Audit Add Login to Server Role イベント クラス](../../event-classes/audit-add-login-to-server-role-event-class.md)と同じです。|  
|SERVER_STATE_CHANGE_GROUP|このイベントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスの状態が変更されたときに発生します。 [Audit Server Starts and Stops Event Class](../../event-classes/audit-server-starts-and-stops-event-class.md)と同じです。|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|プリンシパルが包含データベースに正常にログインしたことを示します。 Audit Successful Database Authentication Event Class と同じです。|  
|SUCCESSFUL_LOGIN_GROUP|プリンシパルが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に正常にログインしたことを示します。 このクラスのイベントは、新しい接続によって生じることも、接続プールから再利用された接続によって生じることもあります。 [Audit Login Event Class](../../event-classes/audit-login-event-class.md)と同じです。|  
|TRACE_CHANGE_GROUP|このイベントは、ALTER TRACE 権限をチェックするすべてのステートメントで発生します。 [Audit Server Alter Trace Event Class](../../event-classes/audit-server-alter-trace-event-class.md)と同じです。|  
|USER_CHANGE_PASSWORD_GROUP|このイベントは、包含データベースのユーザーのパスワードが USER ALTER ステートメントを使用して変更されるたびに発生します。|  
|USER_DEFINED_AUDIT_GROUP|このグループは、[sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql) の使用によって発生するイベントを監視します。 通常、トリガーまたはストアド プロシージャには、重要なイベントを監査できるようにするために、`sp_audit_write` への呼び出しが含まれています。|  
  
### <a name="considerations"></a>考慮事項  
 サーバー レベルのアクション グループは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス全体のアクションを対象とします。 たとえば、該当するアクション グループをサーバー監査の仕様に追加すると、任意のデータベースの任意のスキーマ オブジェクトのアクセス確認が記録されます。 データベース監査の仕様では、そのデータベースのスキーマ オブジェクト アクセスのみが記録されます。  
  
 サーバー レベルのアクションでは、データベース レベルのアクションに対する詳細なフィルタリングは使用できません。 Employee グループのログインの Customers テーブルに対する SELECT アクションの監査などのデータベース レベルの監査では、アクションの詳細なフィルタリングを実装する必要があります。 ユーザーのデータベース監査の仕様に、システム ビューなどのサーバー スコープ オブジェクトは含めないでください。  
  
## <a name="database-level-audit-action-groups"></a>データベース レベルの監査アクション グループ  
 データベース レベルの監査アクション グループは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティ監査イベント クラスに似ています。 イベント クラスの詳細については、「 [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
 データベース レベルの監査アクション グループと、同等の SQL Server イベント クラス (存在する場合) を次の表に示します。  
  
|アクション グループ名|説明|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|このイベントは、アプリケーション ロールのパスワードが変更されるたびに発生します。 [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md)と同じです。|  
|AUDIT_CHANGE_GROUP|このイベントは、任意の監査が作成、変更、または削除されるたびに発生します。 このイベントは、任意の監査の仕様が作成、変更、または削除されるたびに発生します。 監査に対する変更はすべてその監査内で監査されます。 [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md)と同じです。|  
|BACKUP_RESTORE_GROUP|このイベントは、バックアップまたは復元のコマンドが実行されるたびに発生します。 [Audit Backup/Restore イベント クラス](../../event-classes/audit-backup-and-restore-event-class.md)と同じです。|  
|DATABASE_CHANGE_GROUP|このイベントは、データベースが作成、変更、または削除されるときに発生します。 [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md)と同じです。|  
|DATABASE_LOGOUT_GROUP|このイベントは、包含データベースのユーザーがデータベースをログアウトするときに発生します。 [Audit Backup/Restore イベント クラス](../../event-classes/audit-backup-and-restore-event-class.md)と同じです。|  
|DATABASE_OBJECT_ACCESS_GROUP|このイベントは、証明書や非対称キーなどのデータベース オブジェクトへのアクセスが行われるたびに発生します。 [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md)と同じです。|  
|DATABASE_OBJECT_CHANGE_GROUP|このイベントは、スキーマなどのデータベース オブジェクトで、CREATE、ALTER、または DROP ステートメントが実行されたときに発生します。 [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md)と同じです。|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|このイベントは、データベース スコープ内のオブジェクトの所有者が変更されたときに発生します。 [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md)と同じです。|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|このイベントは、アセンブリやスキーマなどのデータベース オブジェクトに対して GRANT、REVOKE、または DENY が実行された場合に発生します。 [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md)と同じです。|  
|DATABASE_OPERATION_GROUP|このイベントは、チェックポイントやクエリ通知のサブスクライブなど、データベースの操作が行われたときに発生します。 [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md)と同じです。|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|このイベントは、ALTER AUTHORIZATION ステートメントを使用してデータベースの所有者を変更した場合に、この動作に必要な権限の確認が行われる際に発生します。 [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md)と同じです。|  
|DATABASE_PERMISSION_CHANGE_GROUP|このイベントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の任意のユーザーによって、ステートメント権限に対して GRANT、REVOKE、または DENY が実行されるたびに、データベースに対する権限の許可などのデータベース限定のイベントに対して発生します。 [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md)と同じです。|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|このイベントは、ユーザーなどのプリンシパルがデータベースで作成、変更、または削除されるときに発生します。 [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md)と同じです。 [Audit Add DB User Event Class](../../event-classes/audit-add-db-user-event-class.md)とも同じです。このイベント クラスは、非推奨の sp_grantdbaccess、sp_revokedbaccess、sp_adduser、および sp_dropuser の各ストアド プロシージャに対して発生します。<br /><br /> このイベントは、非推奨の sp_addrole ストアド プロシージャまたは sp_droprole ストアド プロシージャを使用してデータベース ロールが追加または削除されるたびに発生します。 [Audit Add Role イベント クラス](../../event-classes/audit-add-role-event-class.md)と同じです。|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|このイベントは、EXECUTE AS などのデータベース スコープ内で権限の借用がある場合に発生します。\<ユーザー > や SETUSER です。 [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md)と同じです。|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|このイベントは、データベース ロールにログインが追加または削除されるたびに発生します。 このイベント クラスは、sp_addrolemember、sp_changegroup、および sp_droprolemember の各ストアド プロシージャと共に使用されます。 [Audit Add Member to DB Role イベント クラスs](../../event-classes/audit-add-member-to-db-role-event-class.md)と同じです。|  
|DBCC_GROUP|このイベントは、プリンシパルが任意の DBCC コマンドを実行するたびに発生します。 [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md)と同じです。|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|プリンシパルが包含データベースにログオンしようとして失敗したことを示します。 このクラスのイベントは、新しい接続によって生じることも、接続プールから再利用された接続によって生じることもあります。 このイベントが発生します。|  
|SCHEMA_OBJECT_ACCESS_GROUP|このイベントは、スキーマでオブジェクト権限が使用されるたびに発生します。 [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md)と同じです。|  
|SCHEMA_OBJECT_CHANGE_GROUP|このイベントは、スキーマに対して CREATE、ALTER、または DROP の各操作が実行されたときに発生します。 [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md)と同じです。<br /><br /> このイベントはスキーマ オブジェクトで発生します。 [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md)と同じです。 [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md)とも同じです。|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|このイベントは、スキーマ オブジェクト (テーブル、プロシージャ、関数など) の所有者を変更する権限について確認が行われる際に発生します。 この確認動作は、ALTER AUTHORIZATION ステートメントを使用してオブジェクトに所有者を割り当てたときに行われます。 [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md)と同じです。|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|このイベントは、スキーマ オブジェクトに対して GRANT、DENY、または REVOKE が実行されるたびに発生します。 [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md)と同じです。|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|プリンシパルが包含データベースに正常にログインしたことを示します。 Audit Successful Database Authentication Event Class と同じです。|  
|USER_CHANGE_PASSWORD_GROUP|このイベントは、包含データベースのユーザーのパスワードが USER ALTER ステートメントを使用して変更されるたびに発生します。|  
|USER_DEFINED_AUDIT_GROUP|このグループは、[sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql) の使用によって発生するイベントを監視します。|  
  
## <a name="database-level-audit-actions"></a>データベース レベルの監査アクション  
 データベース レベルのアクションを使用すると、データベース、スキーマ、およびスキーマ オブジェクト (テーブル、ビュー、ストアド プロシージャ、関数、拡張ストアド プロシージャ、キュー、シノニムなど) で特定のアクションを直接監査することができます。 型、XML スキーマ コレクション、データベース、およびスキーマは監査されません。 スキーマ オブジェクトの監査をスキーマおよびデータベースに構成できます。これは、指定したスキーマまたはデータベースに含まれるすべてのスキーマ オブジェクトのイベントが監査されることを意味します。 データベース レベルの監査アクションを次の表に示します。  
  
|操作|説明|  
|------------|-----------------|  
|SELECT|このイベントは、SELECT が実行されるたびに発生します。|  
|UPDATE|このイベントは、UPDATE が実行されるたびに発生します。|  
|INSERT|このイベントは、INSERT が実行されるたびに発生します。|  
|Del|このイベントは、DELETE が実行されるたびに発生します。|  
|EXECUTE|このイベントは、EXECUTE が実行されるたびに発生します。|  
|RECEIVE|このイベントは、RECEIVE が実行されるたびに発生します。|  
|REFERENCES|このイベントは、REFERENCES 権限の確認が行われるたびに発生します。|  
  
### <a name="considerations"></a>考慮事項  
*  データベース レベルの監査アクションは列には適用されません。  
  
*  クエリ プロセッサによってクエリをパラメーター化すると、パラメーターがクエリの列値の代わりに監査イベント ログに表示されます。 
 
*  RPC ステートメントは記録されません。   
  
## <a name="audit-level-audit-action-groups"></a>監査レベルの監査アクション グループ  
 監査プロセス内のアクションを監査することもできます。 この監査は、サーバー スコープで行うことも、データベース スコープで行うこともできます。 データベース スコープでは、データベース監査の仕様についてのみ監査が行われます。 監査レベルの監査アクション グループを次の表に示します。  
  
|アクション グループ名|説明|  
|-----------------------|-----------------|  
|AUDIT_ CHANGE_GROUP|このイベントは、次のいずれかのコマンドが実行されるたびに発生します。<br /><br /> -サーバー監査を作成します。<br />-ALTER SERVER AUDIT<br />-   DROP SERVER AUDIT<br />-サーバー監査の仕様を作成します。<br />-サーバー監査の仕様を変更します。<br />-   DROP SERVER AUDIT SPECIFICATION<br />-データベース監査の仕様を作成します。<br />-   ALTER DATABASE AUDIT SPECIFICATION<br />-   DROP DATABASE AUDIT SPECIFICATION|  
  
## <a name="related-content"></a>関連コンテンツ  
 [サーバー監査およびサーバー監査の仕様を作成する方法](create-a-server-audit-and-server-audit-specification.md)  
  
 [サーバー監査の仕様およびデータベース監査の仕様を作成する方法](create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
