---
title: Web 同期のセキュリティ アーキテクチャ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web synchronization, security architecture
ms.assetid: 74eee587-d5f5-4d1a-bbae-7f4e3f27e23b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff0c6336bcbd3f9ad8c09f5a25f7317c0d2c4c7b
ms.sourcegitcommit: 655a7217bdf516ce3337691574880619f16de70f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2019
ms.locfileid: "73912809"
---
# <a name="security-architecture-for-web-synchronization"></a>Web 同期のセキュリティ アーキテクチャ
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を使用すると、Web 同期のセキュリティ設定をきめ細かく制御できます。 ここでは、Web 同期の構成に含めることができるすべてのコンポーネントを紹介し、コンポーネント間で行われる接続に関する情報を示します。 [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
 次の図は、考えられるすべての接続を示していますが、特定のトポロジでは要求されない接続もあります。 たとえば、FTP サーバーへの接続は、FTP を使用してスナップショットを配信する場合にのみ必要です。  
  
 ![Web 同期のコンポーネントと接続](../media/websyncarchitecture.gif "Web 同期のコンポーネントと接続")  
  
 次の表では、上記の図に示したコンポーネントと接続について説明します。  
  
## <a name="a-windows-user-under-which-the-merge-agent-runs"></a>A. マージ エージェントを実行する Windows ユーザー  
 同期中、マージ エージェント (A) がサブスクライバーで開始されます。 マージ エージェントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ ステップまたはスタンドアロンのカスタム アプリケーションから開始できます。 マージ エージェントが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ ステップから開始されると、マージ エージェントは指定した Windows ユーザーのコンテキストで実行されます。 Windows ユーザーを指定しないと、マージ エージェントは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントの Windows サービス アカウントのコンテキストで実行されます。  
  
|アカウントの種類|アカウントを指定する場所|  
|---------------------|------------------------------------|  
|Windows ユーザー|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: **\@job_login**および **\@** [job_password のパラメーターです。](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)<br /><br /> レプリケーション管理オブジェクト (RMO): <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>プロパティ|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントの Windows サービス アカウント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャー|  
|スタンドアロンのアプリケーション|マージ エージェントは、アプリケーションを実行している Windows ユーザーのコンテキストで実行されます。|  
  
## <a name="b-connection-to-the-subscriber"></a>b. サブスクライバーへの接続  
 マージ エージェントは、Windows 認証または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用してサブスクライバーに接続します。 指定する Windows ユーザーまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、サブスクリプション データベースの **dbowner** 固定データベース ロールのメンバーであるデータベース ユーザーに関連付けられている必要があります。  
  
> [!NOTE]  
>  マージ エージェントが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブから起動された場合、常に Windows 認証が使用されます。 マージ エージェントがプログラムから起動された場合も、明示的に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が指定されている場合を除いて、Windows 認証が使用されます。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|Windows 認証。|マージ エージェントは、マージ エージェント (A) に指定されている Windows ユーザーのコンテキストで接続します。|  
|次のように指定する場合にのみ、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用します。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **SubscriberSecurityMode**に**0**を指定します。|RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberLogin%2A> と <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberPassword%2A><br /><br /> マージ エージェントのコマンド ライン : **-SubscriberLogin** および **-SubscriberLogin**|  
  
## <a name="c-connection-to-an-outgoing-proxy-server"></a>C. 発信プロキシ サーバーへの接続  
 サブスクライバーの内部ネットワークへのアクセスを制限する発信プロキシ サーバーが存在する場合にのみ、この接続に Windows ユーザーを指定します。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|[Windows 認証]|RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyLogin%2A> 、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyPassword%2A> 、および <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyServer%2A><br /><br /> マージ エージェントのコマンド ライン : **-InternetProxyLogin** 、 **-InternetProxyPassword** 、および **-InternetProxyServer**|  
  
## <a name="d-connection-to-iis"></a>D. IIS への接続  
 サブスクライバーに接続して変更をサブスクリプション データベースから抽出した後、マージ エージェントは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) への HTTPS 要求を作成し、データ変更を XML メッセージとしてアップロードします。 マージ エージェントには、IIS に対するログオンの権限が必要です。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|次のいずれかを指定する場合は、基本認証を使用します。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@internet_security_mode**パラメーターの値が**0**です。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-InternetSecurityMode**の値は**0**です。|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: **\@internet_login**および **\@** [internet_password のパラメーターです。](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetLogin%2A> と <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetPassword%2A><br /><br /> マージ エージェントのコマンド ライン : **-InternetLogin** と **-InternetPassword**|  
|次のいずれかが指定されている場合は、統合認証\* が使用されます。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@internet_security_mode**パラメーターの値**1** 。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-InternetSecurityMode**の値は**1**です。|マージ エージェントは、マージ エージェント (A) に指定されている Windows ユーザーのコンテキストで接続します。|  
  
 \* 統合認証は、すべてのコンピューターが同じドメイン内にある場合、または互いに信頼関係を持つ複数のドメイン内にある場合にのみ使用できます。  
  
> [!NOTE]  
>  統合認証を使用する場合は、委任が必要です。 サブスクライバーから IIS への接続には、基本認証と SSL を使用することをお勧めします。  
  
## <a name="e-connection-to-the-publisher"></a>E. パブリッシャーへの接続  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナーおよびマージ レプリケーション競合回避モジュール コンポーネントは、IIS を実行しているコンピューター上でホストされます。 これらのコンポーネントでは、以下の処理が実行されます。  
  
-   「D. IIS への接続」で説明している HTTPS 要求を取得します。  
  
-   パブリケーション データベースへの SQL 接続を行い、アップロードされた変更をパブリケーション データベースに適用します。  
  
-   ダウンロードされた変更を抽出し、マージ エージェントに HTTPS 応答を返送します。  
  
 マージ レプリケーション競合回避モジュールは、Windows 認証または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証のいずれかを使用してパブリッシャーに接続します。 指定する Windows ユーザーまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、次の条件を満たしている必要があります。  
  
-   パブリケーション アクセス リスト (PAL) に登録されている。 詳細については、「[パブリッシャーのセキュリティ保護](secure-the-publisher.md)」を参照してください。  
  
-   パブリケーション データベースのユーザーに関連付けられている。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|次のいずれかを指定する場合は、Windows 認証を使用します。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@publisher_security_mode**パラメーターの値**1** 。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-PublisherSecurityMode**の値は**1**です。|マージ エージェントは、IIS (D) への接続に指定されている Windows ユーザーのコンテキストでパブリッシャーに接続します。 パブリッシャーと IIS が異なるコンピューター上に存在し、接続 (D) に統合認証を使用する場合は、IIS を実行しているコンピューター上で Kerberos 委任を有効にする必要があります。 詳細については、Windows のマニュアルを参照してください。|  
|以下のいずれかを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用します。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@publisher_security_mode**パラメーターの値が**0**です。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-PublisherSecurityMode**の値は**0**です。|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: **\@publisher_login**および **\@** [publisher_password のパラメーターです。](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A> と <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A><br /><br /> マージ エージェントのコマンド ライン : **-PublisherLogin** と **-PublisherPassword**|  
  
## <a name="f-connection-to-the-distributor"></a>F. ディストリビューターへの接続  
 IIS を実行しているコンピューター上でホストされるマージ レプリケーション競合回避モジュールもディストリビューターに接続します。 マージ レプリケーション競合回避モジュールは、Windows 認証または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証のいずれかを使用してディストリビューターに接続します。 指定する Windows ユーザーまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、次の条件を満たしている必要があります。  
  
-   パブリケーション アクセス リスト (PAL) に登録されている。 詳細については、「[パブリッシャーのセキュリティ保護](secure-the-publisher.md)」を参照してください。  
  
-   ディストリビューション データベースのユーザーに関連付けられている。 `Guest` ユーザーでもかまいません。  
  
 スナップショット共有は、通常、ディストリビューター上に存在します。 スナップショット共有の詳細については、後半の「H. スナップショット共有へのアクセス」を参照してください。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|次のいずれかを指定する場合は、Windows 認証を使用します。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@distributor_security_mode**パラメーターの値**1** 。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-DistributorSecurityMode**の値は**1**です。|マージ エージェントは、IIS (D) への接続に指定されている Windows ユーザーのコンテキストでディストリビューターに接続します。 ディストリビューターと IIS が異なるコンピューター上に存在し、接続 (D) に統合認証を使用する場合は、IIS を実行しているコンピューター上で Kerberos 委任を有効にする必要があります。 詳細については、Windows のマニュアルを参照してください。|  
|以下のいずれかを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用します。<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)の **\@distributor_security_mode**パラメーターの値が**0**です。<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> の値に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A> を指定<br /><br /> マージエージェントコマンドライン: **-DistributorSecurityMode**の値は**0**です。|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: **\@distributor_login**および **\@** [distributor_password のパラメーターです。](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A> と <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A><br /><br /> マージ エージェントのコマンド ライン : **-DistributorLogin** と **-DistributorPassword**|  
  
## <a name="g-connection-to-an-ftp-server"></a>G. FTP サーバーへの接続  
 スナップショットをサブスクライバーに適用する前に、IIS を実行しているコンピューターに、UNC の場所ではなく FTP サーバーからスナップショット ファイルをダウンロードする場合にのみ、この接続に Windows ユーザーを指定します。 詳細については、「[FTP によるスナップショットの転送](../transfer-snapshots-through-ftp.md)」を参照してください。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|[Windows 認証]|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: **\@ftp_login**および **\@** [ftp_password のパラメーターです。](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.Publication.FtpLogin%2A> と <xref:Microsoft.SqlServer.Replication.Publication.FtpPassword%2A>|  
  
## <a name="h-access-to-the-snapshot-share"></a>H. スナップショット共有へのアクセス  
 スナップショット共有には、IIS を実行しているコンピューター上でホストされるマージ レプリケーション競合回避モジュールを使用してアクセスします。  
  
|認証の種類|認証を指定する場所|  
|----------------------------|-------------------------------------------|  
|[Windows 認証]|マージ エージェントは、IIS (D) への接続に指定されている Windows ユーザーのコンテキストでスナップショット共有に接続します。 スナップショット共有と IIS が異なるコンピューター上に存在し、接続 (D) に統合認証を使用する場合は、IIS を実行しているコンピューター上で Kerberos 委任を有効にする必要があります。 詳細については、Windows のマニュアルを参照してください。|  
  
## <a name="i-application-pool-account-for-iis"></a>I. IIS のアプリケーション プール アカウント  
 このアカウントは、 [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)] の場合は IIS を実行しているコンピューター上で W3wp.exe プロセスを開始するために、また、 [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]の場合は Dllhost.exe プロセスを開始するために使用します。 これらのプロセスによって、IIS を実行しているコンピューター上で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナーやマージ レプリケーション競合回避モジュールなどのアプリケーションがホストされます。 このアカウントは、IIS を実行しているコンピューター上にある次のレプリケーション DLL に対して読み取りと実行の権限を持っている必要があります。  
  
-   Replisapi  
  
-   Replrec  
  
-   Replprov  
  
-   Msgprox  
  
-   Xmlsub  
  
 また、このアカウントは IIS_WPG グループの一部である必要があります。 詳細については、「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Web 同期用の IIS の構成[」の「](../configure-iis-for-web-synchronization.md) レプリケーション リスナーの権限の設定」を参照してください。  
  
|アカウントの種類|アカウントを指定する場所|  
|---------------------|------------------------------------|  
|必要な権限を持つ Windows ユーザー|インターネット インフォメーション サービス (IIS) マネージャー。|  
  
## <a name="see-also"></a>参照  
 [Web 同期の構成](../configure-web-synchronization.md)   
 [Replication Merge Agent](../agents/replication-merge-agent.md)  
  
  
