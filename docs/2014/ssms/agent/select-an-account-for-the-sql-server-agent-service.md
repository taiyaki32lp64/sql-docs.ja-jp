---
title: SQL Server エージェント サービスのアカウントの選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b2fd7a22c202b1210b17f86903fce32ec8d4b5b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811083"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>SQL Server エージェント サービスのアカウントの選択
  サービス開始アカウントにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] エージェントを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows アカウントとそのネットワーク権限が定義されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、指定されたユーザー アカウントで実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのアカウントを選択します。構成マネージャーでは、次のオプションから選択できます。  
  
-   **[ビルトイン アカウント]** 。 次のビルトイン Windows サービス アカウントの一覧から選択できます。  
  
    -   **[ローカル システム]** アカウント。 このアカウントの名前は NT AUTHORITY\System です。 これは、すべてのローカル システム リソースに無制限にアクセスできる強力なアカウントです。 これは、ローカル コンピューターの Windows **Administrators** グループのメンバーです。つまり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** 固定サーバー ロールのメンバーです。  
  
        > [!IMPORTANT]  
        >  **[ローカル システム アカウント]** オプションは、旧バージョンとの互換性のためだけに用意されています。 ローカル システム アカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが必要としない権限があります。 ローカル システム アカウントとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを実行するのは避けてください。 セキュリティを強化するには、次の「Windows ドメイン アカウントの権限」に示す権限のある Windows ドメイン アカウントを使用します。  
  
-   **[このアカウント]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行する Windows ドメイン アカウントを指定します。 Windows **Administrators** グループのメンバーではない Windows ユーザー アカウントを選択することをお勧めします。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントがローカル **Administrators** グループのメンバーではない場合、マルチサーバー管理の使用には制限があります。 詳細については、後の「サポートされるサービス アカウントの種類」を参照してください。  
  
## <a name="windows-domain-account-permissions"></a>Windows ドメイン アカウントの権限  
 セキュリティを強化するには、 **[このアカウント]** を選択して、Windows ドメイン アカウントを指定します。 指定する Windows ドメイン アカウントは、次の権限を所持している必要があります。  
  
-   すべてのバージョンの Windows で、サービスとしてログオンする権限 (SeServiceLogonRight)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントは、ドメイン コントローラーの Pre-Windows 2000 Compatible Access グループに所属している必要があります。このグループに所属していないと、Windows Administrators グループのメンバー以外のドメイン ユーザーが所有するジョブが失敗します。  
  
-   Windows サーバーでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシをサポートできるように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行しているアカウントに次の権限が必要になります。  
  
    -   スキャン チェックをバイパスする権限 (SeChangeNotifyPrivilege)  
  
    -   プロセス レベル トークンを置き換える権限 (SeAssignPrimaryTokenPrivilege)  
  
    -   プロセスに対してメモリ クォータを調整する権限 (SeIncreaseQuotaPrivilege)  
  
    -   バッチ ログオンの種類を使用してログオンする権限 (SeBatchLogonRight)  
  
> [!NOTE]  
>  アカウントにプロキシのサポートに必要な権限がない場合は、 **sysadmin** 固定サーバー ロールのメンバーのみがジョブを作成できます。  
  
> [!NOTE]  
>  WMI 警告の通知を受信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントに、WMI イベントを含む名前空間、および ALTER ANY EVENT NOTIFICATION に対する権限が許可されている必要があります。  
  
## <a name="sql-server-role-membership"></a>SQL Server ロールのメンバーシップ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行するアカウントは、次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロールのメンバーである必要があります。  
  
-   アカウントは、 **sysadmin** 固定サーバー ロールのメンバーでなければなりません。  
  
-   マルチサーバー ジョブの処理を使用するには、アカウントはマスター サーバーの **msdb** データベースの **TargetServersRole** ロールのメンバーでなければなりません。  
  
