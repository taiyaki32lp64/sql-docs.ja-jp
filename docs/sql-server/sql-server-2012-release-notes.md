---
title: SQL Server 2012 リリース ノート | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 02/01/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Release Notes, SQL Server
ms.assetid: 9ccb390a-67a9-4593-85ea-2b4c41c4620f
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 3a6592781464bb148bf31fdaa135d17a159b5e13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136529"
---
# <a name="sql-server-2012-release-notes"></a>SQL Server 2012 リリース ノートします。
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
このリリース ノートでは、SQL Server 2012 について、インストールやトラブルシューティングを行う前に知っておく必要がある、既知の問題について説明しています ([SQL Server 2012 をダウンロードするにはここをクリックしてください](https://go.microsoft.com/fwlink/?LinkId=238647))。 このリリース ノートは、オンラインのみで入手でき、インストール メディアには含まれていません。また、定期的に更新されます。  
  
SQL Server 2012 の開始方法およびインストール方法の詳細については、SQL Server 2012 の Readme をご覧ください。 Readme ドキュメントは、インストール メディアまたは [Readme](https://download.microsoft.com/download/3/B/D/3BD9DD65-D3E3-43C3-BB50-0ED850A82AD5/ENU/Readme.htm) ダウンロード ページから入手できます。 「 [SQL Server オンライン ブック](https://go.microsoft.com/fwlink/?LinkId=190948) 」または [SQL Server フォーラム](https://go.microsoft.com/fwlink/?LinkId=213599)でも詳細な情報を参照することができます。  
  
## <a name="Install"></a>1.0 インストールの準備  
[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]をインストールする前に、次のことを考慮してください。  
  
### <a name="11-rules-documentation-for-sql-server-2012-setup"></a>1.1 SQL Server 2012 セットアップのルール ドキュメント  
**問題点:** SQL Server セットアップによって、セットアップ操作が完了する前にコンピューターの構成が検証されます。 SQL Server のセットアップ処理中にはさまざまなルールが適用され、システム構成チェッカー (SCC) レポートによって記録されます。 このセットアップ ルールに関するドキュメントは、MSDN ライブラリで提供されなくなりました。  
  
**回避策:** システム構成チェック レポートを参照することで、このセットアップ ルールの詳細を調べることができます。 システム構成チェッカーは、実行された各ルールの簡単な記述と、実行ステータスを含むレポートを生成します。 システム構成チェッカーのレポートは %programfiles%\Microsoft SQL Server\110\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\ に配置されます。  
  
### <a name="12-adding-a-local-user-account-for-the-distributed-replay-controller-service-might-terminate-setup-unexpectedly"></a>1.2 分散再生コントローラー サービスのローカル ユーザー アカウントを追加すると、セットアップが予期せず終了する  
**問題点:** SQL Server セットアップの **[分散再生コントローラー]** ページで、分散再生コントローラー サービスのローカル ユーザー アカウントを追加しようとすると、"SQL Server のセットアップに失敗しました" エラー メッセージが表示され、セットアップが予期せず終了します。  
  
**回避策:** SQL のセットアップ中、[現在のユーザーの追加] または [追加] を使用して、ローカル ユーザー アカウントを追加しないでください。 セットアップ後、以下の手順に従って、手作業でローカル ユーザー アカウントを追加してください。  
  
1.  SQL Server 分散再生コントローラー サービスを停止します。  
  
2.  コントローラー サービスがインストールされているコントローラー コンピューターで、コマンド プロンプトから、「dcomcnfg」と入力します。  
  
3.  [コンポーネント サービス] ウィンドウで、 **[コンソール ルート]**  ->  **[コンポーネント サービス]**  ->  **[コンピューター]**  ->  **[マイ コンピューター]**  ->  **[Dconfig]**  -> **[DReplayController]** の順に移動します。  
  
4.  **[DReplayController]** を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[DReplayController のプロパティ]** ウィンドウの **[セキュリティ]** タブで、 **[起動とアクティブ化のアクセス許可]** セクションの **[編集]** をクリックします。  
  
6.  ローカル ユーザー アカウントに **ローカルとリモートからのアクティブ化** のアクセス許可を付与し、 **[OK]** をクリックします。  
  
7.  [アクセス許可] セクションの **[編集]** をクリックし、 **ローカル ユーザー アカウントにローカルとリモートのアクセス** 権限を付与して、 **[OK]** をクリックします。  
  
8.  **[OK]** をクリックして、 **[DReplayController のプロパティ]** ウィンドウを閉じます。  
  
9. コントローラー コンピューターで、ローカル ユーザー アカウントを **Distributed COM Users** グループに追加します。  
  
10. SQL Server 分散再生コントローラー サービスを開始します。  
  
### <a name="13-sql-server-setup-might-fail-while-trying-to-start-the-sql-server-browser-service"></a>1.3 SQL Server Browser サービスを開始しようとすると、SQL Server セットアップが失敗する場合がある  
**問題点:** SQL Server Browser サービスを開始しようとすると、次のようなエラーが表示され、SQL Server のセットアップが失敗する場合があります。  
  
<pre>The following error has occurred:  
Service 'SQLBrowser' start request failed. Click 'Retry' to retry the failed action, or click 'Cancel' to cancel this action and continue setup.</pre>  
  
内の複数の  
  
<pre>The following error has occurred:  
SQL Server Browser configuration for feature 'SQL_Browser_Redist_SqlBrowser_Cpu32' was cancelled by user after a previous installation failure. The last attempted step: Starting the SQL Server Browser service 'SQLBrowser', and waiting for up to '900' seconds for the process to complete.</pre>  
  
**回避策:** このエラーは、SQL Server エンジンまたは Analysis Services のインストールに失敗したとき発生する場合があります。 この問題を解決するには、SQL Server セットアップ ログを参照して、SQL Server エンジンと Analysis Services のエラーをトラブルシューティングします。 詳細については、「SQL Server セットアップ ログ ファイルの表示と読み取り」をご覧ください。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
### <a name="14-sql-server-2008-2008-r2-analysis-services-failover-cluster-upgrade-to-sql-server-2012-might-fail-after-renaming-the-network-name"></a>1.4 SQL Server 2008 または 2008 R2 の Analysis Services フェールオーバー クラスターのネットワーク名の変更後に SQL Server 2012 へのアップグレードが失敗する場合がある  
**問題点:** Windows クラスター アドミニストレーター ツールを使用して Microsoft SQL Server 2008 または 2008 R2 の Analysis Services フェールオーバー クラスターの名前を変更した後でアップグレードを実行すると、処理が失敗する場合があります。  
  
**回避策:** この問題を解決するには、[このサポート技術情報の資料](https://support.microsoft.com/kb/955784)の「解決策」に記載されている指示に従って、ClusterName レジストリ エントリを更新してください。  
  
### <a name="15-installing-sql-server-2012-on-windows-server-2008-r2-server-core-service-pack-1"></a>1.5 Windows Server 2008 R2 Server Core Service Pack 1 での SQL Server 2012 のインストール  
SQL Server を Windows Server 2008 R2 Server Core SP1 にインストールすることができますが、以下の制限があります。  
  
-   Microsoft SQL Server 2012 では、Server Core オペレーティング システムでのインストール ウィザードを使用したセットアップはサポートされていません。 Server Core にインストールする場合、SQL Server セットアップでは、/Q パラメーターを使用した非表示モード、または /QS パラメーターを使用した簡易非表示モードがサポートされます。  
  
-   以前のバージョンの SQL Server から Microsoft SQL Server 2012 へのアップグレードは、Windows Server 2008 R2 Server Core SP1 を実行しているコンピューターではサポートされていません。  
  
-   Windows Server 2008 R2 Server Core SP1 を実行しているコンピューターでは、Microsoft SQL Server 2012 エディションの 32 ビット バージョンのインストールがサポートされていません。  
  
-   Microsoft SQL Server 2012 は、Windows Server 2008 R2 Server Core SP1 を搭載するコンピューターに、以前のバージョンの SQL Server とサイド バイ サイドでインストールすることはできません。  
  
-   SQL Server 2012 の一部の機能は、Server Core オペレーティング システムではサポートされません。 サポートされる機能と Server Core への SQL Server 2012 のインストールの詳細については、「 [Server Core への SQL Server 2012 のインストール](https://msdn.microsoft.com/library/hh231669(SQL.110).aspx)」をご覧ください。  
  
### <a name="16-semantic-search-requires-you-to-install-an-additional-dependency"></a>1.6 セマンティック検索を使用するには、依存する追加項目のインストールが必要になる  
**問題点:** 統計的セマンティック検索には、追加の前提条件として、セマンティック言語統計データベースが必要です。これは、SQL Server セットアップ プログラムでインストールされません。  
  
**回避策:** セマンティック インデックスの作成の前提条件として、セマンティック言語統計データベースをセットアップするには、次のタスクを実行してください。  
  
1.  SQL Server インストール メディアにある SemanticLanguageDatabase.msi という名前の Windows インストーラー パッケージを実行して、データベースを抽出します。 SQL Server 2012 Express の場合は、セマンティック言語統計データベースを [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=35582) (https://www.microsoft.com/download/details.aspx?id=35582) ) からダウンロードした後、Windows インストーラー パッケージを実行してください。  
  
2.  適切なデータ フォルダーにデータベースを移動します。 データベースを既定の場所に残しておく場合、正しくアタッチするには、権限を変更する必要があります。  
  
3.  抽出したデータベースをアタッチします。  
  
4.  ストアド プロシージャ **sp_fulltext_semantic_register_language_statistics_db** を呼び出し、データベースのアタッチ時に指定した名前を使用して、データベースを登録します。  
  
上記のタスクが完了していない場合に、セマンティック インデックスを作成しようとすると、次のようなメッセージが表示されます。  
  
<pre>Msg 41209, Level 16, State 3, Line 1  
A semantic language statistics database is not registered. Full-text indexes using 'STATISTICAL_SEMANTICS' cannot be created or populated.</pre>  
  
### <a name="17-installation-prerequisite-handling-during-sql-server-2012-setup"></a>1.7 SQL Server 2012 のセットアップ時のインストール前提条件の扱い  
ここでは、SQL Server 2012 セットアップ時のインストール前提条件の扱いについて説明します。  
  
-   SQL Server 2012 のインストールは、Windows 7 SP1 および Windows Server 2008 R2 SP1 でのみサポートされています。 ただし、Windows 7 または Windows Server 2008 R2 で SQL Server 2012 をインストールしても、セットアップはブロックされません。  
  
-   .NET Framework 3.5 SP1 は、SQL Server 2012 のデータベース エンジン、レプリケーション、マスター データ サービス、Reporting Services、Data Quality Services (DQS)、または SQL Server Management Studio を選択する場合に必要ですが、SQL Server セットアップではインストールされなくなりました。  
  
    -   Windows Vista SP2 または Windows Server 2008 SP2 オペレーティング システムを使用しているコンピューターでセットアップを実行する場合に、.NET Framework 3.5 SP1 がインストールされていなければ、SQL Server セットアップでインストールを続行する前に .NET Framework 3.5 SP1 をダウンロードしてインストールするよう要求されます。 .NET Framework 3.5 SP1 は、Windows Update または [ここ](https://www.microsoft.com/download/details.aspx?id=25150)から直接ダウンロードできます。 SQL Server セットアップが中断されないようにするには、SQL Server セットアップを実行する前に .NET Framework 3.5 SP1 をダウンロードしてインストールします。  
  
    -   Windows 7 SP1 または Windows Server 2008 R2 SP1 のオペレーティング システムを使用しているコンピューターでセットアップを実行する場合、SQL Server 2012 をインストールする前に .NET Framework 3.5 SP1 を有効にする必要があります。  
  
        **Windows Server 2008 R2 SP1 で .NET Framework 3.5 SP1 を有効にするには、次のいずれかの方法を使用します。**  
  
        方法 1:サーバー マネージャーの使用  
  
        1.  サーバー マネージャーで **[機能の追加]** をクリックし、使用できる機能の一覧を表示します。  
  
        2.  **[機能の選択]** インターフェイスで、 **[.NET Framework 3.5.1 の機能]** を展開します。  
  
        3.  **[.NET Framework 3.5.1 の機能]** を展開すると、2 つのチェック ボックスが表示されます。 1 つは .NET Framework 3.5.1 用で、もう 1 つは WCF アクティブ化用です。 **.NET Framework 3.5.1**のチェック ボックスをオンにし、 **[次へ]** をクリックします。 .NET Framework 3.5.1 の機能をインストールする前に、必要な役割サービスと機能もインストールする必要があります。  
  
        4.  **[インストール オプションの確認]** で、選択内容を確認して、[インストール] をクリックします。  
  
        5.  インストール プロセスを完了して、 **[閉じる]** をクリックします。  
  
        方法 2:Windows PowerShell の使用  
  
        1.  **[スタート]**  |  **[すべてのプログラム]**  |  **[アクセサリ]** の順にクリックします。  
  
        2.  **[Windows PowerShell]** を展開し、 **[Windows PowerShell]** を右クリックして、 **[管理者として実行]** をクリックします。 **[ユーザー アカウント制御]** ボックスで **[はい]** をクリックします。  
  
        3.  PowerShell コマンド プロンプトで次のコマンドを入力し、各コマンドの後に Enter キーを押します。  
  
            ```  
            Import-Module ServerManager  
            Add-WindowsFeature as-net-framework  
            ```  
  
        **Windows 7 SP1 で .NET Framework 3.5 SP1 を有効にするには、次の方法を使用します。**  
  
        1.  **[スタート]** ボタンをクリックし、 |  **[コントロール パネル]**  |  **[プログラム]** 、 **[Windows の機能の有効化または無効化]** の順にクリックします。 管理者のパスワードの入力または確認入力を求めるメッセージが表示されたら、パスワードを入力するか、確認入力を行います。  
  
        2.  **Microsoft .NET Framework 3.5.1**を有効にするには、この機能の横にあるチェック ボックスをオンにします。 Windows の機能を無効化するには、チェック ボックスをオフにします。  
  
        3.  **[OK]** をクリックします。  
  
        **展開イメージのサービスと管理 (DISM.exe) を使用して .NET Framework 3.5 SP1 を有効にするには、次の方法を使用します。**  
  
        展開イメージのサービスと管理 (DISM.exe) を使用して .NET Framework 3.5 SP1 を有効にすることもできます。 Windows の機能をオンラインで有効にする方法の詳細については、「 [Windows の機能をオンラインで有効または無効にする](https://technet.microsoft.com/library/dd744582(WS.10).aspx)」をご覧ください。 次に、.NET Framework 3.5 SP1 を有効にする手順を説明します。  
  
        1.  コマンド プロンプトで次のコマンドを入力すると、オペレーティング システムで使用できるすべての機能の一覧が表示されます。  
  
            ```  
            sm /online /Get-Features  
            ```  
  
        2.  省略可能:コマンド プロンプトで次のコマンドを入力すると、目的の機能に関する情報が表示されます。  
  
            ```  
            Dism /online /Get-FeatureInfo /FeatureName:NetFx3  
            ```  
  
        3.  Microsoft .NET Framework 3.5.1 を有効にするには、次のコマンドを入力します。  
  
            ```  
            Dism /online /Enable-Feature /FeatureName:NetFx3  
            ```  
  
-   SQL Server 2012 には .NET Framework 4 が必要です。 SQL Server セットアップでは、機能のインストール手順で .NET Framework 4 がインストールされます。  
  
    SQL Server 2012 Express を Windows 2008 R2 SP1 Server Core オペレーティング システムにインストールする場合は .NET Framework 4 がインストールされません。 SQL Server 2012 Express (データベースのみ) をインストールする場合、.NET Framework 3.5 SP1 があれば、.NET Framework 4 は不要です。 .NET Framework 3.5 SP1 がない場合、または SQL Server 2012 Management Studio Express、SQL Server 2012 Express with Tools、SQL Server 2012 Express with Advanced Services のいずれかをインストールする場合は、Windows Server 2008 R2 SP1 Server Core オペレーティング システムに SQL Server2012 Express をインストールする前に、.NET Framework 4 をインストールする必要があります。  
  
-   Visual Studio コンポーネントを適切にインストールできる状態にするために、SQL Server は更新プログラムのインストールを要求します。 SQL Server セットアップは、更新プログラムが存在するかどうかを確認した後、SQL Server のインストールを続行する前に更新プログラムをダウンロードしてインストールするよう要求します。 SQL Server セットアップが中断されないようにするには、SQL Server セットアップを実行する前に、以下の説明に従って更新プログラムをダウンロードしてインストールします (または、Windows Update に用意されている .NET Framework 3.5 SP1 の更新プログラムをすべてインストールします)。  
  
    -   Windows Vista SP2 または Windows Server 2008 SP2 のオペレーティング システムを使用しているコンピューターに SQL Server 2012 をインストールする場合、必要な更新プログラムは [ここ](https://support.microsoft.com/?kbid=956250)から入手できます。  
  
    -   Windows 7 SP1 または Windows Server 2008 R2 SP1 オペレーティング システムを使用しているコンピューターに SQL Server 2012 をインストールする場合、更新プログラムは既にコンピューターにインストールされています。  
  
-   Windows PowerShell 2.0 は SQL Server 2012 のデータベース エンジン コンポーネントおよび SQL Server Management Studio のインストール前提条件ですが、Windows PowerShell は SQL Server セットアップでインストールされなくなりました。 PowerShell 2.0 がコンピューターで表示されない場合は、「 [Windows 管理フレームワーク](https://support.microsoft.com/kb/968929) 」の手順に従って有効にすることができます。 Windows PowerShell 2.0 をインストールする方法は、使用するオペレーティング システムによって異なります。  
  
    -   Windows Server 2008 - Windows PowerShell 1.0 は機能のため、追加することができます。 Windows PowerShell 2.0 はダウンロードしてインストールすることができます (実際には OS 修正プログラムとして適用されます)。  
  
    -   Windows 7/Windows Server 2008 R2 - Windows PowerShell 2.0 が既定でインストールされています。  
  
-   SQL Server 2012 の機能を SharePoint 環境で使用する場合は、SharePoint Server 2010 Service Pack 1 (SP1) と SharePoint の累積的な更新プログラム (2011 年 8 月) が必要です。 SQL Server 2012 の機能をファームに追加する前に、SP1 と SharePoint の [累積的な更新プログラム (2011 年 8 月)](https://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)をインストールし、サーバー ファームに修正プログラムを完全に適用しておく必要があります。 SQL Server 2012 の機能を使用して、データベース エンジンのインスタンスをファームのデータベース サーバーとして使用する場合、PowerPivot for SharePoint を構成する場合、または Reporting Services を SharePoint モードで配置する場合に、この要件が該当します。  
  
### <a name="18-supported-operating-systems-for-sql-server-2012"></a>1.8 SQL Server 2012 でサポートされているオペテーティング システム  
SQL Server 2012 は、Windows Vista SP2、Windows Server 2008 SP2、Windows 2008 R2 SP1、および Windows 7 SP1 の各オペレーティング システムでサポートされています。  
  
### <a name="19-sync-framework-is-not-included-in-the-installation-package"></a>1.9 Sync Framework がインストール パッケージに含まれていない  
**問題点:** Sync Framework は SQL Server 2012 のインストール パッケージには含まれていません。  
  
**回避策:** Sync Framework の適切なバージョンは、[この Microsoft ダウンロード センター ページ](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=23217)からダウンロードしてインストールできます。  
  
### <a name="110-if-visual-studio-2010-service-pack-1-is-uninstalled-the-sql-server-2012-instance-must-be-repaired-to-restore-certain-components"></a>1.10 Visual Studio 2010 Service Pack 1 をアンインストールした場合、特定のコンポーネントを復元するために SQL Server 2012 インスタンスの修復が必要  
**問題:** [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] インストールは、Visual Studio 2010 Service Pack 1 の一部のコンポーネントに依存します。 Service Pack 1 をアンインストールすると、共有コンポーネントの一部が元のバージョンにダウングレードされ、残りのコンポーネントの一部は、コンピューターから完全に削除されます。  
  
**回避策:** 元のソース メディアまたはネットワークのインストール場所の [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] のインスタンスを修復します。  
  
1.  SQL Server のインストール メディアから、SQL Server セットアップ プログラム (setup.exe) を起動します。  
  
2.  必須コンポーネントのインストールとシステムの検証が実行された後、セットアップ プログラムによって **[SQL Server インストール センター]** ページが表示されます。  
  
3.  左側のナビゲーション領域の **[メンテナンス]** をクリックし、 **[修復]** をクリックして修復操作を開始します。 **[スタート]** メニューを使用してインストール センターを起動した場合は、この時点で、インストール メディアの場所を指定する必要があります。  
  
4.  セットアップ サポート ルールおよびセットアップ サポート ファイルのルーチンが実行されて、システムに必須コンポーネントがインストールされていること、およびコンピューターがセットアップの検証ルールに合格していることが確認されます。 続行するには、 **[OK]** または **[インストール]** をクリックします。  
  
5.  **[インスタンスの選択]** ページで、修復するインスタンスを選択し、 **[次へ]** をクリックします。  
  
6.  修復ルールが実行され、操作が検証されます。 続行するには、 **[次へ]** をクリックします。  
  
7.  **[修復の準備完了]** ページで、操作を続行する準備ができたことが示されます。 続行するには、 **[修復]** をクリックします。  
  
8.  **[修復の進行状況]** ページに、修復操作の進行状況が表示されます。 **[完了]** ページでは、操作が完了したことが示されます。  
  
SQL Server のインスタンスを修復する方法の詳細については、「 [失敗した SQL Server 2012 のインストールの修復](../database-engine/install-windows/repair-a-failed-sql-server-installation.md)」をご覧ください。  
  
### <a name="111-an-instance-of-sql-server-2012-might-fail-after-an-os-upgrade"></a>1.11 OS のアップグレード後に SQL Server 2012 のインスタンスが失敗する場合がある  
**問題点:** オペレーティング システムを Windows Vista から Windows 7 SP1 にアップグレードした後、SQL Server 2012 のインスタンスが次のエラーで失敗する場合があります。  
  
`Setup has detected that the .NET Framework version 4 needs to be repaired. Do not restart your computer until Setup is complete.`  
  
**回避策**:オペレーティング システムをアップグレードした後、.NET Framework 4 のインストールを修復します。 詳細については、「 [.NET Framework の既存のインストールを修復する方法](https://support.microsoft.com/kb/306160)」をご覧ください。  
  
### <a name="112-sql-server-edition-upgrade-requires-a-restart"></a>1.12 SQL Server エディションのアップグレードには再起動が必要  
**問題点**: SQL Server 2012 のインスタンスのエディションをアップグレードすると、新しいエディションに関連付けられた機能の一部がすぐにアクティブにならない場合があります。  
  
**回避策**:SQL Server 2012 のインスタンスのエディションのアップグレード後は、コンピューターを再起動します。 SQL Server 2012 でサポートされているアップグレードの詳細については、「 [サポートされているバージョンとエディションのアップグレード](../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)」をご覧ください。  
  
### <a name="113-database-with-read-only-filegroup-or-files-cannot-be-upgraded"></a>1.13 読み取り専用のファイル グループまたはファイルを含むデータベースをアップグレードできない  
**問題点**: データベースまたはそのファイルやファイル グループが読み取り専用に設定されている場合、データベースをアタッチしたり、バックアップからデータベースを復元したりして、データベースをアップグレードすることができません。  エラー 3415 が返されます。  この問題は、SQL Server のインスタンスのインプレース アップグレードを実行するときにも適用されます。 つまり、SQL Server 2012 をインストールして SQL Server の既存のインスタンスを置き換えようとしたときに、既存のデータベースの 1 つ以上が読み取り専用に設定されています。  
  
**回避策:** アップグレードする前に、データベースおよびそのファイルとファイル グループが読み取り/書き込み可能に設定されていることをご確認ください。  
  
### <a name="114-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.14 同じ IP アドレスを使用すると SQL Server フェールオーバー クラスターのインスタンスの再インストールに失敗する  
**問題点:** SQL Server フェールオーバー クラスター インスタンスのインストール中に不正な IP アドレスを指定すると、インストールは失敗します。 失敗したインスタンスをアンインストールした後に、同じインスタンス名と適切な IP アドレスを使用して SQL Server フェールオーバー クラスター インスタンスを再インストールしようとすると、インストールは失敗します。 このエラーは、前のインストールによって残されたリソース グループが重複するため発生します。  
  
**回避策:** この問題を解決するには、再インストール時に別のインスタンス名を使用するか、再インストール前にリソース グループを手動で削除してください。 詳細については、「 [SQL Server フェールオーバー クラスターでのノードの追加または削除](failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」をご覧ください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="AS"></a>2.0 Analysis Services  
  
### <a name="21-sql-editor-and-as-editor-cannot-connect-to-their-respective-server-instances-in-the-same-ssms-instance"></a>2.1 SQL エディターおよび AS エディターから同じ SSMS インスタンス内の対応するサーバー インスタンスに接続できない  
**問題点:** SQL エディターが Analysis Services サーバーに既に接続されている場合、MDX/DMX エディターを使用して Analysis Services サーバーに接続できません。  
  
SQL Server Management Studio 2012 (SSMS) を使用しているときに、エディターで開いている .sql ファイルが SQL Server インスタンスに接続されている場合、同じ SSMS インスタンス内で開いた MDX ファイルまたは DMX ファイルから AS サーバー インスタンスに接続できません。 同様に、SSMS のエディターで既に開いている MDX ファイルまたは DMX ファイルが AS サーバー インスタンスに接続されている場合、同じ SSMS インスタンス内で開いた .sql ファイルから SQL Server インスタンスに接続できません。  
  
**回避策**:この問題を回避するには、次のいずれかの方法を使用します。  
  
-   別の SSMS インスタンスを開始して MDX/DMX ファイルを開く。  
  
-   SQL エディターを切断して、MDX/DMX エディターを AS サーバーに接続する。  
  
### <a name="22-cannot-create-or-open-tabular-projects-when-builtinadministrators-group-name-cannot-be-resolved"></a>2.2 BUILTIN\Administrators グループ名を解決できない場合、テーブル プロジェクトを作成または開くことができない  
**問題点:** テーブル プロジェクトを作成する場合または開く場合は、ワークスペース データベース サーバーの管理者である必要があります。 サーバーの Administrators グループにユーザーを追加するには、ユーザー名またはグループ名を追加します。 BUILTIN\Administrator グループのメンバーであっても、準備したときのドメインにワークスペース データベース サーバーが参加していないと、BIM ファイルを作成または編集することはできません。 BIM ファイルを開く操作または作成する操作を行うと、操作が失敗し、次のエラー メッセージが表示されます。  
  
`"The BIM file cannot be opened. The server connected to is not valid. Reason: You are not an administrator of server [server name]."`  
  
**回避策:**  
  
-   ワークスペース データベース サーバーおよび SQL Server Data Tools (SSDT) コンピューターを再度ドメインに参加させます。  
  
-   ワークスペース データベース サーバーおよび SSDT、あるいはそのいずれかのコンピューターが今後ドメインに参加しない場合は、ワークスペース データベース サーバーの管理者として、BUILTIN\Administrators グループではなく個々のユーザー名を追加します。  
  
### <a name="23-ssis-components-for-as-tabular-models-do-not-work-as-expected"></a>2.3 AS テーブル モデル用の SSIS コンポーネントが予期したとおりに動作しない  
Analysis Services (AS) 用の SQL Server Integration Services (SSIS) コンポーネントが、テーブル モデルに対して予期したとおりに動作しません。 テーブル モデルを扱うための SSIS パッケージを作成する場合、次のような既知の問題があります。  
  
**問題点:** AS 接続マネージャーが、データ ソースと同じソリューションでテーブル モデルを使用できません。  
  
**回避策:** AS 処理タスクまたは AS DDL 実行タスクを構成する前に、明示的に AS サーバーに接続する必要があります。  
  
テーブル モデルを扱う場合、AS 処理タスクに関する問題がいくつかあります。  
  
**問題点:** データベース、テーブル、およびパーティションの代わりに、キューブ、メジャー グループ、およびディメンションが表示されます。 これは、タスクの制限事項です。  
  
**回避策:** キューブ、メジャー グループ、ディメンションの構造を使用して、テーブル モデルを処理することもできます。  
  
**問題点:** テーブル モードで実行する AS でサポートされるいくつかの処理オプションが、AS 処理タスクで表示されません ([デフラグの処理] など)。  
  
**回避策:** ProcessDefrag コマンドが含まれた XMLA スクリプトを実行する代わりに、Analysis Services の DDL 実行タスクを使用します。  
  
**問題点:** ツール内の一部の構成オプションを使用できません。 たとえば、パーティションを処理する際に [関連オブジェクトを処理する] は使用しないでください。また、[並列処理] 構成オプションには、標準 SKU で並列処理がサポートされていないという無効なエラー メッセージが含まれています。  
  
**回避策:** なし  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="BOL"></a>3.0 オンライン ブック  
  
### <a name="31-help-viewer-for-sql-server-crashes-in-environments-configured-to-run-only-ipv6"></a>3.1 IPv6 のみを実行するように構成された環境では SQL Server 用ヘルプ ビューアーがクラッシュする  
**問題点**: IPv6 のみを実行するように構成された環境では、SQL Server 2012 用ヘルプ ビューアーがクラッシュし、次のエラー メッセージが表示されます。  
  
`HelpLibAgent.exe has stopped working.`  
  
> [!IMPORTANT]  
> これは、IPv6 のみを有効にした状態で実行されているすべての環境に当てはまります。 IPv4 (または IPv4 と IPv6 の両方) が有効になっている環境は影響を受けません。  
  
**回避策**:この問題を回避するには、IPv4 を有効にするか、以下の手順を使用してレジストリ エントリを追加し、ACL を作成して、IPv6 に対してヘルプ ビューアーを有効にします。  
  
1.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v1.0 の下に、"IPv6" という名前のレジストリ キーを作成し、値を "1 (DWORD(32 bit))" に設定します。  
  
2.  管理 CMD ウィンドウから次のコマンドを実行して、IPv6 のポートに対するセキュリティ ACL を設定します。  
  
    ```  
    netsh http add urlacl url=https://[::1]:47873/help/ sddl=D:(A;;GX;;;WD)  
    ```  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-not-supported-in-a-cluster"></a>4.1 クラスターでサポートされていない DQS  
**問題点:** DQS は、SQL Server クラスターのインストールではサポートされていません。 SQL Server のクラスター インスタンスをインストールする場合は、 **[機能の選択]** ページで **[Data Quality Services]** チェック ボックスと **[Data Quality Client]** チェック ボックスをオンにしないでください。 クラスター インスタンスのインストール時にこれらのチェック ボックスがオンになっている場合 (および DQSInstaller.exe ファイルを実行して Data Quality Server のインストールを完了している場合)、DQS は、このノードにインストールされますが、クラスターにノードを追加しても追加のノードでは使用できません。そのため、DQS は追加のノードで動作しません。  
  
**回避策:** この問題を回避するには、SQL Server 2012 累積更新プログラム 1 をインストールします。 手順については、「[https://support.microsoft.com/kb/2674817](https://support.microsoft.com/kb/2674817)」を参照してください。  
  
### <a name="42-to-reinstall-data-quality-server-delete-the-dqs-objects-after-uninstalling-data-quality-server"></a>4.2 Data Quality Server を再インストールするには Data Quality Server をアンインストールしてから DQS オブジェクトを削除する必要がある  
**問題点:** Data Quality Server をアンインストールしても、DQS オブジェクト (DQS データベース、DQS ログイン、および DQS ストアド プロシージャ) は SQL Server インスタンスから削除されません。  
  
**回避策:** 同じコンピューターの同じ SQL Server インスタンスに Data Quality Server を再インストールするには、SQL Server インスタンスから手動で DQS オブジェクトを削除する必要があります。 さらに、Data Quality Server を再インストールする前に、そのコンピューターの C:\Program Files\Microsoft SQL Server\MSSQL11.<SQL_Server_Instance>\MSSQL\DATA フォルダーから DQS データベース (DQS_MAIN、DQS_PROJECTS、および DQS_STAGING_DATA) ファイルも削除する必要があります。 この操作を行わないと、Data Quality Server のインストールが失敗します。 ナレッジ ベースやデータ品質プロジェクトなどのデータを残しておく場合は、データベース ファイルを削除せずに別の場所に移動します。 アンインストール プロセスの完了後に DQS オブジェクトを削除する方法の詳細については、「 [Data Quality Server オブジェクトの削除](https://msdn.microsoft.com/library/hh231667.aspx)」をご覧ください。  
  
### <a name="43-indication-of-a-terminated-knowledge-discovery-or-interactive-cleansing-activity-is-delayed"></a>4.3 ナレッジ検出アクティビティや対話的なクレンジング アクティビティの終了通知が遅れる  
**問題点:** 管理者がアクティビティを [アクティビティの監視] 画面で終了した場合、ナレッジ検出、ドメイン管理、または対話的なクレンジングのアクティビティを実行しているインタラクティブ ユーザーには、そのユーザーが次に操作を実行するまで、アクティビティが終了したことが通知されません。  
  
**回避策:** なし  
  
### <a name="44-a-cancel-operation-discards-work-from-multiple-activities"></a>4.4 複数アクティビティに含まれる作業がキャンセル操作によって破棄される  
**問題点:** 実行中のナレッジ検出またはドメイン管理アクティビティに対し **[キャンセル]** をクリックした場合、それより前に完了した他のアクティビティで実行中にパブリッシュ操作が行われていなければ、現在のアクティビティだけでなく、前回のパブリッシュ以降に実行されたすべてのアクティビティに含まれる作業が破棄されます。  
  
**回避策:** これを回避するには、ナレッジ ベースに保存しておく必要のある作業は、新しいアクティビティを開始する前にパブリッシュしてください。  
  
### <a name="45-controls-do-not-scale-properly-on-large-font-sizes"></a>4.5 大きなフォント サイズで、コントロールのサイズが正しく調整されない  
**問題点:** (Windows Server 2008 または Windows 7 で) テキストのサイズを [大 - 150%] に変更した場合、または (Windows 7 で) [カスタム DPI] の設定を [200%] に変更した場合は、 **[新しいナレッジ ベース]** ページの **[キャンセル]** ボタンおよび **[作成]** ボタンにアクセスできません。  
  
**回避策:** この問題を解決するには、フォントを小さいサイズに設定します。  
  
### <a name="46-screen-resolution-of-800x600-is-not-supported"></a>4.6 画面の解像度 800x600 はサポートされていない  
**問題点:** 画面の解像度が 800x600 に設定されていると、Data Quality Client アプリケーションが正しく表示されません。  
  
**回避策:** この問題を解決するには、画面の解像度を高い値に設定します。  
  
### <a name="47-map-bigint-column-in-the-source-data-to-a-decimal-domain-to-prevent-data-loss"></a>4.7 データ損失を回避するには、ソース データの bigint 列を decimal ドメインにマップする  
**問題点:** ソース データ内の列が **bigint** データ型である場合は、この列を DQS の **integer** データ型ではなく、**decimal** データ型のドメインにマップする必要があります。 これは、 **int** データ型よりも **decimal** データ型の方が表現できる値の範囲の値が広く、格納できる値も大きいためです。  
  
### <a name="48-nvarcharmax-and-varcharmax-data-types-are-not-supported-in-the-dqs-cleansing-component-in-integration-services"></a>4.8 NVARCHAR(MAX) および VARCHAR(MAX) データ型が、Integration Services の DQS クレンジング コンポーネントでサポートされない  
**問題点:** **nvarchar(max)** データ型および **varchar(max)** データ型のデータ列が、Integration Services の DQS クレンジング コンポーネントでサポートされていません。 したがって、これらのデータ列は、DQS クレンジング変換エディターの [マッピング] タブでのマッピングで使用できないため、クレンジングすることができません。  
  
**回避策:** DQS クレンジング コンポーネントを使用してこれらのデータ列を処理する前に、データ変換の変換を使用して、これらの列を **DT_STR** データ型または **DT_WSTR** データ型に変換する必要があります。  
  
### <a name="49-the-item-to-run-dqsinstallerexe-on-the-start-menu-is-overwritten-on-new-sql-server-instance-installation"></a>4.9 [スタート] メニューの DQSInstaller.exe を実行するアイテムが新しい SQL Server インスタンスのインストールで上書きされる  
**問題点:** SQL Server インスタンスに Data Quality Services をインストールすることを選択した場合、SQL Server セットアップの完了後に、 **[スタート]** メニューの **[Data Quality Services]** プログラム グループに **[Data Quality Server インストーラー]** というアイテムが作成されます。 ただし、同じコンピューターに複数の SQL Server インスタンスをインストールした場合でも、 **[スタート]** メニューに作成される **[Data Quality Server インストーラー]** アイテムは 1 つです。 このアイテムをクリックすると、最後にインストールされた SQL Server インスタンスの DQSInstaller.exe ファイルが実行されます。  
  
### <a name="410-activity-monitoring-displays-incorrect-status-for-failed-integration-services-cleansing-activities"></a>4.10 [アクティビティ監視] 画面に、失敗した Integration Services クレンジング アクティビティについて正しくないステータスが表示される  
[アクティビティ監視] 画面の **[現在の状態]** 列に、失敗した Integration Services クレンジング アクティビティに対しても **[成功]** と表示されます。  
  
### <a name="411-schema-name-is-not-displayed-as-part-of-tableview-name"></a>4.11 スキーマ名が [テーブル名またはビュー名] の一部として表示されない  
Data Quality Client のマップ ステージ中にいずれかの DQS アクティビティで SQL Server データ ソースを選択すると、スキーマ名のないテーブルとビューの一覧が表示されます。 したがって、同じ名前でスキーマが異なる複数のテーブル/ビューがある場合、それらはデータ プレビューを参照するか、選択してマップに使用可能なフィールドを参照することでのみ区別できます。  
  
### <a name="412-issue-with-cleansing-output-and-export-if-data-source-is-mapped-to-a-composite-domain-containing-a-child-domain-of-date-type"></a>4.12 データ ソースが日付型の子ドメインを含む複合ドメインにマップされている場合のクレンジングの出力およびエクスポートの問題  
クレンジング データ品質プロジェクトで、ソース データ内のフィールドを、日付データ型の子ドメインを持つ複合ドメインにマップした場合、クレンジング結果内の子ドメイン出力に正しくない日付形式があり、データベースへのエクスポート操作が失敗します。  
  
### <a name="413-error-when-mapping-to-an-excel-sheet-that-contains-a--semicolon-in-its-name"></a>4.13 名前に ; (セミコロン) を含む Excel シートへのマップ時のエラー  
**問題点:** Data Quality Client の任意の DQS アクティビティの **[マップ]** ページで、その名前に ; (セミコロン) が含まれるソース Excel シートにマップした場合、 **[マップ]** ページで **[次へ]** をクリックすると、処理されていない例外メッセージが表示されます。  
  
**回避策:** マップするソース データを格納している Excel ファイルのシート名から ; (セミコロン) を削除し、再試行してください。  
  
### <a name="414-issue-with-date-or-datetime-values-in-unmapped-source-fields-in-excel-during-cleansing-and-matching"></a>4.14 クレンジングおよび照合中の Excel のマップされていないソース フィールドの Date または DateTime 値の問題  
**問題点**: ソース データが Excel で、**Date** または **DateTime** データ型の値が含まれるソース フィールドをマップしていない場合は、クレンジングおよび照合アクティビティ中に次が発生します。  
  
-   マップされていない **Date** 値が yyyymmdd の形式で表示およびエクスポートされる。  
  
-   マップされていない **DateTime** 値の時間値が失われ、yyyymmdd の形式で表示およびエクスポートされる。  
  
**回避策:** マップされていないフィールド値は、クレンジング アクティビティでは **[結果の管理と表示]** ページの右下のペイン、照合アクティビティでは **[照合]** ページで確認できます。  
  
### <a name="415-cannot-import-domain-values-from-an-excel-file-xls-containing-more-than-255-columns-of-data"></a>4.15 255 列を超えるデータを含む Excel ファイル (.xls) からドメイン値をインポートできない  
**問題点:** 255 列を超えるデータを含む Excel 97-2003 ファイル (.xls) からドメインに値をインポートした場合、例外メッセージが表示され、インポートに失敗します。  
  
**回避策:** この問題を解決するには、次のいずれかの操作を行います。  
  
-   .xls ファイルを .xlsx ファイルとして保存し、.xlsx ファイルからドメインに値をインポートします。  
  
-   .xls ファイルで 255 列目より後のすべての列のデータを削除してファイルを保存し、.xls ファイルからドメインに値をインポートします。  
  
### <a name="416-activity-monitoring-feature-is-unavailable-for-roles-other-than-dqsadministrator"></a>4.16 アクティビティ監視機能は dqs_administrator 以外のロールでは使用できない  
アクティビティ監視機能は、dqs_administrator ロールを持つユーザーのみが使用できます。 dqs_kb_editor ロールまたは dqs_kb_operator ロールを持つユーザー アカウントの場合、Data Quality Client アプリケーションでアクティビティ監視機能を使用することはできません。  
  
### <a name="417-error-on-opening-a-knowledge-base-in-the-recent-knowledge-base-list-for-domain-management"></a>4.17 ドメイン管理の [最近使用したナレッジ ベース] の一覧でナレッジ ベースを開くとエラーが発生する  
問題点:Data Quality Client のホーム画面で、ドメイン管理アクティビティの **[最近使用したナレッジ ベース]** の一覧でナレッジ ベースを開くと、次のエラーが発生する場合があります。  
  
`"A configuration with name 'RecentList:KB:<domain>\<username>' already exists in the database."`  
  
このエラーは、DQS では SQL Server データベースの文字列と C# の文字列を比較する方法が異なるため発生します。 SQL Server データベースの文字列比較では大文字と小文字が区別されませんが、C# では区別されます。  
  
例を挙げてこの問題を説明します。 Domain\user1 というユーザーがいるとします。 このユーザーが "user1" アカウントを使用して Data Quality Client コンピューターにログオンし、ナレッジ ベースの作業を行います。 各ユーザーが最近使用したナレッジ ベースは、DQS_MAIN データベースの A_CONFIGURATION テーブルにレコードとして格納されています。 この場合、レコードはRecentlist:kb:domain \user1 という名前で格納されます。 その後で、このユーザーが Data Quality Client コンピューターに "User1" という名前でログオンし (最初の U が大文字)、ドメイン管理アクティビティの **[最近使用したナレッジ ベース]** 一覧でナレッジ ベースを開くとします。 DQS の基になるコードで RecentList:KB:DOMAIN\user1 と DOMAIN\User1 という 2 つの文字列が比較されますが、このときに大文字と小文字が区別される C# の方法が使用されます。この 2 つの文字列は一致しないと見なされるため、DQS_MAIN データベースの A_CONFIGURATION テーブルにこのユーザー (User1) 用の新しいレコードを挿入しようとします。 しかし、SQL データベースでは文字列の比較で大文字と小文字が区別されないため、DQS_MAIN データベースの A_CONFIGURATION テーブルにその文字列が既に存在することになり、挿入操作が失敗します。  
  
**回避策:** この問題を解決するには、次のいずれかの操作を行います。  
  
-   次のステートメントを実行して、重複するエントリが存在するかどうかを確認します。  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_CONFIGURATION WHERE NAME like 'RecentList%'  
    ```  
  
    次に、以下のステートメントを実行して、影響を受けるユーザーのレコードだけを削除できます。影響を受けるドメインとユーザー名に合わせて WHERE 句の値を変更してください。  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%<domain>\<username>'  
    ```  
  
    または、DQS のすべてのユーザーの最近使用したアイテムを削除することもできます。  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%'  
    ```  
  
-   Data Quality Client コンピューターにログオンする際に、そのユーザー アカウントの大文字と小文字の表記を前回指定したときと同じにします。  
  
> [!NOTE]  
> この問題を回避するには、Data Quality Client コンピューターにログオンする際に、ユーザー アカウントの大文字と小文字の表記を一貫させてください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DE"></a>5.0 データベース エンジン  
  
### <a name="51-use-of-distributed-replay-controller-and-distributed-replay-client-features"></a>5.1 分散再生コントローラー機能と分散再生クライアント機能の使用  
**問題点:** Windows Server 2008、Windows Server 2008 R2、および Windows Server 7 の Server Core SKU で分散再生コントローラー機能と分散再生クライアント機能がサポートされない場合でも、この 2 つの機能を使用することができます。  
  
**回避策:** Windows Server 2008、Windows Server 2008 R2、および Windows Server 7 の Server Core SKU では、この 2 つの機能をインストールしたり、使用したりしないでください。  
  
### <a name="52-sql-server-management-studio-depends-on-visual-studio-2010-sp1"></a>5.2 SQL Server Management Studio が Visual Studio 2010 SP1 に依存する  
**問題点**: SQL Server 2012 Management Studio が正常に動作するには、Visual Studio 2010 SP1 が必要です。 Visual Studio 2010 SP1 をアンインストールすると、SQL Server Management Studio の機能が損なわれ、サポートされない状態になります。 その場合、次のような問題が発生することがあります。  
  
-   ssms.exe のコマンドライン パラメーターが正常に機能しない。  
  
-   ssms.exe に /? スイッチを付加して実行すると、誤ったヘルプ情報が 表示される。  
  
-   エクスプローラーでファイルをダブルクリックして開くと、常に新しい SSMS インスタンスが起動してファイルが開かれる。  
  
-   通常ユーザー モードでクエリをデバッグできない。  
  
**回避策**:Visual Studio 2010 SP1 をもう一度インストールして、Management Studio を再起動します。  
  
### <a name="53-x64-operating-systems-require-64-bit-powershell-20"></a>5.3 x64 オペレーティング システムには 64 ビットの PowerShell 2.0 が必要  
**問題点:** 64 ビット オペレーティング システム上の SQL Server 2012 インスタンスでは、Windows PowerShell Extensions for SQL Server の 32 ビット インストールがサポートされていません。  
  
**回避策:**  
  
-   64 ビットの SQL Server 2012 を 64 ビットの管理ツールおよび 64 ビットの Windows PowerShell Extensions for SQL Server と共にインストールします。  
  
-   または、32 ビットの Windows PowerShell 2.0 プロンプトから SQLPS モジュールをインポートします。  
  
### <a name="54-an-error-might-occur-when-navigating-in-the-generate-script-wizard"></a>5.4 スクリプト生成ウィザードでの移動時にエラーが発生することがある  
**問題点:** **[スクリプトの保存またはパブリッシュ]** をクリックしてスクリプトの生成ウィザードでスクリプトを生成してから、 **[オプションの選択]** または **[スクリプト作成オプションの設定]** をクリックして移動するか、 **[スクリプトの保存またはパブリッシュ]** を再度クリックすると、次のエラーが発生することがあります。  
  
<pre>
An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo)  
------------------------------  
ADDITIONAL INFORMATION:  
Invalid object name 'sys.federations'. (Microsoft SQL Server, Error: 208)
</pre>  
  
**回避策:** スクリプトの生成ウィザードを閉じて再度開きます。  
  
### <a name="55-new-maintenance-plan-layout-not-compatible-with-earlier-sql-server-tools"></a>5.5 従来の SQL Server ツールが新しいメンテナンス プラン レイアウトをサポートしない  
**問題点:** SQL Server 2012 の管理ツールを使用して、以前のバージョンの SQL Server 管理ツール (SQL Server 2008 R2、SQL Server 2008、または SQL Server 2005) で作成された既存のメンテナンス プランを変更すると、メンテナンス プランが新しい形式で保存されます。 この形式は、以前のバージョンの SQL Server 管理ツールではサポートされません。  
  
**回避策**:なし  
  
### <a name="56-intellisense-has-limitations-when-logged-in-to-a-contained-database"></a>5.6 包含データベースのログイン時に Intellisense の制限がある  
問題点:SQL Server Management Studio (SSMS) および SQL Server Data Tools (SSDT) では、Intellisense は、含まれているユーザーが包含データベースにログインしている場合、期待どおりに機能しません。 その場合、次のような動作が発生します。  
  
1.  無効なオブジェクトに下線が表示されません。  
  
2.  オートコンプリートの一覧が表示されません。  
  
3.  組み込み関数のツールヒント ヘルプが機能しません。  
  
**回避策**:なし  
  
### <a name="57-alwayson-availability-groups"></a>5.7 AlwaysOn 可用性グループ  
可用性グループを作成する前に、オンライン ブックの「 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 (SQL Server)](https://go.microsoft.com/?linkid=9753168) 」をご覧ください。 AlwaysOn 可用性グループの概要については、オンライン ブックの [AlwaysOn 可用性グループ (SQL Server) に関するページ](https://go.microsoft.com/?linkid=9753166)をご覧ください。  
  
#### <a name="571-client-connectivity-for-alwayson-availability-groups"></a>5.7.1 AlwaysOn 可用性グループのクライアント接続性  
**更新日時:** 2012 年 8 月 13 日  
  
このセクションでは、AlwaysOn 可用性グループのドライバー サポート状況を示し、ドライバーがサポートされない場合の回避策について説明します。  
  
**ドライバー サポート**  
  
次の表は、AlwaysOn 可用性グループのドライバー サポートをまとめたものです。  
  
|Driver|マルチサブネット フェールオーバー|アプリケーションの目的|読み取り専用ルーティング|マルチサブネット フェールオーバー:より高速な単一サブネット エンドポイント フェールオーバー|マルチサブネット フェールオーバー:SQL クラスター インスタンスの名前付きインスタンスの解決|  
|----------|--------------------------|----------------------|----------------------|------------------------------------------------------------------|---------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|はい|はい|はい|はい|はい|  
|SQL Native Client 11.0 OLEDB|いいえ|はい|はい|いいえ|いいえ|  
|ADO.NET with .NET Framework 4.0 と接続性に関する修正プログラム **\&#42;**|はい|はい|はい|はい|[ユーザー アカウント制御]|  
|ADO.NET with .NET Framework 3.5 SP1 と接続性に関する修正プログラム **\&#42;\&#42;**|はい|はい|はい|はい|はい|  
|Microsoft JDBC Driver 4.0 for SQL Server|はい|はい|はい|はい|はい|  
  
**\&#42;** ADO .NET with .NET Framework 4.0 用の接続性に関する修正プログラムをダウンロードしてください ([https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211))。  
  
**\&#42;\&#42;** ADO .NET with .NET Framework 3.5 SP1 用の接続性に関する修正プログラムをダウンロードしてください ([https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347))。  
  
**MultiSubnetFailover のキーワードおよび関連機能**  
  
MultiSubnetFailover は、SQL Server 2012 の AlwaysOn 可用性グループおよび AlwaysOn フェールオーバー クラスター インスタンスに対して高速フェールオーバーを有効にするために使用する新しい接続文字列キーワードです。 接続文字列で MultiSubnetFailover=True が設定されていると、次の 3 つのサブ機能が有効になります。  
  
-   AlwaysOn 可用性グループまたはフェールオーバー クラスター インスタンスに対する複数サブネット リスナーへのより高速なマルチサブネット フェールオーバー。  
  
    -   マルチサブネット AlwaysOn フェールオーバー クラスター インスタンスへの名前付きインスタンスの解決。  
  
-   AlwaysOn 可用性グループまたはフェールオーバー クラスター インスタンスの単一サブネット リスナーへのより高速な単一サブネット フェールオーバー。  
  
    -   この機能は、単一のサブネット内に単一の IP を持つリスナーに接続する場合に使用されます。 TCP 接続の再試行をより積極的に実行して、単一サブネット フェールオーバーを高速化します。  
  
-   マルチサブネット AlwaysOn フェールオーバー クラスター インスタンスへの名前付きインスタンスの解決。  
  
    -   複数サブネット エンドポイントを持つ AlwaysOn フェールオーバー クラスター インスタンスの名前付きインスタンス解決サポートを追加します。  
  
**.NET Framework 3.5 および OLEDB で MultiSubnetFailover=True はサポートされない**  
  
**問題点:** 可用性グループまたはフェールオーバー クラスター インスタンスのリスナー名 (ネットワーク名または WSFC クラスター マネージャーのクライアント アクセス ポイント) が、異なるサブネットの複数の IP アドレスを使用したものであるとき、ADO.NET with .NET Framework 3.5SP1 または SQL Native Client 11.0 OLEDB を使用している場合、可用性グループ リスナーに対するクライアント接続要求の 50% が接続タイムアウトに達する可能性があります。  
  
**回避策:** 次のいずれかのタスクを実行することをお勧めします。  
  
-   クラスター リソースを操作する権限がない場合は、接続タイムアウトを 30 秒に設定します (この値は結果として、20 秒の TCP タイムアウトと 10 秒のバッファーになります)。  
  
    **長所:** :クロスサブネット フェールオーバーが発生した場合、クライアントの復旧時間が短くなります。  
  
    **短所**:半数のクライアント接続に 20 秒以上要します。  
  
-   クラスター リソースを操作する権限がある場合は、可用性グループ リスナーのネットワーク名を **RegisterAllProvidersIP**=0 に設定する手法をお勧めします。 詳細については、後の「RegisterAllProvidersIP を無効にし、TTL を短縮する PowerShell サンプル スクリプト」をご覧ください。  
  
    **長所:** クライアント接続のタイムアウト値を大きくする必要がありません。  
  
    **短所:** クロスサブネット フェールオーバーが発生した場合、HostRecordTTL 設定およびクロスサイト DNS/AD レプリケーション スケジュールの設定によっては、クライアントの復旧時間が 15 分以上になる可能性があります。  
  
**RegisterAllProvidersIP を無効にし、TTL を短縮する PowerShell サンプル スクリプト**  
  
次の PowerShell サンプル スクリプトは、 `RegisterAllProvidersIP` を無効にし、TTL を短縮する方法を示しています。 `yourListenerName` は、変更対象のリスナーの名前に置き換えてください。  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName|Set-ClusterParameter RegisterAllProvidersIP 0  
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
```  
  
#### <a name="572-upgrading-from-ctp3-with-availability-group-configured-is-not-supported"></a>5.7.2 可用性グループが構成された CTP3 からのアップグレードはサポートされない  
アップグレードする前に、可用性グループを削除し、再作成します。 これは、CTP3 ビルドの制限によるものです。 将来のビルドではこの制限がなくなります。  
  
#### <a name="573-side-by-side-installation-of-ctp3-with-later-versions-is-not-supported-if-you-have-an-availability-group-configured-in-your-instance"></a>5.7.3 インスタンスに可用性グループが構成されている場合、新しいバージョンでの CTP3 のサイド バイ サイド インストールはサポートされない  
これは、CTP3 ビルドの制限によるものです。 将来のビルドではこの制限がなくなります。  
  
#### <a name="574-side-by-side-installation-of-ctp3-with-later-versions-of-failover-cluster-instances-is-not-supported"></a>5.7.4 新しいバージョンのフェールオーバー クラスター インスタンスでの CTP3 のサイド バイ サイド インストールはサポートされない  
これは、CTP3 ビルドの制限によるものです。 将来のビルドではこの制限がなくなります。 CTP3 からフェールオーバー クラスター インスタンスをアップグレードするには、必ずノード上のすべてのインスタンスを同時にアップグレードします。  
  
#### <a name="575--timeouts-may-occur-when-using-multi-ips-in-the-same-subnet-with-alwayson"></a>5.7.5 AlwaysOn が設定されている同じサブネット内の複数の IP を使用するとタイムアウトが発生する場合がある  
**問題点:** AlwaysOn が設定されている同じサブネット内の複数の IP を使用すると、ユーザーの利用中にタイムアウトが発生する場合があります。 これは、先頭の IP に問題がある場合に発生します。  
  
**回避策:** 接続文字列で 'multisubnetfailover = true' を使用します。  
  
#### <a name="576-failure-to-create-new-availability-group-listeners-because-of-active-directory-quotas"></a>5.7.6 Active Directory クォータが原因で新しい可用性グループ リスナーを作成できない  
**問題点:** 新しい可用性グループ リスナーの作成は、参加しているクラスター ノード マシン アカウントの Active Directory クォータに達したため、失敗する場合があります。 詳細については、「 [コンピューター オブジェクト変更時のクラスター サービス アカウントのトラブルシューティング方法](https://support.microsoft.com/kb/307532) 」および「 [Active Directory Quotas (Active Directory クォータ)](https://technet.microsoft.com/library/cc904295(WS.10).aspx)」をご覧ください。  
  
#### <a name="577-netbios-conflicts-because-availability-group-listener-names-use-an-identical-15-character-prefix"></a>5.7.7 可用性グループ リスナー名で同一の 15 文字のプレフィックスが使用されていることによる NetBIOS の競合  
同じ Active Directory で制御されている 2 つの WSFC クラスターがあり、両方のクラスターで可用性グループ リスナーを作成しようとする場合、15 文字より長い名前を使用して、15 文字のプレフィックスが同一であると、仮想ネットワーク名リソースをオンラインにできなかったことを示すエラーが表示されます。 DNS 名のプレフィックスに対する名前付け規則の詳細については、「 [Assigning Domain Names (ドメイン名を割り当てる)](https://technet.microsoft.com/library/cc731265(WS.10).aspx)」を参照してください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="IS"></a>6.0 Integration Services  
  
### <a name="61-the-change-data-capture-service-for-oracle-and-the-change-data-capture-designer-console-for-oracle"></a>6.1 Change Data Capture Service for Oracle と Change Data Capture Designer Console for Oracle  
CDC Service for Oracle は、Oracle トランザクション ログをスキャンして目的の Oracle テーブルに対する変更を SQL Server 変更テーブルにキャプチャする Windows サービスです。 CDC デザイナー コンソールは、Oracle CDC インスタンスを開発および管理するために使用されます。 CDC デザイナー コンソールは、Microsoft 管理コンソール (MMC) スナップインです。  
  
#### <a name="611-install-the-cdc-service-for-oracle-and-the-cdc-designer-for-oracle"></a>6.1.1 CDC Service for Oracle と CDC Designer for Oracle のインストール  
**問題点:** CDC Service と CDC Designer は、SQL Server セットアップではインストールされません。 更新されたヘルプ ファイルに記載されている要件と前提条件を満たすコンピューターに、CDC Service または CDD Designer を手動でインストールする必要があります。  
  
**回避策:** CDC Service for Oracle をインストールするには、AttunityOracleCdcService.msi を SQL Server のインストール メディアから手動で実行します。 CDC デザイナー コンソールをインストールするには、SQL Server のインストール メディアから AttunityOracleCdcDesigner.msi を手動で実行します。  x86 と x64 用のインストール パッケージは、SQL Server のインストール メディアの .\Tools\AttunityCDCOracle\ にあります。  
  
#### <a name="612-f1-help-functionality-points-to-incorrect-documentation-files"></a>6.1.2 F1 ヘルプ機能で誤ったドキュメント ファイルが参照される  
**問題点:** F1 ヘルプのドロップダウン リストを使用したとき、または Attunity コンソールで "?" をクリックしたときに、適切なヘルプ ドキュメントにアクセスできません。 誤った chm ファイルが参照されます。  
  
**回避策:** CDC Service for Oracle および CDC Designer for Oracle のインストール時に、適切な chm ファイルがインストールされています。 適切なヘルプ コンテンツを表示するには、 `%Program Files%\Change Data Capture for Oracle by Attunity\*.chm`から chm ファイルを直接起動します。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="MDS"></a>7.0 マスター データ サービス  
  
### <a name="71-fixing-an-mds-installation-in-a-cluster"></a>7.1 クラスター内で MDS のインストールを修復する  
**問題点:** **[マスター データ サービス]** チェック ボックスをオンにした状態で、SQL Server 2012 の RTM バージョンのクラスター化されたインスタンスをインストールすると、MDS は 1 つのノードにインストールされますが、クラスターに追加した他のノードでは、使用できなくなり、動作しなくなります。  
  
**回避策**:この問題を解決するには、次の手順を実行して、SQL Server 2012 Cumulative Release 1 (CU1) をインストールする必要があります。  
  
1.  既存の SQL または MDS のインストールがないことを確認します。  
  
2.  ローカル ディレクトリに SQL Server 2012 CU1 をダウンロードします。  
  
3.  プライマリ クラスター ノードに SQL Server 2012 を MDS 機能と共にインストールしてから、その他のクラスター ノードに SQL Server 2012 を MDS 機能と共にインストールします。  
  
この問題の詳細および上記の手順の実行方法については、[https://support.microsoft.com/kb/2683467](https://support.microsoft.com/kb/2683467) をご覧ください。  
  
### <a name="72-microsoft-silverlight-5-required"></a>7.2 Microsoft Silverlight 5 が要求される  
マスター データ マネージャー Web アプリケーションで作業するには、Silverlight 5.0 をクライアント コンピューターにインストールする必要があります。 Silverlight の必要なバージョンがない場合、Web アプリケーションで Silverlight を使用する部分に移動したときに、Silverlight をインストールするよう要求されます。 Silverlight 5 は [https://go.microsoft.com/fwlink/?LinkId=243096](https://go.microsoft.com/fwlink/?LinkId=243096) からインストールできます。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="RS"></a>8.0 Reporting Services  
  
### <a name="81-reporting-services-connectivity-to-sql-server-pdw-requires-updated-drivers"></a>8.1 Reporting Services から SQL Server PDW に接続するにはドライバーの更新が必要  
SQL Server 2012 Reporting Services から Microsoft SQL Server PDW Appliance Update 2 以上に接続するには、PDW 接続ドライバーを更新する必要があります。 詳細については、マイクロソフトのサポートまでお問い合わせください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="SI"></a>9.0 StreamInsight  
SQL Server 2012 には StreamInsight 2.0 が含まれています。 StreamInsight 2.0 を使用するには、Microsoft SQL Server 2012 のライセンスと .NET Framework 4.0 が必要です。 StreamInsight 2.0 には、いくつかのバグ修正に加え、さまざまなパフォーマンスの改善が施されています。 詳細については、「 [Microsoft StreamInsight 2.0 RC0 Release Notes (Microsoft StreamInsight 2.0 のリリース ノート)](https://social.technet.microsoft.com/wiki/contents/articles/6539.aspx)」をご覧ください。 StreamInsight 2.0 を単独でダウンロードするには、Microsoft ダウンロード センターの [Microsoft StreamInsight 2.0 のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkId=241593) にアクセスしてください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="UA"></a>10.0 アップグレード アドバイザー  
  
### <a name="101-link-to-install-upgrade-advisor-is-not-enabled-on-chinese-hk-operating-systems"></a>10.1 中国語 (香港) のオペレーティング システムで、アップグレード アドバイザーのインストール用リンクが無効になっている  
問題点:中国語 (香港特別行政区) オペレーティング システム (OS) のサポートされている Windows バージョンでアップグレード アドバイザーをインストールしようとすると、アップグレード アドバイザーのインストール用リンクが有効になっていない場合があります。  
  
**回避策**:オペレーティング システム アーキテクチャに応じて、SQL Server 2012 メディアの `\1028_CHT_LP\x64\redist\Upgrade Advisor` または `\1028_CHT_LP\x86\redist\Upgrade Advisor` にある **SQLUA.msi** ファイルを検索してください。  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
