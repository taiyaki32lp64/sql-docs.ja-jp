---
title: PowerPivot for SharePoint 2010 | をインストールします。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4eab56329c2b51f792394ffc37921e8a1ed8e117
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "71952249"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010 をインストールする
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は、SharePoint 2010 ファームでの PowerPivot データ アクセスを提供する中間層のバックエンド サービスのコレクションです。 組織で分析データを格納するブックの作成にクライアント アプリケーション [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 2010 を使用する場合、サーバー環境でそのデータにアクセスするには [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] が必要です。 このトピックでは、基本的なインストール プロセスについて説明し、PowerPivot を構成するために役立つその他のトピックに関する情報も示します。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を同じサーバーにインストールする方法については、「[展開チェックリスト: Reporting Services、Power View、および PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)」を参照してください。  
  
## <a name="prerequisites"></a>Prerequisites  
  
1.  SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
2.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 用に SharePoint Server 2010 Enterprise Edition が必要です。 評価版の Enterprise Edition を使用することもできます。  
  
3.  SharePoint Server 2010 SP2 をインストールする必要があります。 これがないと、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の機能を使用するようにファームを構成できません。  
  
4.  コンピューターがドメインに参加する必要があります。  
  
5.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を準備するには、ドメイン ユーザー アカウントが必要です。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] のインストールでは、Analysis Services サービス アカウントは、サーバーの全体管理から管理できるように、ドメイン ユーザーである必要があります。 アカウントと資格情報は、このドキュメントの手順の一部として、 **[サーバーの構成]** ページで入力します。  
  
6.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] インスタンスの名前を使用できる必要があります。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の名前付きインスタンスが既に存在するコンピューターに、PowerPivot for SharePoint をインストールすることはできません。  
  
