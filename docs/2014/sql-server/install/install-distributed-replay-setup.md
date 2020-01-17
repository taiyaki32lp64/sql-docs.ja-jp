---
title: 分散再生 (セットアップ) のインストール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5b2b43d899041d501039ade4d0493a7fdbf0164
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094626"
---
# <a name="install-distributed-replay-setup"></a>分散再生のインストール (セットアップ)
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
  
-   使用するコンピューターが、「 [分散再生の要件](../../tools/sql-server-profiler/replay-requirements.md)」に記載されている前提条件を満たしていることを確認します。  
  
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
  
     C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- または -  
  
     \<共有機能ディレクトリ (x86)>\Tools\\(ユーザーが指定した代替の共有機能 (x86) ディレクトリ)  
  
### <a name="to-install-distributed-replay-features"></a>分散再生機能をインストールするには  
  
1.  分散再生の機能のインストールを開始するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを開始します。  
  
2.  **[セットアップ サポート ルール]** ページでは、SQL Server セットアップ サポート ファイルをインストールするときに発生する可能性がある問題が特定されています。 セットアップを続行する前に、セットアップ サポートの失敗を修正する必要があります。  
  
3.  **[プロダクト キー]** ページでオプション ボタンをクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の無償のエディション、または PID キーを持つ製品版のどちらをインストールするかを指定します。 詳細については、次を参照してください。[エディションと SQL Server 2014 のコンポーネントの](../editions-and-components-of-sql-server-2016.md)します。  
  
4.  **[ライセンス条項]** ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../includes/msconame-md.md)]に送信することもできます。  
  
5.  **[セットアップ サポート ファイル]** ページで **[インストール]** をクリックして、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のセットアップ サポート ファイルをインストールまたは更新します。  
  
6.  **[セットアップ ロール]** ページで、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール**をクリックし、 **[次へ]** をクリックして **[機能の選択]** ページに進みます。  
  
7.  **[機能の選択]** ページで、どの機能をインストールするかを設定します。  
  
    -   管理ツールをインストールするには、 **[管理ツール - 基本]** を選択します。  
  
    -   コントローラー サービスをインストールするには、 **[分散再生コントローラー]** を選択します。  
  
    -   クライアント サービスをインストールするには、 **[分散再生クライアント]** を選択します。  
  
     **重要な**:分散再生コント ローラーを構成するときに、分散再生クライアント サービスの実行に使用される 1 つまたは複数のユーザー アカウントを指定できます。 サポートされているアカウントの一覧を次に示します。  
  
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
  
 以下の追加のトピックでは、分散再生をインストールする他の方法が記載されています。  
  
-   [コマンド プロンプトからの分散再生のインストール](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [構成ファイルを使用した分散再生のインストール](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 分散再生の機能をインストールするには、管理権限が必要です。 sysadmin 権限を持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのみが、テスト サーバーの sysadmin サーバー ロールにクライアント サービス アカウントを追加できます。 Distributed Replay のセキュリティ上の考慮事項の詳細については、「 [Distributed Replay のセキュリティ](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 のエディションでサポートされる機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [分散再生の要件](../../tools/sql-server-profiler/replay-requirements.md)   
 [管理ツール コマンド ライン オプション &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Distributed Replay の構成](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
