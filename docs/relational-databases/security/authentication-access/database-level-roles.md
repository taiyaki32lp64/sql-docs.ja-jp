---
title: データベース レベルのロール | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.database.f1
- sql13.swb.roleproperties.object.f1
- SQL13.SWB.DBROLEPROPERTIES.GENERAL.F1
- sql13.swb.roleproperties.general.f1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e91fcd2281082bbef88f0a8387d3ed6cef603d9
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742839"
---
# <a name="database-level-roles"></a>データベース レベルのロール

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、データベースでの権限を簡単に管理できるように、いくつかの *ロール* が用意されています。ロールは、セキュリティ プリンシパルとして他のプリンシパルをグループ化します。 ロールは、 ***Windows オペレーティング システムの*** グループ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に似ています。 データベース レベルのロールは、その権限のスコープがデータベース全体に及びます。  

データベース ロールに対するユーザーの追加および削除を行うには、 `ADD MEMBER` ALTER ROLE `DROP MEMBER` ステートメントの [と](../../../t-sql/statements/alter-role-transact-sql.md) のオプションを使用します。 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] では、 `ALTER ROLE`のこのような使用はサポートされません。 代わりに、以前の [sp_addrolemember](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) と [sp_droprolemember](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) プロシージャを使用してください。
  
 データベース レベルのロールは 2 種類あります。1 つはデータベースに事前に定義されている *固定データベース ロール* 、もう 1 つはユーザーが作成できる *ユーザー定義データベース ロール* です。  
  
 固定データベース ロールはデータベース レベルで定義されており、各データベースに存在します。 **db_owner** データベース ロールのメンバーは、固定データベース ロールのメンバーシップを管理できます。 msdb データベースには、特別な用途のデータベース ロールもいくつかあります。  
  
 データベース レベルのロールには、すべてのデータベース アカウントとその他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ロールを追加できます。
  
> [!TIP]  
>  ユーザー定義データベース ロールは、固定ロールのメンバーとして追加しないでください。 これを行うと、特権が意図せず昇格されることがあります。  

ユーザー定義データベース ロールの権限は、GRANT、DENY、および REVOKE ステートメントを使用してカスタマイズできます。 詳細については、「 [権限 (データベース エンジン)](../../../relational-databases/security/permissions-database-engine.md)」を参照してください。

すべての権限の一覧については、 [データベース エンジンの権限](https://aka.ms/sql-permissions-poster) ポスターを参照してください。 (サーバー レベルの権限をデータベース ロールに付与することはできません。 ログインおよびその他のサーバー レベル プリンシパル (サーバー ロールなど) は、データベース ロールに追加できません。 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]でのサーバー レベル セキュリティでは、代わりに [サーバー ロール](../../../relational-databases/security/authentication-access/server-level-roles.md) を使用します。 サーバー レベルの権限を [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] と [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]のロールを介して付与することはできません。)

## <a name="fixed-database-roles"></a>固定データベース ロール
  
 次の表に、固定データベース ロールとその機能を示します。 これらのロールは、すべてのデータベースに存在します。 **public** データベース ロールを除き、固定データベース ロールに割り当てられている権限を変更することはできません。   
  
|固定データベース ロールの名前|[説明]|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 固定データベース ロールのメンバーは、データベースでのすべての構成作業とメンテナンス作業を実行でき、 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]でデータベースを削除することもできます。 ( [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] と [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]では、一部のメンテナンス作業にサーバー レベルの権限が必要であり、 **db_owners**では実行できません。)|  
|**db_securityadmin**|**db_securityadmin** 固定データベース ロールのメンバーは、カスタム ロールのロール メンバーシップのみの変更、および権限の管理を実行できます。 このロールのメンバーは、特権を昇格させる可能性があり、そのアクションを監視する必要があります。|  
|**db_accessadmin**|**db_accessadmin** 固定データベース ロールのメンバーは、Windows ログイン、Windows グループ、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインのデータベースに対するアクセスを追加または削除できます。|  
|**db_backupoperator**|**db_backupoperator** 固定データベース ロールのメンバーは、データベースをバックアップできます。|  
|**db_ddladmin**|**db_ddladmin** 固定データベース ロールのメンバーは、すべての DDL (データ定義言語) コマンドをデータベースで実行できます。|  
|**db_datawriter**|**db_datawriter** 固定データベース ロールのメンバーは、すべてのユーザー テーブルのデータを追加、削除、または変更できます。|  
|**db_datareader**|**db_datareader** 固定データベース ロールのメンバーは、すべてのユーザー テーブルからすべてのデータを読み取ることができます。|  
|**db_denydatawriter**|**db_denydatawriter** 固定データベース ロールのメンバーは、データベース内のユーザー テーブルのデータを追加、変更、または削除することはできません。|  
|**db_denydatareader**|**db_denydatareader** 固定データベース ロールのメンバーは、データベース内のユーザー テーブルのデータを読み取ることはできません。|  

