---
title: レプリケーション エージェントのセキュリティ モデル | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bd0cafe74b558dc86f6709b23e2f1195ecada520
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768473"
---
# <a name="replication-agent-security-model"></a>レプリケーション エージェントのセキュリティ モデル
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  レプリケーション エージェントのセキュリティ モデルでは、レプリケーション エージェントの実行や接続に使用されるアカウントをきめ細かく制御できます。異なるアカウントをエージェントごとに指定できます。 アカウントを指定する方法の詳細については、「[ID およびアクセス制御 (レプリケーション)](../../../relational-databases/replication/security/identity-and-access-control-replication.md)」を参照してください。  

エージェントを実行する Windows アカウントがないため、Azure SQL Database マネージド インスタンスのレプリケーション エージェントのセキュリティ モデルは少し異なります。 代わりに、SQL Server 認証を使用してすべての操作を行う必要があります。 
  
> [!IMPORTANT]  
>  **sysadmin** 固定サーバー ロールのメンバーがレプリケーションを構成する際には、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント アカウントの権限を借用するようにレプリケーション エージェントを構成できます。 このとき、レプリケーション エージェントのログインとパスワードを指定する必要はありませんが、その方法はお勧めしません。 セキュリティ上、このトピックの「エージェントに必要な権限」に記載されている最小限の権限を持った各エージェントのアカウントを指定することをお勧めします。  
  
 レプリケーション エージェントは、他の実行可能プログラムと同様に、Windows アカウントのコンテキストで実行されます。 このアカウントを使用して、Windows 統合セキュリティ接続が作成されます。 エージェントを実行するアカウントは、エージェントの開始方法で決まります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブからエージェントを開始する (既定): [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブを使用してレプリケーション エージェントを開始すると、エージェントはレプリケーションを構成するときに指定したアカウントのコンテキストで実行されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントおよびレプリケーションの詳細については、このトピックの「SQL Server エージェントのエージェント セキュリティ」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントを実行するアカウントに必要な権限の詳細については、「[Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)」 (SQL Server エージェントの構成) を参照してください。  
  
-   MS-DOS コマンド ラインから直接、またはスクリプトによってエージェントを開始する: エージェントは、コマンド ラインでエージェントを実行しているユーザーのアカウントのコンテキストで実行されます。  
  
-   レプリケーション管理オブジェクト (RMO) を使用するアプリケーションまたは ActiveX コントロールからエージェントを開始する: エージェントは、RMO を呼び出しているアプリケーションまたは ActiveX コントロールのコンテキストで実行されます。  
  
    > [!NOTE]  
    >  ActiveX コントロールは非推奨とされます。  
  
 Windows 統合セキュリティのコンテキストで接続することをお勧めします。 また、旧バージョンとの互換性のために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティを使用できます。 推奨事項の詳細については、「 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)」を参照してください。  
  
## <a name="permissions-that-are-required-by-agents"></a>エージェントに必要な権限  
 エージェントを実行して接続するアカウントには、さまざまな権限が必要です。 これらの権限を次の表に詳しく示します。 各エージェントは異なる Windows アカウントで実行することをお勧めします。また、このアカウントには、必要な権限のみ許可してください。 複数のエージェントに関連するパブリケーション アクセス リスト (PAL) の詳細については、「[Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md)」 (パブリッシャーのセキュリティ保護) を参照してください。  
  
