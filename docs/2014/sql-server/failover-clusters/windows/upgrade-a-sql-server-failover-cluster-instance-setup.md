---
title: SQL Server フェールオーバー クラスター インスタンスのアップグレード (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d018fb391c7633877f985b4e5e0798bfd803a5fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62680376"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>SQL Server フェールオーバー クラスター インスタンスのアップグレード (セットアップ)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] フェールオーバー クラスターにアップグレードするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用します。  
  
 フェールオーバー クラスターのアップグレードにおけるダウンタイムは、フェールオーバー時間およびアップグレード スクリプトの実行に必要な時間のみです。 フェールオーバー クラスターのローリング アップグレード プロセスに従えば、ダウンタイムを最小に抑えられます。 必須コンポーネントがフェールオーバー クラスター ノードにすべて揃っていない場合、必須コンポーネントのインストールに追加のダウンタイムが必要になります。 アップグレード中にダウンタイムを最小限に抑える方法の詳細については、次を参照してください。、[ベスト プラクティスのフェールオーバー クラスターのアップグレード前](#BestPractices)このページの「します。  
  
 アップグレードする方法の詳細については、次を参照してください。 [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)と[SQL Server 2014 にアップグレード](../../../database-engine/install-windows/upgrade-sql-server.md)します。  
  
 コマンド プロンプトを使用するためのサンプル構文の詳細については、次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
## <a name="prerequisites"></a>前提条件  
 作業を開始する前に、次の重要な情報を確認してください。  
  
-   [フェールオーバー クラスタリングをインストールする前に](../install/before-installing-failover-clustering.md)  
  
-   [アップグレード アドバイザーを使用したアップグレードの準備](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md)します。  
  
-   [データベース エンジンのアップグレード](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   セットアップでは、クラスター化されたオペレーティング システムに対して .NET Framework 4.0 がインストールされます。 ダウンタイムをできるだけ最小限に抑えるために、セットアップの実行前に .NET Framework 4.0 をインストールすることを検討してください。  
  
-   Visual Studio コンポーネントを適切にインストールできる状態にするために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は更新プログラムのインストールを要求します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは、更新プログラムが存在するかどうかを確認した後、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールを続行する前に更新プログラムをダウンロードしてインストールするよう要求します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップの中断を回避するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行する前に、以下の説明に従って更新プログラムをダウンロードおよびインストールします (または Windows Update に用意されている .NET 3.5 SP1 のすべての更新プログラムをインストールします)。  
  
     インストールする場合[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]、Windows Server 2008 SP2 オペレーティング システムでコンピューターから必要な更新プログラムを取得できます[ここ](https://go.microsoft.com/fwlink/?LinkId=198093)  
  
     [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] SP1 または [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 オペレーティング システム搭載のコンピューターに [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] をインストールする場合は、この更新プログラムが含まれています。  
  
-   .NET Framework 3.5 SP1 は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでインストールされなくなりましたが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] をインストールする際に必要になる場合があります。 詳細については、 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)][リリース ノート](https://go.microsoft.com/fwlink/?LinkId=296445)をインストールするには、Windows PowerShell が必要です。  
  
-   ローカルでのインストールの場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限を持つドメイン アカウントを使用する必要があります。  
  
-   インスタンスをアップグレードする[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]フェールオーバー クラスターでは、アップグレード中のインスタンスがフェールオーバー クラスターにある必要があります。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロンのインスタンスを [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] フェールオーバー クラスターに移動するには、新しく [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] フェールオーバー クラスターをインストールし、その後、データベース コピー ウィザードを使用してスタンドアロンのインスタンスからユーザー データベースを移行します。 詳細については、「 [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="rolling-upgrades"></a>ローリング アップグレード  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] にアップグレードするには、フェールオーバー クラスター ノードをパッシブ ノードから 1 つずつアップグレードする操作でセットアップを実行する必要があります。 各ノードをアップグレードする場合、ノードはフェールオーバー クラスターの実行可能な所有者から除外されます。 予期しないフェールオーバーが発生した場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセットアップによりクラスター リソース グループの所有権がアップグレード済みのノードに移動するまで、アップグレード済みのノードはフェールオーバーに関与しません。  
  
 既定では、セットアップに自動的に決定アップグレード済みのノードにフェールオーバーするときにします。 決定の際に基準になるのは、フェールオーバー クラスター インスタンス内のノード総数、およびアップグレード済みのノード数です。 半数のノード、または既にアップグレードされて、次のノードでアップグレードを実行するときに、セットアップはアップグレード済みのノードへのフェールオーバーとなります。 アップグレード済みのノードにフェールオーバーする際、クラスター グループはアップグレード済みのノードに移動します。 すべてのアップグレード済みノードは実行可能な所有者の一覧に格納され、まだアップグレードされていないすべてのノードは実行可能な所有者の一覧から削除されます。 残りの各ノードをアップグレードする場合、ノードはフェールオーバー クラスターの実行可能な所有者に追加されます。  
  
 ダウンタイムでのこのプロセス結果は、1 回のフェールオーバー時間、および全フェールオーバー クラスター アップグレード時のデータベース アップグレード スクリプトの実行時間に限定されます。  
  
 アップグレード プロセス中にクラスター ノードのフェールオーバーの動作を制御するには、コマンド プロンプトでアップグレード操作を実行して、/FAILOVERCLUSTERROLLOWNERSHIP パラメーターを使用します。 詳細については、「[コマンド プロンプトからの SQL Server 2014 のインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
 **注**、単一ノードのフェールオーバー クラスターがある場合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]セットアップでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]リソース グループがオフラインです。  
  
## <a name="considerations-when-upgrading-from-includessversion2005includesssversion2005-mdmd"></a>アップグレードする場合の考慮事項 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]  
 クラスターのセキュリティ ポリシーにドメイン グループを指定している場合は、[!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] でサービス SID を指定できません。 サービス SID を使用するには、サイド バイ サイド アップグレードを実行する必要があります。  
  
 選択すると[!INCLUDE[ssDE](../../../includes/ssde-md.md)]でインストールされたかどうかに関係なく、セットアップ時に、アップグレード、フルテキスト検索が含まれている[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]します。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] でフルテキスト検索を有効にしていた場合、セットアップでは、使用できるオプションに関係なくフルテキスト検索カタログが再構築されます。  
  
## <a name="upgrading-to-a-includesssql14includessssql14-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] マルチサブネット フェールオーバー クラスターへのアップグレード  
 想定されるアップグレード シナリオは 2 つあります。  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターが現在、単一のサブネットで構成されている場合:最初に、セットアップを開始してアップグレード プロセスに従って、既存のクラスターを [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] にアップグレードする必要があります。 既存のフェールオーバー クラスターのアップグレードの完了後に、AddNode 機能を使用して別のサブネット上のノードを追加します。 [クラスター ネットワークの構成] ページで、IP アドレス リソースの依存関係が OR に変更されていることを確認します。 これで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターが作成されます。  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターが現在、拡張 V-LAN テクノロジを使用して複数のサブネット上で構成されている場合:最初に既存のクラスターを [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] にアップグレードする必要があります。 拡張 V-LAN テクノロジでは単一のサブネットが構成されるため、ネットワーク構成を複数のサブネットに変更し、Windows フェールオーバー クラスター管理ツールを使用して IP アドレス リソースの依存関係を OR に変更する必要があります。  
  
###  <a name="BestPractices"></a> ベスト プラクティスをアップグレードする前に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]フェールオーバー クラスター  
 再起動による予期しないダウンタイムを回避するには、クラスター ノードでアップグレードを実行する前に、.NET Framework 4.0 の no-reboot パッケージをすべてのフェールオーバー クラスター ノードにあらかじめインストールしておきます。 前提条件をプレインストールする次の手順をお勧めします。  
  
-   .NET Framework 4.0 の no-reboot パッケージをインストールし、共有コンポーネントのみのアップブレードをパッシブ ノードから開始します。 これにより、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0、Windows インストーラー 4.5、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サポート ファイルがインストールされます。  
  
-   必要に応じて、1 回以上再起動します。  
  
-   アップグレード済みのノードにフェールオーバーします。  
  
-   最後に残ったノードで共有コンポーネントをアップグレードします。  
  
 すべての共有コンポーネントがアップグレードされ、必須コンポーネントがインストールされた後、フェールオーバー クラスター アップグレード プロセスを起動します。 まずをパッシブ ノードからなり、クラスター リソース グループを所有するノードに向かって各フェールオーバー クラスター ノードでアップグレードを実行する必要があります。  
  
-   既存のフェールオーバー クラスターに機能を追加することはできません。  
  
-   フェールオーバー クラスターのエディションの変更は、特定のシナリオに制限されています。 詳細については、「 [サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」をご覧ください。  
  
##  <a name="UpgradeSteps"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアップグレードするには  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアップグレードするには  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール メディアを挿入し、ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。 必須コンポーネントがインストールされていない場合は、インストールするように求められます。  
  
2.  > [!IMPORTANT]  
    >  手順 3. および 4. の詳細については、次を参照してください。、[ベスト プラクティスのフェールオーバー クラスターのアップグレード前](#BestPractices)セクション。  
  
3.  必須コンポーネントがインストールされると、インストール ウィザードによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが起動します。 既存のインスタンスをアップグレードする[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 をクリックして**からアップグレード[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]、または[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]します。**  
  
4.  セットアップ サポート ファイルが必要な場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによってインストールされます。 コンピューターの再起動を求めるメッセージが表示されたら、再起動してから続行します。  
  
5.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  [プロダクト キー] ページで、以前の製品バージョンのエディションに一致する新しいバージョンのエディション用の PID キーを入力します。 たとえば、エンタープライズ フェールオーバー クラスターをアップグレードするには、 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]用の PID キーを入力する必要があります。 **[次へ]** をクリックして次に進みます。 フェールオーバー クラスターのアップグレードに使用する PID キーは、同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス内のすべてのフェールオーバー クラスター ノードで一貫している必要があります。 詳細については、次を参照してください。[エディションと SQL Server 2014 のコンポーネント](../../editions-and-components-of-sql-server-2016.md)と[Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)します。  
  
7.  [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../../includes/msconame-md.md)]に送信することもできます。 **[次へ]** をクリックして次に進みます。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
8.  [インスタンスの選択] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にアップグレードする [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]インスタンスを指定します。 **[次へ]** をクリックして次に進みます。  
  
9. [機能の選択] ページでは、アップグレードする機能があらかじめ選択されています。 機能名を選択すると、右側のペインに各コンポーネント グループの説明が表示されます。 アップグレードする機能は変更できず、アップグレード操作中に機能を追加することもできないことに注意してください。 アップグレード済みのインスタンスに機能を追加する[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]アップグレード操作が完了したらを参照してください。 [、インスタンスの SQL Server 2014 への機能の追加&#40;セットアップ&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)します。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 SQL Server セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。  
  
10. フィールドが [インスタンスの構成] ページで以前のインスタンスから自動的に生成されます。 新しい InstanceID 値を指定することもできます。  
  
     **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** チェック ボックスをオンにして、値を指定します。 既定値をオーバーライドする場合、すべてのフェールオーバー クラスター ノードでアップグレードされたものと同じインスタンス ID を指定する必要があります。 アップグレード済みインスタンスのインスタンス ID は、すべてのノードに一致している必要があります。  
  
     **検出されたインスタンスと機能**-グリッドには、インスタンスが表示されます。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]セットアップが実行されているコンピューター上にあります。 **[次へ]** をクリックして次に進みます。  
  
11. [必要なディスク領域] ページでは、指定した機能に必要なディスク領域が計算され、セットアップを実行中のコンピューター上の空き領域と比較されます。  
  
12. [フルテキスト検索アップグレード] ページで、アップグレードするデータベースのアップグレード オプションを指定します。 詳細については、「 [フルテキスト検索アップグレード オプション](../../install/full-text-search-upgrade-options.md)」。  
  
13. **[エラー レポート]** ページで、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
14. アップグレード処理が開始される前に、システム構成チェッカーによって別のルール セットが実行され、コンピューターの構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
15. フェールオーバー クラスター インスタンス内のノードの一覧、および各ノードの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネントのインスタンスのバージョン情報が [クラスター アップグレード レポート] ページに表示されます。 また、データベース スクリプト状態およびレプリケーション スクリプト状態が表示されます。 さらに、 **[次へ]** をクリックしたときの動作についての情報メッセージも表示されます。 ノードの数を合計し、アップグレード済みのフェールオーバー クラスター ノードの数、によってセットアップがクリックしたときの動作を表示します**次**します。 必須コンポーネントをまだインストールしていない場合に生じ得る不要なダウンタイムについての警告も表示されます。  
  
16. [アップグレードの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[アップグレード]** をクリックします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
17. アップグレード中は、セットアップの進行に合わせてアップグレードの進行状況を監視できるように、[進行状況] ページに状態が表示されます。  
  
18. 現在のノードでアップグレードが終了すると、すべてのフェールオーバー クラスター ノード、各フェールオーバー クラスター ノードの機能、およびそのバージョン情報に関するアップグレード状態の情報が [クラスター アップグレード レポート] ページに表示されます。 表示されたバージョン情報を確認し、残りのノードでのアップグレードを続行します。 アップグレードしたノードでフェールオーバーが発生した場合は、状態ページを確認する作業も必要になります。 Windows クラスター アドミニストレーターのツールを使用して確認することもできます。  
  
19. アップグレードが終了すると、[完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
20. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
21. アップグレード プロセスを完了するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの他のすべてのノードで、手順 1. ～ 21. を繰り返します。  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターをアップグレードするには  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターにアップグレードするには (既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスターがマルチサブネット クラスターでない場合)  
  
1.  手順 1 で説明されている 24、 [SQL Server フェールオーバー クラスターをアップグレードする](#UpgradeSteps)にクラスターをアップグレードする前のセクション[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]します。  
  
2.  AddNode セットアップ操作を使用して別のサブネット上のノードを追加し、 **[クラスター ネットワークの構成]** ページで IP アドレス リソースの依存関係が OR になっていることを確認します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;Setup&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>拡張 V-LAN を現在使用しているマルチサブネット クラスターをアップグレードするには  
  
1.  手順 1 で説明されている 24、 [SQL Server フェールオーバー クラスターをアップグレードする](#UpgradeSteps)にクラスターをアップグレードする前のセクション[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]します。  
  
2.  ネットワーク設定を変更し、リモート ノードを別のサブネットに移動します。  
  
3.  Windows フェールオーバー クラスター管理ツールを使用して、IP アドレス リソースの依存関係が OR に設定された新しいサブネットの新しい IP アドレスを追加します。  
  
## <a name="next-steps"></a>次の手順  
 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]へのアップグレード後は、次の作業を実行します。  
  
-   サーバーを登録します。  
  
     アップグレードすると、以前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのレジストリ設定が削除されます。 アップグレード後、サーバーを再登録する必要があります。  
  
-   統計を更新します。  
  
     クエリ パフォーマンスを最適化するため、アップグレードに続いてすべてのデータベース上で統計を更新することをお勧めします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのユーザー定義テーブル内の統計を更新するには、**sp_updatestats** ストアド プロシージャを使用します。  
  
-   新しい構成[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インストール  
  
     システムのセキュリティを向上させるため、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、有効化できるようになっています。 外部からのアクセスの設定の詳細については、このリリースの Readme ファイルを参照してください。  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトから SQL Server 2014 をインストールします。](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