## <a name="supported-service-account-types"></a>サポートされるサービス アカウントの種類  
 以下の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスで使用できる Windows アカウントの種類を示します。  
  
|サービス アカウントの種類|非クラスター化サーバー|クラスター化サーバー|ドメインコントローラー (非クラスター化)|  
|--------------------------|---------------------------|----------------------|------------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ドメイン アカウント (Windows Administrators グループのメンバー)|サポートされている|Supported|サポートされている|  
|Windows ドメイン アカウント (管理者以外)|サポート<sup>1</sup>|サポート<sup>1</sup>|サポート<sup>1</sup>|  
|ネットワーク サービス アカウント (NT AUTHORITY\NetworkService)|サポートされている<sup>1、3、4</sup>|サポートされていません|サポートされていません|  
|ローカル ユーザー アカウント (管理者以外)|サポート<sup>1</sup>|サポートされていません|適用なし|  
|ローカル システム アカウント (NT AUTHORITY\System)|サポートされている<sup>2</sup>|サポートされていません|サポートされている<sup>2</sup>|  
|ローカル サービス アカウント (NT AUTHORITY\LocalService)|サポートされていません|サポートされていません|サポートされていません|  
  
 <sup>1</sup>以下の制限事項1を参照してください。  
  
 <sup>2</sup>以下の制限事項2を参照してください。  
  
 <sup>3</sup>以下の制限事項3を参照してください。  
  
 <sup>4</sup>以下の制限事項4を参照してください。  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>制限事項 1: マルチサーバー管理での非管理者アカウントの使用  
 ターゲット サーバーをマスター サーバーに参加させると、次のエラー メッセージが表示されることがあります: "参加操作に失敗しました。"  
  
 このエラーを解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの両方を再起動します。 詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md) 」を参照してください。  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>制限事項 2: マルチサーバー管理でのローカル システム アカウントの使用  
 マルチサーバー管理は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスがローカル システム アカウントで実行されるとき、同じコンピューターにマスター サーバーとターゲット サーバーの両方が存在する場合にのみサポートされます。 この構成を使用している場合に、ターゲット サーバーをマスター サーバーに参加させると、次のメッセージが返されます。  
  
 " *<target_server_computer_name>* のエージェント開始アカウントに対象サーバーとしてのログオン権限があることを確認します"  
  
 情報提供を目的としたこのメッセージは無視できます。 参加操作は、正常に完了します。 詳細については、「 [マルチサーバー環境の作成](create-a-multiserver-environment.md)」を参照してください。  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>制限事項 3: SQL Server ユーザーである場合のネットワーク サービス アカウントの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスをネットワーク サービス アカウントで実行する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーとしてログインするアクセス権がそのネットワーク サービス アカウントに明示的に与えられていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが起動しないことがあります。  
  
 これを解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているコンピューターを再起動します。 これは一度実行するだけで済みます。  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>制限事項 4: SQL Server Reporting Services が同じコンピューターで実行されている場合のネットワーク サービス アカウントの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスをネットワーク サービス アカウントで実行する場合、同じコンピューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] も動作していると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] エージェントが起動しないことがあります。  
  
 これを解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているコンピューターを再起動し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの両方を再起動します。 これは一度実行するだけで済みます。  
  
## <a name="common-tasks"></a>一般的なタスク  
 **SQL Server エージェント サービスの開始アカウントを指定するには**  
  
-   [Set the Service Startup Account for SQL Server Agent &#40;SQL Server Configuration Manager&#41;](set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
 **SQL Server エージェントのメール プロファイルを指定するには**  
  
-   [データベース メールを使用するように SQL Server エージェント メールを構成する](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、オペレーティング システムを起動するときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを開始する必要があることを指定します。  
  
## <a name="see-also"></a>参照  
 [を含めて、すべての](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [サービスの管理方法に関するトピック &#40;SQL Server 構成マネージャー&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)   
 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)  
  
  
