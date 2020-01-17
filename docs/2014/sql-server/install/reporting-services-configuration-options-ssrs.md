---
title: Reporting Services 構成オプション (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1b54661c47ff40af595be55d444f6c0ffb4bc2cd
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952124"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Reporting Services 構成オプション (SSRS)
  インストール ウィザードの [!INCLUDE[msCoName](../../includes/msconame-md.md)][Reporting Services の構成][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページを使用すると、レポート サーバーのインストール方法および構成方法を指定できます。 インストール オプションを使用できるかどうかは、これより前に **[機能の選択]** ページで選択したオプションや、レポート サーバーのインストール時に [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のローカル インスタンスを一緒にインストールするかどうかによって決まります。  
  
 SSL (Secure Sockets Layer) 証明書がコンピューターにインストールされ、強いワイルドカードにバインドされている場合は、HTTPS プレフィックスを使用して Reporting Services の URL がセットアップで作成されます。 証明書を Reporting Services Url にマップする方法の詳細については、「 [Secure Sockets Layer (SSL) 接続用のレポートサーバーの構成](https://go.microsoft.com/fwlink/?LinkId=199089)(SQL Server オンラインブックでの https://go.microsoft.com/fwlink/?LinkId=199089)」を参照してください。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] およびこのリリースのインストールと構成に関する最新情報については、「[追加のインストール情報](https://go.microsoft.com/fwlink/?LinkId=207425)」 (https://go.microsoft.com/fwlink/?LinkId=207425)を参照してください。  
  
## <a name="options"></a>および  
  
### <a name="reporting-services-native-mode"></a>Reporting Services ネイティブ モード  
 セットアップ時に満たされていない要件があるために既定のレポート サーバーの構成を実行できない場合は、インストール ウィザードで最小限のインストール オプションしか使用できません。この場合、必要なファイルはコピーされますが、セットアップの終了後に Reporting Services の構成マネージャーを使用してネイティブ モードのレポート サーバーを構成する必要があります。  
  
> [!NOTE]  
>  既定のインストール オプションのいずれかを選択した場合、既存のレポート サーバー データベース ファイルによってセットアップが失敗することがあります。 既定のインストール オプションを選択すると、セットアップは既定の名前を使用してレポート サーバー データベースを作成しようとします。 既定の名前のデータベースが既に存在する場合、セットアップは失敗し、インストールのロールバックが必要になります。 この問題を回避するには、セットアップを実行する前に既存のデータベースの名前を変更するか、 **[インストールのみ]** オプションを選択して、セットアップの完了後にデータベースのカスタム設定を指定できるようにします。  
  
#### <a name="install-and-configure"></a>[インストールと構成]  
 レポート サーバー データベース、サービス アカウント、および URL 予約の既定値を使用して、ネイティブ モードのレポート サーバー インスタンスをインストールします。 このオプションを選択した場合は、セットアップが終了するとレポート サーバー インスタンスを使用できるようになります。 ローカル [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを使用してレポート サーバー データベースが作成され、既定値を使用するようにレポート サーバーが構成されます。  
  
 このオプションを使用できるのは、レポート サーバーのインストールで使用される既定値が現在のシステムに対して有効な場合のみです。 このオプションは、開発者がすべてのコンポーネントをローカルにインストールする場合や、ユーザーがソフトウェアを評価する場合に適しています。  
  
 セットアップで使用される既定の設定に関する情報や、既定の構成をインストールできない理由を確認するには、 **[詳細]** をクリックします。 ネイティブモードのレポートサーバーの既定の構成の詳細については、「[ネイティブモードインストールの既定の構成 (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199091) 」 (https://go.microsoft.com/fwlink/?LinkId=199091)を参照してください。  
  
#### <a name="install-only"></a>[インストールのみ]  
 レポート サーバーのプログラム ファイルをインストールし、レポート サーバー サービス アカウントを作成し、レポート サーバーの WMI (Windows Management Instrumentation) プロバイダーを登録します。 このインストール オプションは、"ファイルのみ" のインストールと呼ばれます。 既定の構成を使用しない場合は、このオプションを選択します。 既定の構成をインストールできない場合や、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]フェールオーバー クラスターをインストールする場合は、このオプションしか使用できません。 ファイルのみのインストールの詳細については、「[ファイルのみのインストール (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199093) 」 (https://go.microsoft.com/fwlink/?LinkId=199093)を参照してください。  
  
 セットアップの終了後、レポート サーバーを使用するには、レポート サーバー データベースを作成し、レポート サーバーを構成する必要があります。 レポート サーバーの構成やデータベースの作成には、Reporting Services 構成マネージャーを使用します。 詳細については、「[レポートサーバーデータベースを作成する方法 (Reporting Services 構成)](https://go.microsoft.com/fwlink/?LinkId=199094) 」 (https://go.microsoft.com/fwlink/?LinkId=199094) および「[レポートサーバーデータベース接続の構成](https://go.microsoft.com/fwlink/?LinkId=199095)(https://go.microsoft.com/fwlink/?LinkId=199095))」を参照してください。  
  
### <a name="reporting-services-sharepoint-mode"></a>Reporting Services SharePoint モード  
  
#### <a name="install-only"></a>[インストールのみ]  
 レポート サーバーのプログラム ファイルと PowerShell コマンドレットをインストールします。 インストールが完了したら、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービスを起動し、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成する必要があります。 詳細については、以下を参照してください。  
  
-   [Power View およびデータ警告用の SharePoint モードレポートサーバーのインストール Reporting Services](https://go.microsoft.com/fwlink/?LinkId=207543) (https://go.microsoft.com/fwlink/?LinkId=207543)。  
  
-   [Reporting Services SharePoint モードを単一サーバーファームとしてインストール](https://go.microsoft.com/fwlink/?LinkId=207544)します (https://go.microsoft.com/fwlink/?LinkId=207544)。  
  
-   [Reporting Services レポートサーバー (SSRS)](https://go.microsoft.com/fwlink/?LinkID=207244) (https://go.microsoft.com/fwlink/?LinkID=207244)。  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>SharePoint テクノロジ用 Reporting Services アドインのインストール  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースから、アドインは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの機能の選択ページで SQL Server インストールの一部としてインストールすることができるようになりました。  
  
 ただし、SharePoint 2010 用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインは、次のいずれかの方法を使用してインストールできます。  
  
-   SharePoint 2010 製品準備ツールの **PreRequisiteInstaller.exe**を実行する。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアからインストールします。 **セットアップの終了後、** インストール メディアの Setup フォルダーにある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rsSharePoint.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイルをクリックします。  
  
-   アドインをダウンロードし、インストールします。 詳細については、「 [SharePoint 製品用 Reporting Services アドインの検索場所](https://go.microsoft.com/fwlink/?LinkID=208634)」 (https://go.microsoft.com/fwlink/?LinkID=208634)を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=199096)  の開始  
 [レポートサーバーデータベースの作成 (Reporting Services 構成)](https://go.microsoft.com/fwlink/?LinkId=199094)   
 [Upgrade and Migrate Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)   
 [Reporting Services のコマンド プロンプト インストール (SharePoint モードとネイティブ モード)](https://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
