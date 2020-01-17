---
title: データベース レベルのロール | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
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
manager: craigg
ms.openlocfilehash: 3df05bddf37970ce0ff0d796bc2b5d93d309b4dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011723"
---
# <a name="database-level-roles"></a>データベース レベルのロール
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、データベースでの権限を簡単に管理できるように、いくつかの *ロール* が用意されています。ロールは、セキュリティ プリンシパルとして他のプリンシパルをグループ化します。 ロールは、 ***Windows オペレーティング システムの*** グループ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に似ています。 データベース レベルのロールは、その権限のスコープがデータベース全体に及びます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]には、データベース レベルのロールが 2 種類あります。1 つはデータベースに事前に定義されている *固定データベース ロール* 、もう 1 つはユーザーが作成できる *可変データベース ロール* です。  
  
 固定データベース ロールはデータベース レベルで定義されており、各データベースに存在します。 **db_owner** データベース ロールのメンバーは、固定データベース ロールのメンバーシップを管理できます。 msdb データベースには、特別な用途の固定データベース ロールもいくつかあります。  
  
 データベース レベルのロールには、すべてのデータベース アカウントとその他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ロールを追加できます。 固定データベース ロールの各メンバーは、そのロールに他のログインを追加できます。  
  
> [!IMPORTANT]  
>  可変データベース ロールは、固定ロールのメンバーとして追加しないでください。 これを行うと、特権が意図せず昇格されることがあります。  
  
 次の表に、固定データベース レベルのロールとその機能を示します。 これらのロールは、すべてのデータベースに存在します。  
  
|データベース レベルのロール名|説明|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 固定データベース ロールのメンバーは、データベースでのすべての構成作業とメンテナンス作業を実行でき、データベースを削除することもできます。|  
|**db_securityadmin**|**db_securityadmin** 固定データベース ロールのメンバーは、ロールのメンバーシップを変更し、権限を管理できます。 このロールにプリンシパルを追加すると、特権が意図せず昇格されることがあります。|  
|**db_accessadmin**|**db_accessadmin** 固定データベース ロールのメンバーは、Windows ログイン、Windows グループ、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインのデータベースに対するアクセスを追加または削除できます。|  
|**db_backupoperator**|**db_backupoperator** 固定データベース ロールのメンバーは、データベースをバックアップできます。|  
|**db_ddladmin**|**db_ddladmin** 固定データベース ロールのメンバーは、すべての DDL (データ定義言語) コマンドをデータベースで実行できます。|  
|**db_datawriter**|**db_datawriter** 固定データベース ロールのメンバーは、すべてのユーザー テーブルのデータを追加、削除、または変更できます。|  
|**db_datareader**|**db_datareader** 固定データベース ロールのメンバーは、すべてのユーザー テーブルからすべてのデータを読み取ることができます。|  
|**db_denydatawriter**|**db_denydatawriter** 固定データベース ロールのメンバーは、データベース内のユーザー テーブルのデータを追加、変更、または削除することはできません。|  
|**db_denydatareader**|**db_denydatareader** 固定データベース ロールのメンバーは、データベース内のユーザー テーブルのデータを読み取ることはできません。|  
  
## <a name="msdb-roles"></a>msdb ロール  
 msdb データベースには、次の表に示す特別な用途のロールが含まれています。  
  
|msdb ロール名|説明|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|これらのデータベース ロールのメンバーは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]を管理および使用できます。 以前のバージョンからアップグレードされた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスには、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] ではなくデータ変換サービス (DTS) を使用して名前が付けられた古いバージョンのロールが含まれている場合があります。 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|これらのデータベース ロールのメンバーは、データ コレクターを管理および使用できます。 詳細については、「 [Data Collection](../../data-collection/data-collection.md)」を参照してください。|  
|**PolicyAdministratorRole**|**PolicyAdministratorRole** データベース ロールのメンバーは、ポリシー ベースの管理のポリシーと条件で、すべての構成作業とメンテナンス作業を実行できます。 詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|これらのデータベース ロールのメンバーは、登録済みサーバーのグループを管理および使用できます。|  
|**dbm_monitor**|作成した、`msdb`データベースのデータベース ミラーリング モニターに最初のデータベースが登録されるとします。 **dbm_monitor** ロールには、メンバーは割り当てられていません。システム管理者がそのロールにユーザーを割り当てる必要があります。|  
  
> [!IMPORTANT]  
>  db_ssisadmin ロールおよび dc_admin ロールのメンバーは、特権を sysadmin に昇格できる可能性があります。 このような特権の昇格が発生するのは、それらのロールが [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージを変更でき、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] エージェントの sysadmin セキュリティ コンテキストを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パッケージを実行できるためです。 メンテナンス プラン、データ コレクション セット、およびその他の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージの実行時にこの特権の昇格を防ぐには、特権が制限されたプロキシ アカウントを使用するようにパッケージを実行する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブを構成するか、db_ssisadmin ロールおよび dc_admin ロールには sysadmin メンバーのみを追加するようにします。  
  
## <a name="working-with-database-level-roles"></a>データベース レベルのロールの操作  
 次の表では、データベース レベルのロールを操作するためのコマンド、ビュー、および関数について説明します。  
  
|機能|型|説明|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|メタデータ|固定データベース ロールの一覧を返します。|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|メタデータ|固定データベース ロールの権限を表示します。|  
|[sp_helprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|メタデータ|現在のデータベース内のロールに関する情報を返します。|  
|[sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|メタデータ|現在のデータベースに含まれるロールのメンバーに関する情報を返します。|  
|[sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|メタデータ|データベース ロールのメンバーごとに 1 行のデータを返します。|  
|[IS_MEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-member-transact-sql)|メタデータ|現在のユーザーが、指定された Microsoft Windows グループまたは Microsoft SQL Server データベース ロールのメンバーであるかどうかを示します。|  
|[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)|コマンド|現在のデータベースに新しいデータベース ロールを作成します。|  
|[ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)|コマンド|データベース ロールの名前を変更します。|  
|[DROP ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-role-transact-sql)|コマンド|データベースからロールを削除します。|  
|[sp_addrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|コマンド|現在のデータベースに新しいデータベース ロールを作成します。|  
|[sp_droprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|コマンド|現在のデータベースからデータベース ロールを削除します。|  
|[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|コマンド|データベース ユーザー、データベース ロール、Windows ログイン、または Windows グループを、現在のデータベースのデータベース ロールに追加します。|  
|[sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|コマンド|現在のデータベースの SQL Server ロールからセキュリティ アカウントを削除します。|  
  
## <a name="public-database-role"></a>public データベース ロール  
 データベース ユーザーはすべて、 **public** データベース ロールに属しています。 セキュリティ保護可能なオブジェクトに対する特定の権限が与えられていないか権限が拒否されているユーザーは、そのオブジェクトに対して **public** に付与されている権限を継承します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [セキュリティ関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [SQL Server の保護](../securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
