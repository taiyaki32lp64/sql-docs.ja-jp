---
title: 分散再生のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4aa2cc0859972f980e26d67e054dba3c955527c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950036"
---
# <a name="install-distributed-replay"></a>分散再生のインストール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  次の 3 つのいずれかの方法で分散再生をインストールできます。  
  
-   [インストール ウィザードからの分散再生のインストール](#bkmk_wizard)  
  
-   [コマンド プロンプトからの 分散再生のインストール](#bkmk_command_prompt)  
  
-   [構成ファイルを使用した 分散再生のインストール](#bkmk_configuration_file)  
  
##  <a name="bkmk_wizard"></a> インストール ウィザードからの分散再生のインストール  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生機能を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードでインストールします。 機能をインストールする場所を計画する際には、以下について検討してください。  
  
-   管理ツールは、分散再生コントローラーと同じコンピューター上、または別のコンピューター上にインストールできます。  
  
-   各 分散再生環境には、コントローラーを 1 つだけ置くことができます。  
  
-   クライアント サービスは、最大で 16 の (物理または仮想) コンピューター上にインストールできます。  
  
-   分散再生コントローラー コンピューター上には、クライアント サービスのインスタンスを 1 つだけインストールできます。 分散再生環境に複数のクライアントを置く場合は、クライアント サービスをコントローラーと同じコンピューターにインストールすることはお勧めできません。 そのようにすると、分散再生の全体的な速度が低下します。  
  
-   パフォーマンスのテストのシナリオでは、管理ツール、Distributed Replay コントローラー サービス、またはクライアント サービスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対象インスタンスにインストールすることはお勧めしません。 これらのすべての機能をターゲット サーバーにインストールするのは、アプリケーションの互換性に関する機能テストを行うときだけに限定する必要があります。  
  
-   インストール後は、クライアント上で 分散再生クライアント サービスを開始する前に、コントローラー サービスである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラーを実行する必要があります。  
  
> [!NOTE]  
>  分散再生の機能を削除または変更するには、 **コントロール パネル** で Windows の **[プログラムと機能]** ウィンドウを使用します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [プログラムのアンインストールまたは変更] **ウィンドウで** を選択し、 **[削除]** をクリックして [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを開きます。 **[機能の選択]** ページで、削除する分散再生機能を選択します。  
  
 **前提条件:**  
  
-   使用するコンピューターが、「 [分散再生の要件](../../tools/distributed-replay/distributed-replay-requirements.md)」に記載されている前提条件を満たしていることを確認します。  
  
-   この手順を開始する前に、コントローラーおよびクライアントのサービスを実行するためのドメイン ユーザー アカウントを作成します。 これらのアカウントは、Windows Administrators グループのメンバーにしないことをお勧めします。 詳細については、「 [Distributed Replay のセキュリティ](../../tools/distributed-replay/distributed-replay-security.md) 」の「ユーザーおよびサービス アカウント」を参照してください。  
  
    > [!NOTE]  
    >  管理ツール、コントローラー サービス、およびクライアント サービスが同じコンピューター上で実行されている場合は、ローカル ユーザー アカウントを使用できます。  
  
 **インストール先:**  
  
 既定のファイルの場所と標準インストールを使用した場合、基本ディレクトリは C:\Program Files \Microsoft SQL Server になります。 その下の以下の場所に、バイナリとアセンブリがインストールされます。  
  
-   32 ビット システムの場合:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]ツール  
  
     \- または -  
  
     \<共有機能ディレクトリ>\Tools\\(ユーザーが指定した代替の共有機能ディレクトリ)  
  
-   64 ビット システムの場合:  
  
     C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86)\130\Tools  
  
     \- または -  
  
     \<共有機能ディレクトリ (x86)>\Tools\\(ユーザーが指定した代替の共有機能 (x86) ディレクトリ)  
  
#### <a name="to-install-distributed-replay-features"></a>分散再生機能をインストールするには  
  
1.  分散再生の機能のインストールを開始するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを開始します。  
  
2.  **[セットアップ サポート ルール]** ページでは、SQL Server セットアップ サポート ファイルをインストールするときに発生する可能性がある問題が特定されています。 セットアップを続行する前に、セットアップ サポートの失敗を修正する必要があります。  
  
3.  **[プロダクト キー]** ページでオプション ボタンをクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の無償のエディション、または PID キーを持つ製品版のどちらをインストールするかを指定します。 詳細については、「 [SQL Server 2016 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
4.  **[ライセンス条項]** ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../includes/msconame-md.md)]に送信することもできます。  
  
5.  **[セットアップ サポート ファイル]** ページで **[インストール]** をクリックして、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のセットアップ サポート ファイルをインストールまたは更新します。  
  
6.  **[セットアップ ロール]** ページで、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール**をクリックし、 **[次へ]** をクリックして **[機能の選択]** ページに進みます。  
  
7.  **[機能の選択]** ページで、どの機能をインストールするかを設定します。  
  
    -   管理ツールをインストールするには、 **[管理ツール - 基本]** を選択します。  
  
    -   コントローラー サービスをインストールするには、 **[分散再生コントローラー]** を選択します。  
  
    -   クライアント サービスをインストールするには、 **[分散再生クライアント]** を選択します。  
  
     **重要**: 分散再生コントローラーを構成するとき、分散再生クライアント サービスの実行に使用する 1 つ以上のユーザー アカウントを指定できます。 サポートされているアカウントの一覧を次に示します。  
  
    -   ドメイン ユーザー アカウント  
  
    -   ユーザーによって作成されたローカル ユーザー アカウント  
  
    -   管理者  
  
    -   仮想アカウントおよび管理されたサービス アカウント (MSA)  
  
    -   ネットワーク サービス、ローカル サービス、およびシステム  
  
     グループ アカウント (ローカルまたはドメイン) およびその他の組み込みのアカウント (Everyone など) は使用できません。  
  
8.  必要に応じて、省略記号 (...) ボタンをクリックし、共有機能のディレクトリのパスを変更します。  
  
    1.  32 ビットのコンピューターの場合、既定のインストール パスは **C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  64 ビットのコンピューターの場合、既定のインストール パスは **C:\Program Files (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\** です。  
  
9. 終了したら **[次へ]** をクリックします。  
  
10. **[インストール ルール]** ページで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップはコンピューターの構成を検証します。 検証プロセスが完了したら、 **[次へ]** をクリックします。  
  
11. **[必要なディスク領域]** ページでは、指定した機能に必要なディスク領域が計算されます。 その後、必要なディスク領域が使用可能なディスク領域と比較されます。  
  
12. **[エラー レポート]** ページで、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の強化に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
13. **[インストール構成ルール]** ページでは、システム構成チェッカーによって別のルール セットが実行され、コンピューターの構成と指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
14. **[プログラムインストールの準備完了]** ページで、 **[インストール]** をクリックします。  
  
    > [!IMPORTANT]  
    >  分散再生をインストールした後、コントローラー コンピューターとクライアント コンピューターのファイアウォール ルールを作成し、ターゲット サーバー上で各クライアント コンピューターの権限を付与する必要があります。 詳細については、「 [インストール後の手順の実行](../../tools/distributed-replay/complete-the-post-installation-steps.md)」を参照してください。  
  
### <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 分散再生の機能をインストールするには、管理権限が必要です。 sysadmin 権限を持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのみが、テスト サーバーの sysadmin サーバー ロールにクライアント サービス アカウントを追加できます。 Distributed Replay のセキュリティ上の考慮事項の詳細については、「 [Distributed Replay のセキュリティ](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
##  <a name="bkmk_command_prompt"></a> コマンド プロンプトからの 分散再生のインストール  
 分散再生の新しいインスタンスをコマンド プロンプトでインストールすると、インストールする機能とその機能の構成を指定できます。 コマンド プロンプトによるインストールでは、分散再生ユーティリティ コンポーネントのインストール、修復、アップグレード、およびアンインストールがサポートされています。 コマンド プロンプトを使用してインストールする場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、/Q パラメーターを使用した Full Quiet モードがサポートされます。  
  
> [!NOTE]  
>  ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。  
  
### <a name="installation-parameters"></a>インストール パラメーター  
 最上位の機能には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、ツールなどがあります。 ツール機能により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理ツール、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、およびその他の共有コンポーネントがインストールされます。 分散再生コンポーネントをインストールするには、次のパラメーターを指定します。  
  
|コンポーネント|パラメーター|  
|---------------|---------------|  
|[分散再生コントローラー]|**DREPLAY_CTLR**|  
|[分散再生クライアント]|**DREPLAY_CLT**|  
|管理ツール|**ツール**|  
  
> [!IMPORTANT]  
>  分散再生をインストールした後、コントローラー コンピューターとクライアント コンピューターのファイアウォール ルールを作成し、ターゲット サーバー上で各クライアント コンピューターの権限を付与する必要があります。 詳細については、「 [インストール後の手順の実行](../../tools/distributed-replay/complete-the-post-installation-steps.md)」を参照してください。  
  
 次の表に示すパラメーターは、インストール用のコマンド ライン スクリプトを作成する場合に使用します。  
  
|パラメーター|[説明]|サポートされる値|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **省略可**|分散再生コントローラー サービスのサービス アカウント。|アカウントとパスワードのチェック|  
|/CTLRSVCPASSWORD<br /><br /> **省略可**|分散再生コントローラー のサービス アカウントのパスワード。|アカウントとパスワードのチェック|  
|/CTLRSTARTUPTYPE<br /><br /> **省略可**|分散再生コントローラー サービスのスタートアップの種類。|自動<br /><br /> Disabled<br /><br /> 手動|  
|/CTLRUSERS<br /><br /> **省略可**|分散再生コントローラー サービスの権限を持つユーザーを指定します。|区切り記号に " " (スペース) を使用した、一連のユーザー アカウント文字列<br /><br /> **重要**: 分散再生コントローラー サービスを構成するとき、分散再生クライアント サービスの実行に使用する 1 つ以上のユーザー アカウントを指定できます。 サポートされているアカウントの一覧を次に示します。<br /><br /> ドメイン ユーザー アカウント<br /><br /> ユーザーによって作成されたローカル ユーザー アカウント<br /><br /> 管理者<br /><br /> 管理者<br /><br /> 仮想アカウントおよび管理されたサービス アカウント (MSA)<br /><br /> ネットワーク サービス、ローカル サービス、およびシステム<br /><br /> <br /><br /> 注: グループ アカウント (ローカルまたはドメイン) およびその他の組み込みのアカウント (Everyone など) は使用できません。|  
|/CLTSVCACCOUNT<br /><br /> **省略可**|分散再生クライアント サービスのサービス アカウント。|アカウントとパスワードのチェック|  
|/CLTSVCPASSWORD<br /><br /> **省略可**|分散再生クライアント のサービス アカウントのパスワード。|アカウントとパスワードのチェック|  
|/CLTSTARTUPTYPE<br /><br /> **省略可**|分散再生クライアント サービスのスタートアップの種類。|自動<br /><br /> Disabled<br /><br /> 手動|  
|/CLTCTLRNAME<br /><br /> **省略可**|分散再生クライアント サービスと通信するクライアントのコンピューター名です。||  
|/CLTWORKINGDIR<br /><br /> **省略可**|分散再生クライアント サービス用の作業ディレクトリです。|有効なパス|  
|/CLTRESULTDIR<br /><br /> **省略可**|分散再生クライアント サービス用の結果ディレクトリです。|有効なパス|  
  
### <a name="sample-syntax"></a>サンプル構文:  
 **分散再生コントローラー コンポーネントをインストールする場合**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **分散再生クライアント コンポーネントをインストールする場合**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
##  <a name="bkmk_configuration_file"></a> 構成ファイルを使用した 分散再生のインストール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップには、ユーザー入力およびシステムの既定値に基づいて構成ファイルを生成する機能が用意されています。 管理ツールをインストールするように指定すると、構成ファイルを使用して、3 つの 分散再生コンポーネント (管理ツール、分散再生コントローラー、および分散再生クライアント) を配置できます。 SQL Server セットアップでは、分散再生ユーティリティ コンポーネントのインストール、修復、およびアンインストールがサポートされています。  
  
 セットアップでは、コマンド ラインからのみ構成ファイルを使用できます。 以下に、構成ファイルを使用する際のパラメーターの処理順序について説明します。  
  
-   構成ファイルによって、パッケージの既定値が上書きされます。  
  
-   コマンド ライン値によって、構成ファイル内の値が上書きされます。  
  
 構成ファイルの使用方法の詳細については、「 [構成ファイルを使用した SQL Server 2016 のインストール](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)」を参照してください。  
  
> [!IMPORTANT]  
>  分散再生をインストールした後、コントローラー コンピューターとクライアント コンピューターのファイアウォール ルールを作成し、ターゲット サーバー上で各クライアント コンピューターの権限を付与する必要があります。 詳細については、「 [インストール後の手順の実行](../../tools/distributed-replay/complete-the-post-installation-steps.md)」を参照してください。  
  
#### <a name="to-generate-a-configuration-file"></a>構成ファイルを生成するには  
  
1.  セットアップ ウィザードに従って **[インストールの準備完了]** ページまで進みます。 構成ファイルのパスは、 **[インストールの準備完了]** ページの [構成ファイルのパス] セクションで指定します。  
  
2.  INI ファイルを生成するには、インストールを実際に完了しなくてもセットアップを取り消します。  
  
#### <a name="to-install-distributed-replay-using-the-configuration-file"></a>構成ファイルを使用して 分散再生をインストールするには  
  
-   コマンド プロンプトからインストールを実行し、ConfigurationFile パラメーターを使用して ConfigurationFile.ini を指定します。  
  
 **サンプル構文**  
  
 次の例では、コマンド プロンプトで構成ファイルを指定する方法を示しています。  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  構成ファイルでパスワードを構成することはできないため、コマンドラインで両方のパスワードを指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 の各エディションでサポートされる機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [分散再生の要件](../../tools/distributed-replay/distributed-replay-requirements.md)   
 [管理ツール コマンド ライン オプション &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Distributed Replay の構成](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