固定データベース ロールに割り当てられている権限を変更することはできません。 次の図は、固定データベース ロールに割り当てられている権限を示しています。

![fixed_database_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-database-roles.png)

## <a name="special-roles-for-includesssds_mdincludessssds-mdmd-and-includesssdw_mdincludessssdw-mdmd"></a>特別なロール - [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] と [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]

以下のデータベース ロールは、仮想 master データベース内にのみ存在します。 その権限は master で実行されるアクションに制限されます。 これらのロールに追加できるのは、master のデータベース ユーザーのみです。 これらのロールにログインを追加することはできませんが、ログインに基づいてユーザーを作成してから、そのユーザーをロールに追加することはできます。 これらのロールに、master の包含データベース ユーザーを追加することもできます。 ただし、master の **dbmanager** ロールに追加された包含データベース ユーザーを使用して新しいデータベースを作成することはできません。

|ロール名|[説明]|  
|--------------------|-----------------|
|**dbmanager** | データベースの作成と削除を行うことができます。 データベースを作成する dbmanager ロールのメンバーは、そのデータベースの所有者になります。これにより、ユーザーは dbo ユーザーとしてそのデータベースに接続できるようになります。 dbo ユーザーには、データベースでのすべてのデータベース権限があります。 dbmanager ロールのメンバーには、所有していないデータベースへのアクセス権が必ずしもあるとは限りません。|
|**loginmanager** | 仮想 master データベースのログインを作成および削除できます。|

> [!NOTE]
> サーバー レベル プリンシパルと Azure Active Directory 管理者 (構成されている場合) には [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] と [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)] でのすべての権限があり、すべてのロールのメンバーである必要はありません。 詳細については、「[SQL Database の認証と承認:アクセス権の付与](https://azure.microsoft.com/documentation/articles/sql-database-manage-logins/)」を参照してください。 
  
## <a name="msdb-roles"></a>msdb ロール  
 msdb データベースには、次の表に示す特別な用途のロールが含まれています。  
  
|msdb ロール名|[説明]|  
|--------------------|-----------------|  
|**db_ssisadmin**<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|これらのデータベース ロールのメンバーは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]を管理および使用できます。 以前のバージョンからアップグレードされた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスには、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] ではなくデータ変換サービス (DTS) を使用して名前が付けられた古いバージョンのロールが含まれている場合があります。 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。|  
|**dc_admin**<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|これらのデータベース ロールのメンバーは、データ コレクターを管理および使用できます。 詳細については、「 [Data Collection](../../../relational-databases/data-collection/data-collection.md)」を参照してください。|  
|**PolicyAdministratorRole**|**PolicyAdministratorRole** データベース ロールのメンバーは、ポリシー ベースの管理のポリシーと条件で、すべての構成作業とメンテナンス作業を実行できます。 詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|これらのデータベース ロールのメンバーは、登録済みサーバーのグループを管理および使用できます。|  
|**dbm_monitor**|データベース ミラーリング モニターに最初のデータベースが登録されたときに、 **msdb** データベースに作成されます。 **dbm_monitor** ロールには、メンバーは割り当てられていません。システム管理者がそのロールにユーザーを割り当てる必要があります。|  
  
