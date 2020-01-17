---
title: アップグレードする SQL Server 2014 のインストール ウィザード (セットアップ) を使用して |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775408"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>インストール ウィザードを使用した SQL Server 2014 へのアップグレード (セットアップ)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードでは、1 つの機能ツリーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをアップグレードできます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を以前のバージョンと並列でインストールすることもできます。または、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から既存データベース設定と構成の設定を移行し、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスに適用することもできます。  
  
 詳細については、次のトピックをご覧ください。  
  
-   [サポートされているバージョンとエディションのアップグレード](supported-version-and-edition-upgrades.md)  
  
-   [SQL Server の複数のバージョンおよびインスタンスの使用](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [SQL Server フェールオーバー クラスター インスタンスのアップグレード &#40;セットアップ&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [コマンド プロンプトからの SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)  
  
-   [データベース コピー ウィザードの使用](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのアップグレードは、[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 を実行しているコンピューターではサポートされていません。 Server Core インストールの詳細については、次を参照してください。 [Server Core での SQL Server 2014 のインストール](install-sql-server-on-server-core.md)します。  
  
## <a name="prerequisites"></a>前提条件  
 セットアップは管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、リモート共有に対する読み取り権限と実行権限を持つ、ローカル管理者のドメイン アカウントを使用する必要があります。  
  
 アップグレードする前に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、次のトピックを確認してください。  
  
-   [SQL Server 2014 へのアップグレード](upgrade-sql-server.md)  
  
-   [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [システム構成チェッカーの検査パラメーター](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server データベース エンジンの旧バージョンとの互換性](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  アップグレードする機能は変更できず、アップグレード操作中に機能を追加することもできないことに注意してください。 アップグレード済みのインスタンスに機能を追加する方法の詳細についての[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]アップグレード操作が完了したらを参照してください。 [、インスタンスの SQL Server 2014 への機能の追加&#40;セットアップ&#41;](add-features-to-an-instance-of-sql-server-setup.md)します。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-upgrade-to-includesscurrentincludessscurrent-mdmd"></a>にアップグレードするには [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアを挿入し、ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。  
  
2.  インストール ウィザードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターが開始されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存のインスタンスをアップグレードするには、左側のナビゲーション領域の **[インストール]** をクリックし、 **[[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] からのアップグレード]** をクリックします。  
  
3.  [プロダクト キー] ページで、オプションをクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の無償のエディションにアップグレードするかどうか、または SQL Server の製品版の PID キーを持っているかどうかを指定します。 詳細については、次を参照してください。[エディションと SQL Server 2014 のコンポーネント](../../sql-server/editions-and-components-of-sql-server-2016.md)と[Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md)します。  
  
4.  [ライセンス条項] ページで使用許諾契約書を確認し、同意する場合は **[ライセンス条項に同意する]** チェック ボックスをオンにして、 **[次へ]** をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../includes/msconame-md.md)]に送信することもできます。  
  
5.  [グローバル ルール] ウィンドウ内で、ルール エラーが存在していない場合は、セットアップ手順は自動的に [製品の更新プログラム] ページに進みます。  
  
6.  [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update] ページは、コントロール パネルの [すべてのコントロール パネル項目] で [Windows Update]、[設定の変更] の順にクリックし、[ [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update] のチェック ボックスがオフになっている場合、次に表示されます。 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update] ページでチェック マークを付けると、Windows Update を調べるときに最新の更新プログラムが含まれるようにコンピューターの設定が変更されます。  
  
7.  [製品の更新プログラム] ページに、使用できる最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品の更新プログラムが表示されます。 更新プログラムを含めない場合は、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [製品の更新プログラムを含める]** チェック ボックスをオフにします。 製品の更新プログラムが検出されない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップではこのページは表示されず、 **[セットアップ ファイルのインストール]** ページに自動的に移動します。  
  
8.  [セットアップ ファイルのインストール] ページのセットアップには、セットアップ ファイルのダウンロード、抽出、およびインストールの進行状況が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの更新プログラムが検出され、含まれるように指定されている場合は、その更新プログラムもインストールされます。  
  
9. [アップグレード ルール] ウィンドウ内で、ルール エラーが存在していない場合は、セットアップ手順は自動的に [インスタンスの選択] ページに進みます。  
  
10. [インスタンスの選択] ページで、アップグレードする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。 管理ツールや共有機能をアップグレードするには、 **[共有機能のみをアップグレード]** を選択します。  
  
11. [機能の選択] ページでは、アップグレードする機能があらかじめ選択されています。 機能名を選択すると、右側のペインに各コンポーネント グループの説明が表示されます。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。  
  
    > [!NOTE]  
    >  **[インスタンスの選択]** ページで **[\<共有機能のみをアップグレード>]** を選択して、共有機能のアップグレードを選択した場合は、[機能の選択] ページのすべての共有機能があらかじめ選択されています。 すべての共有機能は同時にアップグレードされます。  
  
12. [インスタンスの構成] ページで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのインスタンス ID を指定します。  
  
     **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** ボックスに値を指定します。  
  
     すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack とアップグレードは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの各コンポーネントに適用されます。  
  
     **[インストール済みのインスタンス]** : セットアップを実行中のコンピューター上にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがグリッドに表示されます。 既定のインスタンスが既にコンピューターにインストールされている場合、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の名前付きインスタンスをインストールする必要があります。  
  
13. このトピックの残りの部分のワーク フローは、インストールするように指定した機能に応じて異なります。 選択した機能によっては、表示されないページもあります。  
  
14. [サーバーの構成 - サービス アカウント] ページには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの既定のサービス アカウントが表示されます。 このページで実際に構成するサービスは、アップグレードする機能によって異なります。  
  
     認証情報とログイン情報は、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスからそのまま移行されます。 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに同じログイン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 サービスを自動的に開始するか、手動で開始するか、または無効にするかを指定することもできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、サービス アカウントを個別に構成して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに、サービスでのタスクの実行に必要な最小権限が付与されるようにすることをお勧めします。 詳細については、「 [Windows サービス アカウントと権限の構成](../configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスに含まれるすべてのサービス アカウントに同じログイン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
     **セキュリティに関する注意** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのログイン情報を指定したら、 **[次へ]** をクリックします。  
  
15. [フルテキスト検索アップグレード オプション] ページで、アップグレードするデータベースのアップグレード オプションを指定します。 詳細については、「 [フルテキスト検索アップグレード オプション](../../sql-server/install/full-text-search-upgrade-options.md)」。  
  
16. すべてのルールに合格した場合は、[機能ルール] ウィンドウは自動的に進行します。  
  
17. [アップグレードの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[インストール]** をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
18. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、進行状況ページに状態が表示されます。  
  
19. インストールが終了すると、[完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
20. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのアップグレード後は、次の作業を実行します。  
  
-   **サーバーの登録**: アップグレードすると、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのレジストリ設定が削除されます。 アップグレード後、サーバーを再登録する必要があります。  
  
-   **統計の更新**: クエリ パフォーマンスを最適化するため、アップグレードに続いてすべてのデータベース上で統計を更新することをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのユーザー定義テーブル内の統計を更新するには、`sp_updatestats` ストアド プロシージャを使用します。  
  
-   **新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール内容の構成**: システムのセキュリティを向上させるため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、有効化できるようになっています。 外部からのアクセスの設定の詳細については、このリリースの Readme ファイルを参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 へのアップグレード](upgrade-sql-server.md)   
 [旧バージョンとの互換性](../../getting-started/backward-compatibility.md)  
  
  