> [!NOTE]  
>  特定の Windows オペレーティング システム内のユーザー アカウント制御 (UAC) により、スナップショット共有への管理アクセスが妨害される場合があります。 このため、スナップショット エージェント、ディストリビューション エージェント、およびマージ エージェントによって使用される Windows アカウントに、スナップショット共有の権限を明示的に与える必要があります。 この操作は、Windows アカウントが Administrators グループのメンバーである場合にも必要です。 詳細については、「[Secure the Snapshot Folder](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
|エージェント|アクセス許可|  
|-----------|-----------------|  
|スナップショット エージェント|このエージェントを実行する Windows アカウントは、ディストリビューターに接続するときに使用されます。 このアカウントは、次の条件を満たしている必要があります。<br /><br /> \- 最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。<br /><br /> \- スナップショット共有に対する読み取り、書き込み、変更権限がある。<br /><br /> <br /><br /> パブリッシャーへの *接続* に使用されるアカウントは、最低でもパブリケーション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。|  
|ログ リーダー エージェント (Log Reader Agent)|このエージェントを実行する Windows アカウントは、ディストリビューターに接続するときに使用されます。 このアカウントは、最低でもディストリビューション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。<br /><br /> パブリッシャーへの接続に使用されるアカウントは、最低でもパブリケーション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。<br /><br /> **sync_type** オプション *replication support only*、 *initialize with backup*、または *initialize from lsn*を選択した場合、 **sp_addsubscription**の実行後にログ リーダー エージェントを実行して、スクリプトの設定がディストリビューション データベースに書き込まれるようにする必要があります。 ログ リーダー エージェントが、 **sysadmin** 固定サーバー ロールのメンバーであるアカウントで実行されている必要があります。 **sync_type** オプションが *Automatic*に設定されている場合、特別なログ リーダー エージェントの操作は必要ありません。|  
|プッシュ サブスクリプションのディストリビューション エージェント|このエージェントを実行する Windows アカウントは、ディストリビューターに接続するときに使用されます。 このアカウントは、次の条件を満たしている必要があります。<br /><br /> \- 最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。<br /><br /> \- PAL のメンバーである。<br /><br /> \- スナップショット共有に対する読み取り権限を持っている。<br /><br /> \- サブスクリプションが SQL Server 以外のサブスクライバー用の場合、サブスクライバーの OLE DB プロバイダーのインストール ディレクトリに対する読み取り権限を持っている。<br /><br /> \- LOB データをレプリケートする場合、ディストリビューション エージェントにはレプリケーションの **C:\Program Files\Microsoft SQL Server\XX\COMfolder** に対する書き込みアクセス許可が必要です。ここで XX はインスタンス ID を表します。<br /><br /> <br /><br /> \- サブスクライバーへの *接続* に使用されるアカウントは、最低でもサブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。サブスクリプションが SQL Server 以外のサブスクライバー用である場合は、同等の権限を持っている必要があります。<br /><br /> また、ディストリビューション エージェントで `-subscriptionstreams >= 2` を使用する場合は、デッドロックを検出するためにサブスクライバーに対する **View Server State** 権限を与える必要があります。|  
|プル サブスクリプションのディストリビューション エージェント|このエージェントを実行する Windows アカウントは、サブスクライバーに接続するときに使用されます。 このアカウントは、最低でもサブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。 ディストリビューターへの接続に使用されるアカウントは、次の条件を満たしている必要があります。<br /><br /> \- PAL のメンバーである。<br /><br /> \- スナップショット共有に対する読み取り権限を持っている。<br /><br /> \- LOB データをレプリケートする場合、ディストリビューション エージェントにはレプリケーションの **C:\Program Files\Microsoft SQL Server\XX\COMfolder** に対する書き込みアクセス許可が必要です。ここで XX はインスタンス ID を表します。<br /><br /> <br /><br /> ディストリビューション エージェントで `-subscriptionstreams >= 2` を使用する場合は、デッドロックを検出するためにサブスクライバーに対する **View Server State** 権限を与える必要があります。|  
|プッシュ サブスクリプションのマージ エージェント|このエージェントを実行する Windows アカウントは、パブリッシャーおよびディストリビューターに接続するときに使用されます。 このアカウントは、次の条件を満たしている必要があります。<br /><br /> \- 最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。<br /><br /> \- PAL のメンバーである。<br /><br /> \- パブリケーション データベースでの読み取り/書き込みアクセス許可を持つユーザーに関連付けられたログインである。<br /><br /> \- スナップショット共有に対する読み取り権限を持っている。<br /><br /> <br /><br /> サブスクライバーへの *接続* に使用されるアカウントは、最低でもサブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。|  
|プル サブスクリプションのマージ エージェント|このエージェントを実行する Windows アカウントは、サブスクライバーに接続するときに使用されます。 このアカウントは、最低でもサブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。 パブリッシャーおよびディストリビューターへの接続に使用されるアカウントは、次の条件を満たしている必要があります。<br /><br /> \- PAL のメンバーである。<br /><br /> \- パブリケーション データベースでの読み取り/書き込みアクセス許可を持つユーザーに関連付けられたログインである。<br /><br /> \- ディストリビューション データベース内のユーザーに関連付けられたログインである。 **Guest** ユーザーでもかまいません。<br /><br /> \- スナップショット共有に対する読み取り権限を持っている。|  
|キュー リーダー エージェント (Queue Reader Agent)|このエージェントを実行する Windows アカウントは、ディストリビューターに接続するときに使用されます。 このアカウントは、最低でもディストリビューション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。<br /><br /> パブリッシャーへの接続に使用されるアカウントは、最低でもパブリケーション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。<br /><br /> サブスクライバーへの接続に使用されるアカウントは、最低でもサブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。|  
  
## <a name="agent-security-under-sql-server-agent"></a>SQL Server エージェントのエージェント セキュリティ  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] プロシージャ、または RMO を使用してレプリケーションを構成すると、既定では各エージェントの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブが作成されます。 その後エージェントは、連続実行、スケジュールを基にした実行、要求時実行にかかわらず、ジョブ ステップのコンテキストで実行されます。 これらのジョブは、 **の** [ジョブ] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]フォルダーで表示できます。 次の表にジョブ名の一覧を示します。  
  
|エージェント|ジョブ名|  
|-----------|--------------|  
|スナップショット エージェント|**\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<整数>**|  
|マージ パブリケーション パーティションに対するスナップショット エージェント|**Dyn_\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<GUID>**|  
|ログ リーダー エージェント (Log Reader Agent)|**\<パブリッシャー>-\<PublicationDatabase>-\<整数>**|  
|プル サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<SubscriptionDatabase>-\<整数>**|  
|プッシュ サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|  
|プッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|  
|プル サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<SubscriptionDatabase>-\<GUID>**|  
|SQL Server 以外のサブスクライバーへのプッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|  
|キュー リーダー エージェント (Queue Reader Agent)|**[\<ディストリビューター>].\<整数>**|  
  
 \*Oracle パブリケーションに対するプッシュ サブスクリプションの場合は、ジョブ名が **\<>-\<PublicationDatabase>** ではなく **\<>-\<** > になります。  
  
 \*\*Oracle パブリケーションに対するプル サブスクリプションの場合は、ジョブ名が **\<パブリッシャー>-\<PublicationDatabase>** ではなく **\<パブリッシャー>-\<DistributionDatabase**> になります。  
  
 レプリケーションの構成時には、エージェントを実行するアカウントを指定します。 しかし、すべてのジョブ ステップは *プロキシ*のセキュリティ コンテキストで実行されます。そのためレプリケーションでは、指定したエージェント アカウントに対して、以下のマッピングが内部的に実行されます。  
  
-   アカウントは、まず [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](../../../t-sql/statements/create-credential-transact-sql.md) ステートメントを使用して資格情報にマップされます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント プロキシは、資格情報を使用して Windows ユーザー アカウントに関する情報を格納します。  
  
-   [sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) ストアド プロシージャが呼び出され、資格情報を使用してプロキシが作成されます。  
  
> [!NOTE]  
>  この情報は、適切なセキュリティ コンテキストでエージェントを実行する作業についての理解を深めるために提供されています。 作成済みの資格情報またはプロキシは通常、直接操作する必要はありません。  
  
## <a name="see-also"></a>参照  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [レプリケーションのセキュリティ設定の表示および変更](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [スナップショット フォルダーのセキュリティ保護](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
