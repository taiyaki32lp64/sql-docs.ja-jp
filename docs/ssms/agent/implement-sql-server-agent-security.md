---
title: SQL Server エージェントのセキュリティの実装 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8de2fa7123859a6394459a62570ffc86aab37361
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262366"
---
# <a name="implement-sql-server-agent-security"></a>SQL Server エージェントのセキュリティの実装
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用すると、データベース管理者は、各ジョブ ステップをそのジョブ ステップの実行に必要な権限だけがあるセキュリティ コンテキスト内で実行できます。適切なセキュリティ コンテキストは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシによって決まります。 特定のジョブ ステップに対応する権限を設定するには、必要な権限のあるプロキシを作成し、そのプロキシをジョブ ステップに割り当てます。 プロキシは、複数のジョブ ステップに対して指定できます。 同じ権限を必要とするジョブ ステップに対しては、同じプロキシを使用します。  
  
次のセクションでは、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用してジョブを作成または実行するために、許可する必要のあるデータベース ロールについて説明します。  
  
## <a name="granting-access-to-sql-server-agent"></a>SQL Server エージェントへのアクセスの許可  
ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用するには、次の 1 つ以上の固定データベース ロールのメンバーである必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
上記のロールは、 **msdb** データベースに格納されています。 既定では、これらのデータベース ロールのメンバーであるユーザーはいません。 これらのロールのメンバーシップは、明示的に許可する必要があります。 **sysadmin** 固定サーバー ロールのメンバーであるユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントへのフル アクセスが許可されているので、上記の固定データベース ロールのメンバーでなくても [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用できます。 上記のいずれかのデータベース ロールまたは **sysadmin** ロールのメンバーでないユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する際に、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]エージェント ノードを使用できません。  
  
これらのデータベース ロールのメンバーは、自身が所有するジョブの表示および実行に加えて、既存のプロキシ アカウントとして実行するジョブ ステップの作成を行えます。 これらの各ロールに関連付けられている特定の権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
**sysadmin** 固定サーバー ロールのメンバーには、プロキシ アカウントを作成、変更、および削除する権限があります。 **sysadmin** ロールのメンバーには、プロキシを指定せずに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントとして実行するジョブ ステップを作成する権限があります。このアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの起動に使用されるアカウントです。  
  
## <a name="guidelines"></a>ガイドライン  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのセキュリティを向上するには、次のガイドラインに従ってください。  
  
-   プロキシ専用のユーザー アカウントを作成し、ジョブ ステップの実行にはこれらのプロキシ ユーザー アカウントのみを使用します。  
  
-   プロキシ ユーザー アカウントに対し、必要な権限のみを許可します。 特定のプロキシ アカウントに割り当てられたジョブ ステップの実行に実際に求められる権限だけを許可してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスは、Windows **Administrators** グループのメンバーである Microsoft Windows アカウントで実行しないでください。  
  
-   プロキシの安全性は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資格情報ストアと同程度です。  
  
-   ユーザーの書き込み操作で NT イベント ログへの書き込みが可能な場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを介して警告を発行できます。  
  
-   NT Admin アカントを、サービス アカウントまたはプロキシ アカウントとして指定しないでください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、他方の資産にアクセスできます。 この 2 つのサービスは単一の処理領域を共有し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの sysadmin になります。  
  
-   TSX が MSX で参加する場合、MSX の sysadmin が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の TSX インスタンスを完全に制御します。  
  
-   ACE は拡張機能であり、それ自体を呼び出すことはできません。 ACE は Chainer ScenarioEngine.exe (別名 Microsoft.SqlServer.Chainer.Setup.exe) によって呼び出されるか、別のホスト プロセスによって呼び出すことができます。  
  
-   ACE は、SSDP によって所有される次の構成 DLL に依存します。理由は、これらの DLL の API は ACE によって呼び出されるためです。  
  
    -   **SCO**: Microsoft.SqlServer.Configuration.Sco.dll。仮想アカウント用の新しい SCO 検証が含まれます。  
  
    -   **Cluster**: Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC**: Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Extension**: Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>参照  
[定義済みロールの使用](../../reporting-services/security/role-definitions-predefined-roles.md)  
[sp_addrolemember (Transact-SQL)](https://msdn.microsoft.com/a583c087-bdb3-46d2-b9e5-3921b3e6d10b)  
[sp_droprolemember (Transact-SQL)](https://msdn.microsoft.com/c2f19ab1-e742-4d56-ba8e-8ffd40cf4925)  
[セキュリティと保護 (データベース エンジン)](https://msdn.microsoft.com/dfb39d16-722a-4734-94bb-98e61e014ee7)  
  
