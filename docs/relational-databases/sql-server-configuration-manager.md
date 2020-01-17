---
title: SQL Server 構成マネージャー | Microsoft Docs
description: SQL Server 構成マネージャー クライアントを活用する
ms.custom: ''
ms.date: 12/31/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: vanto
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], managing
- network protocols [SQL Server], managing
- Client Network Utility
- accounts [SQL Server]
- SQL Server Configuration Manager
- Server Network Utility
- accounts [SQL Server], services
- services [SQL Server], managing
- tools [SQL Server], SQL Server Configuration Manager
- configuration manager [SQL Server]
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
author: rothja
ms.author: jroth
ms.openlocfilehash: b447e659b68ced56484296f4763a25e843022b06
ms.sourcegitcommit: ab7209b5856537bfef0a6e9d0527d9002bd0a528
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75608021"
---
# <a name="sql-server-configuration-manager"></a>SQL Server 構成マネージャー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に関連付けられているサービスの管理、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]が使用するネットワーク プロトコルの設定、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クライアント コンピューターからのネットワーク接続の設定を行うためのツールです。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは SQL Server のインストールと共にインストールされます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは、[スタート] メニューから利用できる [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール スナップインであり、他の [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール画面に追加することも可能です。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール (**mmc.exe**) は、**SQLServerManager\<バージョン>.msc** ファイル ([!INCLUDE[ssSQL15](../includes/sssql15-md.md)] の **SQLServerManager13.msc** など) を使用して構成マネージャーを開きます。 特定のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を管理するにはそれに対応するバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーが必要になります。 最新の 5 つのバージョンのパスを次に示します (Windows が C ドライブにインストールされている場合)。  
  
|||  
|-|-|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2019|C:\Windows\SysWOW64\SQLServerManager15.msc| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2017|C:\Windows\SysWOW64\SQLServerManager14.msc|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
|[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
> 
>  -   **Windows 10**:  
>          [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを開くには、 **スタート画面**で、「SQLServerManager13.msc」( [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]の場合) と入力します。 他のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 場合、13 を対応する数値に置き換えます。 SQLServerManager13.msc をクリックすると、構成マネージャーが開きます。 スタート画面やタスク バーに構成マネージャーをピン留めするには、SQLServerManager13.msc を右クリックして、 **[ファイルの場所を開く]** をクリックします。 エクスプローラーでは、SQLServerManager13.msc を右クリックし、 **[スタート画面にピン留め]** または **[タスクバーにピン留め]** をクリックします。  
> -   **Windows 8**:  
>          [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを開くには、**検索**チャームの **[アプリ]** で、「**SQLServerManager\<バージョン>.msc**」(「**SQLServerManager13.msc**」など) と入力し、**Enter** キーを押します。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーと SQL Server Management Studio では、一部のサーバー設定を表示および変更するために、Windows Management Instrumentation (WMI) を使用します。 WMI には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各種ツールによって要求されるレジストリ操作を管理する API 呼び出しに対する統一的なインターフェイスが用意されており、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャー スナップイン コンポーネントの選択された SQL サービスを制御し、操作するための機能も充実しています。 WMI に関連した権限を構成する方法については、「[SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して、他のコンピューター上のサービスの開始、停止、一時停止、再開、構成を行う方法については、「[別のコンピューターへの接続 &#40;SQL Server 構成マネージャー&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md)」を参照してください。  
  
## <a name="managing-services"></a>サービスの管理  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して、サービスの開始、一時停止、再開、停止、サービスのプロパティの表示、変更を行うことができます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用し、起動時のパラメーターを使用して[!INCLUDE[ssDE](../includes/ssde-md.md)]を起動します。  詳細については、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md)」を参照してください。  
  
## <a name="changing-the-accounts-used-by-the-services"></a>サービスが使用するアカウントの変更  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサービスを管理できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサービスまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントのサービスが使用するアカウントやパスワードを変更する場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のツール ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーなど) を必ず使用してください。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーでは、アカウント名の変更だけでなく、その新しいアカウントが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の設定を読み取れるように Windows レジストリ内の権限を設定するなど、付加的な構成も行えます。 Windows サービス コントロール マネージャーなどの他のツールでもアカウント名を変更できますが、関連する設定の変更はできません。 サービスがレジストリ内の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の部分にアクセスできなければ、そのサービスを正しく開始できません。  
  
 もう 1 つのメリットとして、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャー、SMO、WMI のいずれかによって変更したパスワードは、サービスを再起動しなくてもすぐに有効になります。  
  
## <a name="manage-server--client-network-protocols"></a>サーバーとクライアントのネットワーク プロトコルの管理  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーでは、サーバーとクライアントのネットワーク プロトコルや接続オプションを設定できます。 通常は、正しいプロトコルを有効にした後にサーバー ネットワーク接続を変更する必要が生じることはありません。 ただし、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が特定のネットワーク プロトコル、ポート、パイプのいずれかで受信を待機するようにサーバー接続の設定を変更しなければならない場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用してその変更を行えます。 プロトコルを有効にする方法の詳細については、「 [サーバー ネットワーク プロトコルの有効化または無効化](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)」を参照してください。 ファイアウォール経由でプロトコルへのアクセスを有効にする方法については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーでは、サーバーとクライアントのネットワーク プロトコルを管理できます。たとえば、プロトコルの暗号化を強制的に設定する機能、別名のプロパティを表示する機能、プロトコルを有効/無効にする機能などがあります。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーでは、別名の作成と削除や、プロトコルの優先順位の変更を行えます。また、サーバーの別名のプロパティとして、以下のようなプロパティを表示できます。  
  
-   [別名] - クライアントの接続先のコンピューターに使用するサーバーの別名です。  
  
-   [プロトコル] - 構成エントリに使用するネットワーク プロトコルです。  
  
-   [接続パラメーター] - ネットワーク プロトコル構成の接続アドレスに関連したパラメーターです。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーでは、フェールオーバー クラスター インスタンスの情報も表示できます。ただし、一部の操作 (サービスの開始と停止など) については Cluster Administrator を使用する必要があります。  
  
### <a name="available-network-protocols"></a>使用可能なネットワーク プロトコル  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、共有メモリ、TCP/IP、名前付きパイプの各プロトコルをサポートしています。 ネットワーク プロトコルの選択の詳細については、「 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)」を参照してください。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、VIA、Banyan VINES Sequenced Packet Protocol (SPP)、Multiprotocol、AppleTalk、NWLink IPX/SPX の各ネットワーク プロトコルはサポートしていません。 以前にこれらのプロトコルを使用して接続していたクライアントの場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に接続するには別のプロトコルを選択する必要があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーで WinSock プロキシを設定することはできません。 WinSock プロキシの設定については、ISA Server のドキュメントを参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [サービスの管理方法に関するトピック &#40;SQL Server 構成マネージャー&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
  
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
 [SQL Server エージェント サービスの開始、停止、または一時停止](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
 [SQL Server のインスタンスが自動的に開始されるようにする設定 &#40;SQL Server 構成マネージャー&#41;](../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)  
  
 [SQL Server のインスタンスの自動開始の回避 &#40;SQL Server 構成マネージャー&#41;](../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)  
  
  