7.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] インスタンスは、SQL Server フェールオーバー クラスターに含めることはできません。 SharePoint 製品の高可用性機能を使用します。 たとえば、Excel Services では PowerPivot for SharePoint サーバーの負荷分散が管理されます。 詳細については、「 [Excel Services のデータモデルの設定を管理する (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) 」 (https://technet.microsoft.com/library/jj219780.aspx)を参照してください。  
  
8.  既存のファームに [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールする場合は、クラシック モード認証用に構成されている SharePoint Web アプリケーションが 1 つ以上必要です。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセスは、Web アプリケーションでクラシック モード認証がサポートされている場合にのみ機能します。 クラシックモードの要件の詳細については、「 [PowerPivot の認証と承認](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization)」を参照してください。  
  
9. 次の追加トピックを確認し、システムとバージョンの要件を理解してください。  
  
    -   [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a>手順 1: PowerPivot for SharePoint をインストールする  
 この手順では、SQL Server セットアップを実行して [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールします。 後続の手順では、サーバーをインストール後のタスクとして構成します。  
  
1.  インストールメディアを挿入するか、SQL Server のセットアップファイルが格納されているフォルダーを開き、 **setup.exe**をダブルクリックします。  
  
2.  左側のナビゲーションウィンドウで、 **[インストール]** をクリックします。  
  
3.  **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** をクリックします。  
  
4.  **[プロダクトキー]** ページで、評価版を指定するか、enterprise edition のライセンスコピーのプロダクトキーを入力します。  
  
     **[次へ]** をクリックします。  
  
5.  マイクロソフト ソフトウェア ライセンス条項に同意してください。カスタマー エクスペリエンスおよびエラー レポートもオンにしていただければさいわいです。 **[次へ]** をクリックします。  
  
6.  セットアップ ファイルの更新を求めるメッセージが表示されたら、その指示に従ってください。  
  
7.  **[インストールルール]** ページでは、のインストールを妨げる可能性のある問題が特定されます。 リストを調べて、発生する可能性のある問題がシステムで検出されたかどうかを確認してください。  
  
    > [!NOTE]  
    >  Windows ファイアウォールが有効になっているので、ポートを開いてリモート アクセスを有効にするように求める警告が表示されます。 この警告は、通常、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のインストールには該当しません。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のサービスとデータ ファイルへの接続は、SharePoint サービス間の通信用に既に開かれている SharePoint ポートを使用して確立されます。  
  
     **[次へ]** をクリックします。 SQL Server セットアップ プログラム ファイルがサーバーにインストールされるまで待機します。  
  
8.  **[セットアップ ロール]** ページで、 **[SQL Server PowerPivot for SharePoint]** を選択します。  
  
9. オプションで、データベース エンジンのインスタンスをインストールに追加することができます。 新しいファームを設定し、ファームの構成データベースとコンテンツデータベースを実行するためにデータベースサーバーが必要な場合は、この操作を行うことができます。 データベース エンジンを追加した場合は、PowerPivot 名前付きインスタンスとしてインストールされます。 このインスタンスへの接続を指定する必要がある場合 (たとえば、ファーム構成ウィザードを使用してファームを構成する場合) は、<`servername`> \Powerpivot の形式でデータベース名を入力します。  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. **[次へ]** をクリックします。  
  
11. **[機能の選択]** ページには、インストールされる機能の読み取り専用の一覧が表示されます。 このロールに対してあらかじめ選択されている項目を、追加または削除することはできません。 **[次へ]** をクリックします。  
  
12. **[機能ルール]** ページで、 **[次へ]** をクリックします。 このページはスキップされる場合があります。  
  
13. **[インスタンスの構成]** ページに、"PowerPivot" というインスタンス名が表示されます。この名前は情報として示されており、読み取り専用になっています。 **POWERPIVOT**のこのインスタンス名は**必須であり、変更することはできません**。 ただし、ディレクトリ名とレジストリ キーをわかりやすく示した独自のインスタンス ID を入力することができます。 **[次へ]** をクリックします。  
  
14. **[サーバーの構成]** ページで、必要なアカウント情報を入力します。  
  
     SQL Server Analysis Services については、ドメイン ユーザー アカウントを指定する必要があります。 ビルトイン アカウントを指定しないでください。 ドメインアカウントは、SharePoint サーバーの全体管理で*管理アカウント*として Analysis Services サービスアカウントを管理するために必要です。  
  
     ![SSAS サーバーの構成](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS サーバーの構成")  
  
     SQL Server データベース エンジンと SQL Server エージェントを追加した場合は、サービスがドメイン ユーザー アカウントまたは既定の仮想アカウントで実行されるように構成できます。  
  
     サービスを提供するために、自分のドメイン ユーザー アカウントを使用しないでください。 このようなアカウントを使用すると、ネットワークのリソースに対して持っている権限と同じ権限をサーバーに付与することになります。 悪意のあるユーザーがサーバーに侵入した場合、そのユーザーは管理者のドメイン資格情報でログインし、管理者と同じデータやアプリケーションをダウンロードしたり使用したりできるようになります。  
  
15. **[次へ]** をクリックします。  
  
16. データベース エンジンをインストールする場合は、[データベース エンジンの構成] ページが表示されます。 データベースエンジンの構成 で、**現在のユーザーの追加** をクリックして、データベースエンジンインスタンスに対する管理者権限をユーザーアカウントに付与します。 **[追加]** をクリックして、他のアカウントを追加します。 **[次へ]** をクリックします。  
  
17. **[Analysis Services の構成]** ページで、 **[現在のユーザーの追加]** をクリックして、ユーザー アカウントに管理権限を付与します。 セットアップの完了後にサーバーを構成するには、管理権限が必要になります。  
  
18. 同じページで、管理者権限も必要なユーザーの Windows ユーザーアカウントを追加します。 たとえば、データベースの接続に関する問題のトラブルシューティングを行ったりバージョン情報を取得したりするために、SQL Server Management Studio で [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスに接続するユーザーには、サーバーに対するシステム管理者権限が必要です。 サーバーのトラブルシューティングや管理を担当する可能性があるユーザーのユーザー アカウントをここで追加しておきます。  
  
19. **[次へ]** をクリックします。  
  
20. 残りの各ページで、インストールの準備完了 ページが表示されるまで **次へ** をクリックします。  
  
21. **[インストール]** をクリックします。  
  
> [!TIP]  
>  SQL Server インストールの問題を解決する必要がある場合は、「 [SQL Server セットアップログファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
##  <a name="bkmk_config"></a>手順 2: サーバーを構成する  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] データベース サーバーを使用する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または SharePoint ファームを構成する前に、SharePoint 2010 SP2 をインストールする必要があります。 サービス パックをインストールしていない場合は、サーバーの構成を始める前にここでインストールしてください。  
  
 サーバーが構成されるまでは、インストールは完了しません。 このリリースでは、サーバーの構成は、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツール、サーバーの全体管理、PowerShell のいずれかの方法を使用して、常にインストール後のタスクとして実行されます。 続行するには、次のいずれかのアプローチを使用します。  
  
-   [PowerPivot for SharePoint 2010 &#40;PowerPivot 構成ツールの構成または修復&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [サーバーの全体管理での PowerPivot サーバーの管理と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
-   [Windows PowerShell を使用した PowerPivot の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
 **データベースエンジンインスタンスに接続しています。** [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールしたときに、SQL Server セットアップで、データベース エンジンのインスタンスをインストールに追加することができました。 新しいファームを設定し、ファームの構成データベースとコンテンツデータベースを実行するためにデータベースサーバーが必要な場合は、データベースエンジンインスタンスをインストールに追加した可能性があります。 データベース エンジンを追加した場合は、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の名前付きインスタンスとしてインストールされています。 このインスタンスへの接続を指定する必要がある場合 (たとえば、ファーム構成ウィザードを使用してファームを構成する場合)、必ずデータベース名を次の形式で入力してください: <`servername`> \Powerpivot  
  
##  <a name="bkmk_redist"></a>手順 3: Excel Services アプリケーションサーバーに Analysis Services OLE DB プロバイダーをインストールする  
 個々のアプリケーション サーバーで Excel Calculation Services と [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] を実行する場合は、追加のインストール手順が必要となります。 Excel Calculation Services を実行しているアプリケーション サーバーに、適切なバージョンの Analysis Services OLE DB (MSOLAP) プロバイダーをインストールします。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの MSOLAP は SQL Server セットアップに含まれているため、アプリケーション サーバーが PowerPivot アプリケーション サーバーではない場合にのみ、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの MSOLAP を明示的にインストールする必要があります。  
  
    > [!NOTE]  
    >  Excel Calculation Services アプリケーションサーバーには、グローバルアセンブリ内の**microsoft.analysisservices.sharepoint.integration.dll**ファイルのインスタンスも必要です。 アプリケーション サーバーに .dll をインストールするには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] をインストールします。 SQL Server セットアップウィザードの **機能の選択** ページで、管理ツール-完全 を選択します。  
  
-   アプリケーション サーバーで古い [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックをサポートする必要がある場合は、SQL Server 2008 R2 バージョンの MSOLAP をインストールする必要があります。  
  
 検証手順を含め、プロバイダーのインストールの詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB Provider のインストール](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
##  <a name="bkmk_verify"></a>手順 4: インストールを確認する  
 この最後の手順では、SharePoint 2010 と [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] の両方が完全に機能することを確認します。 手順については、「 [PowerPivot for SharePoint のインストールの検証](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [PowerPivot for SharePoint 2010 インストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [展開チェックリスト: Reporting Services、Power View、PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [配置チェックリスト: SharePoint 2010 ファームへの PowerPivot サーバーの追加によるスケールアウト](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [展開チェックリスト: PowerPivot for SharePoint 2010 のマルチサーバーインストール](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  
