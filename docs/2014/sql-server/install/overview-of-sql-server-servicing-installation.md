---
title: SQL Server のサービスのインストールの概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6a9fd19b-2367-4908-b638-363b1e929e1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8e9532c9d3ecbc32942e6a70d82f5837856a329
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093591"
---
# <a name="overview-of-sql-server-servicing-installation"></a>SQL Server サービスのインストールの概要
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サービス更新プログラムが適用された、インストール済みの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] コンポーネントに更新プログラムを適用できます。 既存の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] コンポーネントのバージョン レベルが更新のバージョン レベルより新しい場合、そのコンポーネントは、セットアップ プログラムによって自動的にアップデートから除外されます。 更新サービスを適用する方法の詳細についてを参照してください[SQL Server 2014 サービス更新プログラムのインストール](../../database-engine/install-windows/install-sql-server-servicing-updates.md)します。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする際は、次の点に注意してください。  
  
-   1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに属する機能はすべて同時にアップデートする必要があります。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]をアップデートする際に、同じ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの一部として [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がインストールされている場合は、それらのコンポーネントもアップデートする必要があります。 共有機能は、管理ツールなど、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、常に最新の更新プログラムで更新する必要があります。 機能ツリーで選択されていないコンポーネントまたはインスタンスは、更新されません。  
  
-   既定では、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新のログ ファイルは %program Files % に保存されます\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\LOG\\します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップでは、更新プログラムと元のメディアを統合して、元のメディアと更新プログラムを同時に実行できるようになりました。 詳細については、次を参照してください。 [SQL Server のインストールで新](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)します。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サービス更新プログラムを適用する前に、データのバックアップを検討することをお勧めします。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Update で入手できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを最新で安全な状態に保つために、更新プログラムを定期的に確認することをお勧めします。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の完全なインストールとして提供されています。 このリリースでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RTM インスタンスに適用される標準の修正プログラム実行可能パッケージとして Service Pack が提供されるのではなく、インストール パッケージ (2 ファイルで構成) が提供されます。 これを実行すると、SP1 がプレインストールされた状態で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスがインストールされます。  
  
## <a name="requirements-and-known-issues"></a>要件および既知の問題  
 パッケージをインストール、ダウンロード、および展開するために必要な推奨ディスク領域は、パッケージのサイズの約 2.5 倍です。 サービス パックのインストール後は、ダウンロードしたパッケージを削除できます。 一時ファイルは、すべて自動的に削除されます。  
  
 **既知の問題を確認してください。** 現在のリリースの既知の問題の詳細については、対応するリリースのノート トピックを参照してください。[SQL Server リリース ノート](https://msdn.microsoft.com/f617a0af-92dd-47aa-82c3-f51b1346bcd8)します。  
  
## <a name="installation-overview"></a>インストールの概要  
 ここでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の累積更新プログラムおよびサービス パックのインストール方法について、次の各操作を含めて説明します。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのインストールの準備  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのインストール  
  
-   サービスとアプリケーションの再起動  
  
### <a name="prepare-for-a-includesscurrentincludessscurrent-mdmd-update-installation"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのインストールの準備  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムをインストールする前に、次のように対処することを強くお勧めします。  
  
-   **バックアップ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]システム データベース**- をインストールする前に[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のバックアップを作成、更新プログラム、 `master`、 `msdb`、および`model`データベース。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムをインストールするとこれらのデータベースは変更され、以前のバージョンの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]と互換性がなくなります。 これらの更新プログラムが適用されていない [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を再インストールする場合には、これらのデータベースのバックアップ データが必要になります。  
  
     また、必要なユーザー データベースのバックアップも行ってください。  
  
    > [!IMPORTANT]  
    >  レプリケーション トポロジに含まれる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに更新プログラムを適用する場合は、適用前に、システム データベースに加えてレプリケートされたデータベースもバックアップする必要があります。  
  
-   **バックアップ、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース、構成ファイル、およびリポジトリ**- のインスタンスを更新する前に[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]次をバックアップする必要があります。  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース。 既定では、C:\Program Files にインストールされて\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12\< 。インスタンス Id > \OLAP\Data\\します。 WOW のインストールの既定のパスは C:\ProgramFiles (x86) \ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12\< 。インスタンス Id > \OLAP\Data\\します。  
  
    -   msmdsrv.ini 構成ファイル内の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の構成設定。 既定では、C:\Program Files 内にあるこれが\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12\< 。InstanceID > \OLAP\Config\ ディレクトリにあります。  
  
    -   (省略可) [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] リポジトリが格納されているデータベース。 この手順が必要になるのは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が Decision Support オブジェクト (DSO) ライブラリを使用するように構成された場合のみです。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース、構成ファイル、およびリポジトリをバックアップしなかった場合、更新された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスを以前のバージョンに戻すことはできなくなります。  
  
-   **システム データベースに十分な空き領域があることを確認**- の自動拡張オプションが選択されていない場合、`master`と`msdb`システム データベースでは、これらのデータベースにそれぞれ 500 KB 以上の空き領域の必要があります。 データベースに十分な空き領域があるかどうかを確認するには、`sp_spaceused` データベースと `master` データベースで `msdb` システム ストアド プロシージャを実行します。 いずれかのデータベースで未割り当て領域が 500 KB より少ない場合は、データベースのサイズを増やします。  
  
-   **サービスとアプリケーションを停止**、システムの再起動を避けるため、すべてのアプリケーションとサービスのインスタンスへの接続を停止する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードすると、インストールする前に[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新します。 これには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]および [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]も含まれます。 詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md) 」を参照してください。  
  
    > [!NOTE]  
    >  フェールオーバー クラスター環境ではサービスを停止できません。 詳細については、後のフェールオーバー クラスターのインストールに関するセクションを参照してください。  
  
-   更新プログラムのインストール後にコンピューターを再起動しなくてもいいように、セットアップではファイルをロックしているプロセスの一覧が表示されます。 更新プログラムのセットアップ プログラムで、インストール中にサービスを終了する必要がある場合は、インストールの完了後にそのサービスが再起動されます。  
  
-   セットアップで、インストール中にファイルがロックされていると認識された場合、インストール終了後にコンピューターの再起動が必要になることがあります。 再起動が必要な場合は、コンピューターの再起動を促すメッセージが表示されます。  
  
### <a name="install-includesscurrentincludessscurrent-mdmd-updates"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのインストール  
 ここでは、インストール プロセスについて説明します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムは、この更新プログラムをインストールするコンピューターに対して管理者特権があるアカウントでインストールする必要があります。 ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。  
  
#### <a name="starting-a-includesscurrentincludessscurrent-mdmd-update"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムの開始  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムをインストールするには、自己解凍形式のパッケージ ファイルを実行します。  
  
 累積更新プログラム パッケージ (CU):\<SQLServer2014>-KBxxxxxx-*PPP*.exe  
  
 サービス パック パッケージ (PCU):\<SQLServer2014>\<SPx> -KBxxxxxx-PPP-LLL.exe  
  
-   x はサービス パックの番号を表します。  
  
-   PPP は特定のプラットフォームを表します。  
  
-   Lll の文字の省略形、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などの言語。英語の場合は LLL は ENU です。  
  
 フェールオーバー クラスターに含まれる [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] コンポーネントに更新プログラムを適用するには、フェールオーバー クラスターのインストールに関するセクションを参照してください。 無人モードで更新プログラムのインストールを実行する方法の詳細については、次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
####  <a name="Slipstream"></a> 製品の更新プログラム[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]インストール  
 製品の更新プログラムは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップの機能です。 セットアップでは、メインの製品と使用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールを統合できます。 製品の更新プログラムは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Update、Windows Server Update Services (WSUS)、ローカル フォルダー、またはネットワーク共有を検索して、適切な更新プログラムを探します。  セットアップで最新バージョンの適用可能な更新プログラムが検出されると、ダウンロードが実行されて、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プロセスと統合されます。 製品の更新プログラムは、累積更新プログラム、サービス パック、またはサービス パックと累積更新プログラムに取り込むことができます。 製品の更新プログラム機能は、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1 で提供されていたスリップストリーム機能を拡張したものです。  
  
## <a name="updating-a-prepared-image-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の準備済みイメージの更新  
 未構成の準備済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの構成を完了しなくても、そのインスタンスに更新プログラムを適用できます。 準備済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに更新プログラムを適用するさまざまな方法について説明します。  
  
-   事前に準備された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを更新する。  
  
     準備済みインスタンスに対する更新プログラムは、構成前に適用することができます。 更新プログラム パッケージは、インスタンスが準備された状態であることを検出すると、その準備済みインスタンスに修正プログラムを適用します。その際、構成は完了しません。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update を使用して準備済みインスタンスを更新する。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Update を使用して、準備済み [!INCLUDE[msCoName](../../includes/msconame-md.md)] インスタンスに更新プログラムを適用できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update パッケージは、インスタンスが準備された状態であることを検出すると、その準備済みインスタンスに修正プログラムを適用します。その際、構成は完了しません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の準備済みイメージを更新している場合は、InstanceID パラメーターを指定する必要があります。 詳細およびサンプル構文については、「 [コマンド プロンプトからの更新プログラムのインストール](../../database-engine/install-windows/installing-updates-from-the-command-prompt.md)」を参照してください。  
  
## <a name="updating-a-completed-image-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の完了したイメージの更新  
 完了および構成済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを更新するには、インストールされているその他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスと同じプロセスに従います。  
  
## <a name="rebuilding-a-includesscurrentincludessscurrent-mdmd-failover-cluster-node"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] フェールオーバー クラスター ノードの再構築  
 更新プログラムの適用後にフェールオーバー クラスター内のノードを再構築する必要がある場合は、次の手順を実行します。  
  
1.  フェールオーバー クラスター内のノードを再構築します。 ノードの再構築の詳細については、「[フェールオーバー クラスター インスタンス障害からの復旧](../failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)」を参照してください。  
  
2.  元の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ プログラムを実行して、フェールオーバー クラスター ノードに [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をインストールします。  
  
3.  追加したノードに対して [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのセットアップを実行します。  
  
## <a name="restart-services-and-applications"></a>サービスとアプリケーションの再起動  
 セットアップ プログラムの完了時に、コンピューターの再起動が必要になる場合があります。 システムを再起動した後、または再起動を求められることなくセットアップ プログラムが終了した後は、コントロール パネルの **[サービス]** ノードを使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムの適用前に停止したサービスを再起動します。 たとえば、分散トランザクション コーディネーター サービスや [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search サービスのようなサービス、またはインスタンス固有のサービスなどを再起動します。  
  
 次に、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新プログラムのセットアップの実行前に終了したアプリケーションを再起動します。 インストールが正常に終了した直後に、アップグレード後の `master` データベース、`msdb` データベース、および `model` データベースをバックアップすることもお勧めします。  
  
## <a name="uninstalling-updates-from-includesscurrentincludessscurrent-mdmd"></a>更新プログラムのアンインストール [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 累積更新プログラムおよびサービス パックのアンインストールは、コントロール パネルの **[プログラムと機能]** で行うことができます。 インストールされた更新プログラムの一覧を表示するには、 **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をクリックします。 **[プログラム]** 、 **[プログラムと機能]** 、 **[インストールされた更新プログラムを表示]** の順にクリックして、[インストールされた更新プログラム] を開きます。 各累積更新プログラムは、個別に表示されています。 ただし、累積更新プログラムより新しいサービス パックがインストールされていると、累積更新プログラムの項目が表示されなくなるため、サービス パックをアンインストールしないと個別の項目を利用できません。  
  
 サービス パックおよび更新プログラムをアンインストールするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに適用されている最新のものから古いものへと順番に処理していってください。 以下の各例では、サービス パックおよび更新プログラムをアンインストールすることによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Cumulative Update 1 の状態になります。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスに Cumulative Update 1 および SP1 がインストールされている場合は、SP1 をアンインストールします。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスに Cumulative Update 1、SP1、および Cumulative Update 2 がインストールされている場合は、まず Cumulative Update 2 をアンインストールし、次に SP1 をアンインストールします。  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトから SQL Server 2014 をインストールします。](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 サービス更新プログラムをインストールします。](../../database-engine/install-windows/install-sql-server-servicing-updates.md)   
 [SQL Server のインストールの検証](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