> [!IMPORTANT]  
>  **db_ssisadmin** ロールおよび **dc_admin** ロールのメンバーは、特権を sysadmin に昇格できる可能性があります。 このような特権の昇格が発生するのは、それらのロールが [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージを変更でき、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] エージェントの sysadmin セキュリティ コンテキストを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パッケージを実行できるためです。 メンテナンス プラン、データ コレクション セット、およびその他の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージの実行時にこの特権の昇格を防ぐには、特権が制限されたプロキシ アカウントを使用するようにパッケージを実行する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブを構成するか、 **db_ssisadmin** ロールおよび **dc_admin** ロールには **sysadmin** メンバーのみを追加するようにします。  

## <a name="working-with-r-services"></a>R Services の使用  

**適用対象:** SQL Server ([!INCLUDE[ssSQLv14_md](../../../includes/sssqlv14-md.md)] 以降)   

R Services がインストールされている場合は、パッケージの管理で追加のデータベース ロールを使用できます。 詳細については、 [SQL Server の R パッケージ管理](../../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)に関するページを参照してください。

|ロール名 |[説明]|  
|-------------|-----------------|
|**rpkgs-users** |ユーザーは、rpkgs-shared ロールのメンバーによってインストールされた共有パッケージを使用することができます。|
|**rpkgs-private** |rpkgs-users ロールと同じアクセス許可で共有パッケージにアクセスできます。 このロールのメンバーは、プライベート スコープのパッケージをインストール、削除および使用することもできます。|
|**rpkgs-shared** |rpkgs-private ロールと同じアクセス許可を提供します。 このロールのメンバーであるユーザーは、共有パッケージをインストールまたは削除することもできます。|
  
## <a name="working-with-database-level-roles"></a>データベース レベルのロールの操作  
 次の表では、データベース レベルのロールを操作するためのコマンド、ビュー、および関数について説明します。  
  
|機能|型|[説明]|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)|メタデータ|固定データベース ロールの一覧を返します。|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)|メタデータ|固定データベース ロールの権限を表示します。|  
|[sp_helprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)|メタデータ|現在のデータベース内のロールに関する情報を返します。|  
|[sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)|メタデータ|現在のデータベースに含まれるロールのメンバーに関する情報を返します。|  
|[sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|メタデータ|データベース ロールのメンバーごとに 1 行のデータを返します。|  
|[IS_MEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-member-transact-sql.md)|メタデータ|現在のユーザーが、指定された Microsoft Windows グループまたは Microsoft SQL Server データベース ロールのメンバーであるかどうかを示します。|  
|[CREATE ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md)|コマンド|現在のデータベースに新しいデータベース ロールを作成します。|  
|[ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)|コマンド|データベース ロールの名前またはメンバーシップを変更します。|  
|[DROP ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-role-transact-sql.md)|コマンド|データベースからロールを削除します。|  
|[sp_addrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)|コマンド|現在のデータベースに新しいデータベース ロールを作成します。|  
|[sp_droprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)|コマンド|現在のデータベースからデータベース ロールを削除します。|  
|[sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)|コマンド|データベース ユーザー、データベース ロール、Windows ログイン、または Windows グループを、現在のデータベースのデータベース ロールに追加します。 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 以外のすべてのプラットフォームでは代わりに `ALTER ROLE` を使用する必要があります。|  
|[sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)|コマンド|現在のデータベースの SQL Server ロールからセキュリティ アカウントを削除します。 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 以外のすべてのプラットフォームでは代わりに `ALTER ROLE` を使用する必要があります。|
|[GRANT](../../../t-sql/statements/grant-transact-sql.md)| アクセス許可 | ロールに権限を追加します。
|[DENY](../../../t-sql/statements/deny-transact-sql.md)| アクセス許可 | ロールに対する権限を拒否します。
|[REVOKE](../../../t-sql/statements/revoke-transact-sql.md)| アクセス許可 | 以前に許可または拒否した権限を取り消します。
  
  
## <a name="public-database-role"></a>public データベース ロール  
 データベース ユーザーはすべて、 **public** データベース ロールに属しています。 セキュリティ保護可能なオブジェクトに対する特定の権限が与えられていないか権限が拒否されているユーザーは、そのオブジェクトに対して **public** に付与されている権限を継承します。 データベース ユーザーを **public** ロールから削除することはできません。 
  
## <a name="related-content"></a>関連コンテンツ  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)  
  
 [SQL Server の保護](../../../relational-databases/security/securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)  
  
  
