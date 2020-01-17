---
title: データベース エンジン サービスの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e747a85c816c8e57757be9acb61b14204266ff35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782053"
---
# <a name="manage-the-database-engine-services"></a>データベース エンジン サービスの管理
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オペレーティング システム上でサービスとして動作します。 サービスとは、システムのバックグラウンドで実行されるアプリケーションの一種です。 通常は、Web サーバー、イベント ログ、ファイル サーバーなど、オペレーティング システムの中核的な機能をサービスによって提供します。 サービスは、コンピューターのデスクトップにユーザー インターフェイスを表示することなく実行できます。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、およびその他のいくつかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントはサービスとして実行されます。 これらのサービスは、オペレーティング システムの起動時に開始されるのが一般的です。 起動時のサービスの状態は、セットアップ中に行った指定に依存します。一部のサービスは既定では開始されません。 ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスの管理について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスにログインする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを開始、停止、一時停止、再開、および再起動する方法を知っておく必要があります。 ログイン後には、サーバーの管理やデータベースに対するクエリなどのタスクを実行することができます。  
  
## <a name="using-the-sql-server-service"></a>SQL Server サービスの使用  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]インスタンスを開始すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスも開始されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを開始すると、ユーザーはサーバーに対する新しい接続を確立できるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始と終了は、ローカルまたはリモートからサービスとして行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは、既定のインスタンスの場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)、名前付きインスタンスの場合は MSSQL$ *\<instancename>* と呼ばれます。  
  
## <a name="using-sql-server-configuration-manager"></a>SQL Server 構成マネージャーの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスを停止、開始、または一時停止できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] サービスを管理することはできません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、選択したサービスのプロパティを参照することもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、MMC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール) スナップインです。 MMC およびスナップインの動作の詳細については、Windows ヘルプを参照してください。  
  
 **SQL Server 構成マネージャーを使用するには**  
  
-   **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
 **Windows 8 を使用して SQL Server 構成マネージャーにアクセスするには**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではありません。そのため、Windows 8.0 を実行している場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、 **検索** チャームで、 **[アプリ]** の下に「 **SQLServerManager12.msc** 」( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]の場合) と入力し ( [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の場合は「 **SQLServerManager11.msc** 」、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の場合は「 **SQLServerManager10.msc** 」と入力し)、 **Enter**キーを押します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|||  
|-|-|  
|[サービスの管理に関するセキュリティ要件](security-requirements-for-managing-services.md)|[SQL Server のインスタンスの自動開始の回避 &#40;SQL Server 構成マネージャー&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[Windows サービス アカウントと権限の構成](configure-windows-service-accounts-and-permissions.md)|[SQL Server のサービス開始アカウントの変更 &#40;SQL Server 構成マネージャー&#41;](scm-services-change-the-service-startup-account.md)|  
|[ネットワークを使用する場合とネットワークを使用しない場合の SQL Server の実行](run-sql-server-with-or-without-a-network.md)|[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](scm-services-configure-server-startup-options.md)|  
|[SQL Server Browser サービス &#40;データベース エンジンと SSAS&#41;](sql-server-browser-service-database-engine-and-ssas.md)|[SQL Server で使用されるアカウントのパスワードの変更 &#40;SQL Server 構成マネージャー&#41;](scm-services-change-the-password-of-the-accounts-used.md)|  
|[データベース エンジン サービスのスタートアップ オプション](database-engine-service-startup-options.md)|[SQL Server エラー ログの構成](scm-services-configure-sql-server-error-logs.md)|  
|[データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](start-stop-pause-resume-restart-sql-server-services.md)|[サーバーの認証モードの変更](change-server-authentication-mode.md)|  
|[シングル ユーザー モードでの SQL Server の起動](start-sql-server-in-single-user-mode.md)|[SQL ライター サービス](sql-writer-service.md)|  
|[最小構成での SQL Server の起動](start-sql-server-with-minimal-configuration.md)|[シャットダウン メッセージのブロードキャスト &#40;コマンド プロンプト&#41;](broadcast-a-shutdown-message-command-prompt.md)|  
|[別のコンピューターへの接続 &#40;SQL Server 構成マネージャー&#41;](scm-services-connect-to-another-computer.md)|[SQL Server インスタンスへのログイン &#40;コマンド プロンプト&#41;](log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[SQL Server のインスタンスが自動的に開始されるようにする設定 &#40;SQL Server 構成マネージャー&#41;](scm-services-set-an-instance-to-start-automatically.md)|[データベース エンジン アクセスのファイル システム権限の構成](configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server エージェントの構成](../../ssms/agent/sql-server-agent.md)  
  
 [SQL Server へのログイン](logging-in-to-sql-server.md)  
  
  
