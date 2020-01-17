---
title: 新しい SQL Server フェールオーバー クラスターの作成 (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- adding nodes
- failover clustering [SQL Server], creating clusters
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- clusters [SQL Server], creating
- removing nodes
ms.assetid: 30e06a7d-75e9-44e2-bca3-b3b0c4a33f61
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02cb0eb53ee8561884799c3a5e4f4f44eb5ff752
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893183"
---
# <a name="create-a-new-sql-server-failover-cluster-setup"></a>新しい SQL Server フェールオーバー クラスターの作成 (セットアップ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールまたはアップグレードするには、フェールオーバー クラスターの各ノードでセットアップ プログラムを実行する必要があります。 既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターにノードを追加するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスに追加するノードで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行する必要があります。 他のノードを管理するアクティブなノードでは、セットアップを実行しないでください。  
  
 ノードがクラスター化される方法に応じて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターは次のように構成されます。  
  
-   ノードが同じサブネットまたは同じサブネットのセットにある場合 - IP アドレス リソースの依存関係が AND に設定されます。  
  
-   ノードが異なるサブネット上にある場合 - IP アドレス リソースの依存関係が OR に設定されます。この構成は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスター構成と呼ばれます。 詳細については、「 [SQL Server マルチサブネット クラスタリング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターには、次のインストール オプションがあります。  
  
 **オプション 1: ノードの追加を伴う統合インストール**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 統合フェールオーバー クラスター インストールは、次の手順で構成されています。  
  
-   単一ノードの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスを作成および構成します。 ノードの構成が正常に完了すると、完全に機能するフェールオーバー クラスター インスタンスが完成します。 フェールオーバー クラスターには 1 つのノードしかないので、この時点では高可用性は備わっていません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに追加する各ノードで、セットアップを実行し、ノードの追加機能を使用して、ノードを追加します。  
  
    -   追加するノードに追加サブネットまたは異なるサブネットがある場合は、セットアップで追加の IP アドレスを指定できます。 追加するノードが別のサブネット上にある場合は、IP アドレス リソース依存関係が OR に変更されることも確認する必要があります。 ノードの追加操作時に発生する可能性のあるさまざまなシナリオの詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」をご覧ください。  
  
 **オプション 2: 高度/エンタープライズ インストール**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 高度/エンタープライズ フェールオーバー クラスター インストールは、次の手順で構成されています。  
  
-   新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの実行可能な所有者となる各ノードで、「 [準備](#prepare)」セクションに記載されたフェールオーバー クラスター セットアップの準備手順を実行します。 1 つのノードでフェールオーバー クラスター セットアップの準備が完了すると、指定したすべての設定を含む Configuration.ini ファイルが作成されます。 他のノードで準備を行うときには、同じ手順を実行する代わりに、最初のノードから自動生成された Configuration.ini ファイルを、セットアップ コマンド 詳細については、「 [構成ファイルを使用した SQL Server 2016 のインストール](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)」を参照してください。 この手順ではノードのクラスター化の準備を行いますが、この手順が終了しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスは操作できません。  
  
-   ノードをクラスタリング用に準備した後、準備されたいずれかのノードでセットアップを実行します。 この手順で、フェールオーバー クラスター インスタンスを構成し、完了します。 この手順が終了すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスが操作できるようになり、そのインスタンスに対して事前に準備されたすべてのノードが、新しく作成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの実行可能な所有者となります。  
  
     複数のサブネット上のノードをクラスター化している場合、セットアップによって、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で準備されたフェールオーバー クラスター インスタンスを持つすべてのノードのすべてのサブネットの和集合が検出されます。 サブネットに複数の IP アドレスを指定することができます。 準備された各ノードは、少なくとも 1 つの IP アドレスを持つ実行可能な所有者であることが必要となります。  
  
     サブネットに指定された各 IP アドレスが、準備されたすべてのノードでサポートされている場合、依存関係は AND に設定されます。  
  
     サブネットに指定された各 IP アドレスが、準備されたすべてのノードでサポートされていない場合、依存関係は OR に設定されます。 詳細については、「 [SQL Server マルチサブネット クラスタリング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)」を参照してください。  
  
    > [!NOTE]  
    >  フェールオーバー クラスターの実行機能には、基になる Windows フェールオーバー クラスターが必要です。 Windows フェールオーバー クラスターが存在しない場合、セットアップはエラーとなって終了します。  
  
 既存のフェールオーバー クラスター インスタンスにノードを追加する方法と、既存のフェールオーバー クラスター インスタンスからノードを削除する方法の詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除&#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」をご覧ください。  
  
 リモート インストールの詳細については、「[サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」をご覧ください。  
  
 Windows フェールオーバー クラスターへの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインストールの詳細については、「 [SQL Server Analysis Services をクラスター化する方法](https://go.microsoft.com/fwlink/p/?LinkId=396548)」をご覧ください。  
  
## <a name="prerequisites"></a>Prerequisites  
 作業を開始する前に、次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックのトピックを参照してください。  
  
-   [SQL Server のインストール計画](../../../sql-server/install/planning-a-sql-server-installation.md)  
  
-   [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [SQL Server インストールにおけるセキュリティの考慮事項](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server マルチサブネット クラスタリング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行する前に、クラスター アドミニストレーター内の共有ドライブの場所をメモしてください。 この情報は、新しいフェールオーバー クラスターを作成するときに必要になります。  
  
### <a name="to-install-a-new-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-integrated-install-with-add-node"></a>ノードの追加を伴う統合インストールを使用して新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールするには  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール メディアを挿入し、ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。 必須コンポーネントをインストールする方法の詳細については、「 [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」をご覧ください。  
  
2.  インストール ウィザードで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが開始されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の新しいクラスター インストールを行うには、インストール ページで **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [フェールオーバー クラスターの新規インストール]** をクリックします。  
  
3.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
4.  続行するには、 **[次へ]** をクリックします。  
  
5.  [セットアップ サポート ファイル] ページで **[インストール]** をクリックして、セットアップ サポート ファイルをインストールします。  
  
6.  セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 確認が完了したら、 **[次へ]** をクリックして続行します。 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
7.  [プロダクト キー] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の無償のエディションをインストールするかどうか、または SQL Server の製品版の PID キーを持っているかどうかを指定します。 詳細については、「 [SQL Server 2016 のエディションとコンポーネント](../../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
8.  [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../../includes/msconame-md.md)]に送信することもできます。 **[次へ]** をクリックして次に進みます。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
9. [機能の選択] ページで、インストールするコンポーネントを選択します。 機能名を選択すると、右側のペインに各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできますが、フェールオーバー クラスタリングをサポートしているのは [!INCLUDE[ssDE](../../../includes/ssde-md.md)]、テーブル モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 、および多次元モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] だけです。 他のコンポーネントをオンにした場合、それらのコンポーネントは、セットアップを実行している現在のノードでフェールオーバー機能のないスタンドアロン機能として実行されます。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] モードの詳細については、「 [Analysis Services インスタンスのサーバー モードの決定](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)」をご覧ください。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。  
  
     このページの下部にあるフィールドを使用して、共有コンポーネントのカスタム ディレクトリを指定できます。 共有コンポーネントのインストール パスを変更するには、ダイアログ ボックスの下部に示されているフィールドのパスを更新するか、参照ボタンをクリックしてインストール ディレクトリに移動します。 既定のインストール パスは、C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \\です。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、システム データベース (Master、Model、MSDB、および TempDB) と [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のユーザー データベースをサーバー メッセージ ブロック (SMB) ファイル共有にインストールすることもできます。 SMB ファイル共有をストレージとして使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールの詳細については、「 [SQL Server をストレージ オプションとして SMB ファイル共有にインストールする](../../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)」をご覧ください。  
  
     共有コンポーネントには絶対パスを指定する必要があります。 フォルダーを圧縮または暗号化しないでください。 マップされたドライブはサポートされていません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を 64 ビット オペレーティング システムにインストールしている場合は、次のオプションが表示されます。  
  
    1.  共有機能ディレクトリ  
  
    2.  共有機能ディレクトリ (x86)  
  
     前の各オプションには異なるパスを指定する必要があります。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] サービス機能をオンにすると、レプリケーションとフルテキスト検索の両方が自動的にオンになります。 Data Quality Services (DQS) は、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] サービス機能を選択したときにも選択されます。 これらのサブ機能をいずれかをオフにすると、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] サービス機能もオフになります。  
  
10. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによって、構成を検証するために選択した機能に基づく別のルール セットが実行されます。  
  
11. [インスタンスの構成] ページで、既定のインスタンスまたは名前付きインスタンスをインストールするかどうかを指定します。 詳細については、「 [Instance Configuration](../../install/instance-configuration.md)」を参照してください。  
  
     **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [ネットワーク名]** : 新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターのネットワーク名を指定します。 これは、ネットワーク上でフェールオーバー クラスターを識別するために使用される名前です。  
  
    > [!NOTE]  
    >  このネットワーク名は、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターでは、仮想 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 名と呼ばれていました。  
  
     **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** ボックスを選択して、値を指定します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の標準的なスタンドアロン インスタンスでは、既定のインスタンスの場合も名前付きインスタンスの場合も、 **[インスタンス ID]** ボックスの値として既定値以外は使用しません。  
  
     **[インスタンス ルート ディレクトリ]** : 既定では、インスタンス ルート ディレクトリは、C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\ になります。 既定以外のルート ディレクトリを指定するには、表示されたフィールドを使用するか、参照ボタンをクリックしてインストール フォルダーを検索します。  
  
     **検出された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [インスタンスとこのコンピューターの機能]** : セットアップを実行中のコンピューター上にある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスがグリッドに表示されます。 既定のインスタンスが既にコンピューターにインストールされている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の名前付きインスタンスをインストールする必要があります。 **[次へ]** をクリックして次に進みます。  
  
12. [クラスター リソース グループ] ページを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仮想サーバー リソースが配置されるクラスター リソース グループ名を指定します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター リソース グループ名を指定するには、2 つのオプションがあります。  
  
    -   ドロップダウン リストを使用して、使用する既存のグループを指定します。  
  
    -   作成する新しいグループの名前を入力します。 "使用可能記憶域" という名前はグループ名として有効ではないことに注意してください。  
  
13. [クラスター ディスクの選択] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの共有クラスター ディスク リソースを選択します。 クラスター ディスクは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データが配置される場所です。 複数のディスクを指定できます。 [使用可能な共有ディスク] グリッドには、使用可能なディスクの一覧、各ディスクが共有ディスクに適しているかどうか、および各ディスク リソースの説明が表示されます。 **[次へ]** をクリックして次に進みます。  
  
    > [!NOTE]  
    >  最初のドライブはすべてのデータベースの既定のドライブとして使用されますが、これは [!INCLUDE[ssDE](../../../includes/ssde-md.md)] または [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 構成ページで変更できます。  
    >   
    >  SMB ファイル共有をデータ フォルダーとして使用する場合は、[クラスター ディスクの選択] ページで共有ディスクの選択を省略できます。  
  
14. [クラスター ネットワークの構成] ページで、次のように、フェールオーバー クラスター インスタンスのネットワーク リソースを指定します。  
  
    -   **[ネットワークの設定]** - フェールオーバー クラスター インスタンスの IP の種類と IP アドレスを指定します。  
  
     **[次へ]** をクリックして次に進みます。  
  
15. このページでクラスターのセキュリティ ポリシーを指定します。  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 以降のバージョン: サービス SID (サーバー セキュリティ ID) が推奨設定であり、既定の設定です。 これをセキュリティ グループに変更することはできません。 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]のサービス SID 機能については、「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」をご覧ください。 これは、 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]のスタンドアロンおよびクラスター セットアップでテストが行われています。  
  
    -   [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスにドメイン グループを指定します。 すべてのリソースの権限は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがグループ メンバーとして含まれる、ドメイン レベルのグループによって制御されます。  
  
     **[次へ]** をクリックして次に進みます。  
  
16. このトピックの残りの部分のワーク フローは、インストールするように指定した機能に応じて異なります。 選択した機能 ([!INCLUDE[ssDE](../../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]) によっては、表示されないページもあります。  
  
17. [サーバーの構成 - サービス アカウント] ページで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。  
  
     すべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスに同じログイン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 スタートアップの種類は、すべてのクラスター対応サービス (フルテキスト検索および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントを含む) に対して手動に設定され、インストール時に変更することはできません。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、各サービスに最小の権限を与えるためにはサービス アカウントを個別に構成することをお勧めします。サービス アカウントを個別に構成すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスには、サービスでのタスクの実行に必要な最小権限が付与されます。 詳細については、「 [サーバー構成 - サービス アカウント](https://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) 」および「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のこのインスタンスに含まれるすべてのサービス アカウントに同じログオン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
     **セキュリティに関する注意** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン情報を指定したら、 **[次へ]** をクリックします。  
  
18. **[サーバーの構成 - 照合順序]** タブを使用して、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] および [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]に既定以外の照合順序を指定します。  
  
19. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [の構成 - アカウントの準備] ページを使用して、次の項目を指定します。  
  
    -   [セキュリティ モード] : [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス用に Windows 認証または混合モード認証を選択します。 混合モード認証を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力する必要があります。  
  
         デバイスが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]との接続を正常に確立した後のセキュリティ メカニズムは Windows 認証モード、混合モードのどちらの場合も同じです。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [管理者] - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスの 1 人以上のシステム管理者を指定する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
     一覧の編集が完了したら、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
20. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 データ ディレクトリは、フェールオーバー クラスターの共有クラスター ディスク上に配置されるようにしてください。  
  
    > [!NOTE]  
    >  サーバー メッセージ ブロック (SMB) ファイル サーバーをデータ ディレクトリとして指定するには、 **\Servername\ShareName** ... の形式で \\既定のデータ ルート ディレクトリ\\をファイル共有に指定します。  
   
21. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [の構成 - FILESTREAM] ページを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対する FILESTREAM を有効にします。 **[次へ]** をクリックして次に進みます。  
  
22. [[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の構成 - アカウントの準備] ページを使用して、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザーまたはアカウントを指定します。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のシステム管理者を少なくとも 1 人指定する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の管理者権限を持つユーザー、グループ、またはコンピューターの一覧を編集します。
  
     一覧の編集が完了したら、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
23. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 データ ディレクトリは、フェールオーバー クラスターの共有クラスター ディスク上に配置されるようにしてください。  
   
24. 作成する [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インストールの種類を指定するには、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [の構成] ページを使用します。 フェールオーバー クラスター インストールの場合、このオプションは未構成の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インストールに設定されます。 インストールの完了後に、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービスを構成する必要があります。  
  
 
25. システム構成チェッカーによって別のルール セットが実行され、構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
26. [インストールの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[インストール]** をクリックします。 セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
27. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、[インストールの進行状況] ページに状態が表示されます。  
  
28. インストールが終了すると、 **[完了]** ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
29. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」をご覧ください。  
  
30. 作成した単一ノードのフェールオーバーにノードを追加するには、追加する各ノードでセットアップを実行し、AddNode 操作の手順に従います。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
    > [!NOTE]  
    >  複数のノードを追加する場合には、構成ファイルを使用してインストールを配置できます。 詳細については、「 [構成ファイルを使用した SQL Server 2016 のインストール](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)」を参照してください。  
    >   
    >  インストールする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エディションは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター内のすべてのノードで一致している必要があります。 既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに新しいノードを追加する場合は、エディションが既存のフェールオーバー クラスターのエディションと一致するように指定してください。  
  
##  <a name="prepare"></a> 準備  
  
#### <a name="advancedenterprise-failover-cluster-install-step-1-prepare"></a>高度/エンタープライズ フェールオーバー クラスターのインストール手順 1: 準備  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール メディアを挿入し、ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。 必須コンポーネントをインストールする方法の詳細については、「 [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」をご覧ください。 必須コンポーネントがインストールされていない場合は、インストールするように求められます。  
  
2.  Windows インストーラー 4.5 が必要です。これはインストール ウィザードによってインストールされます。 コンピューターの再起動を促すメッセージが表示された場合は、再起動してから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを再実行します。  
  
3.  必須コンポーネントがインストールされると、インストール ウィザードによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが起動します。 クラスタリングに対してノードを準備するには、 **[詳細設定]** ページに移動し、 **[高度なクラスターの準備]** をクリックします。  
  
4.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
5.  [セットアップ サポート ファイル] ページで **[インストール]** をクリックして、セットアップ サポート ファイルをインストールします。  
  
6.  セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 確認が完了したら、 **[次へ]** をクリックして続行します。 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
7.  ローカライズされたオペレーティング システムでのインストールで、インストール メディアに英語とそのオペレーティング システムに対応する言語の両方の言語パックが含まれている場合は、[言語の選択] ページで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの言語を指定できます。 言語間サポートとインストールに関する注意点の詳細については、「 [SQL Server のローカル言語版](../../../sql-server/install/local-language-versions-in-sql-server.md)」を参照してください。  
  
     続行するには、 **[次へ]** をクリックします。  
  
8.  [プロダクト キー] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の無償のエディションをインストールするかどうか、または SQL Server の製品版の PID キーを持っているかどうかをクリックして指定します。 詳細については、「 [SQL Server 2016 のエディションとコンポーネント](../../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
    > [!NOTE]  
    >  同じフェールオーバー クラスターに対して準備するすべてのノードで、同じプロダクト キーを指定する必要があります。  
  
9. [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../../includes/msconame-md.md)]に送信することもできます。 **[次へ]** をクリックして次に進みます。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
10. [機能の選択] ページで、インストールするコンポーネントを選択します。 機能名を選択すると、右側のペインに各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできますが、フェールオーバー クラスタリングをサポートしているのは [!INCLUDE[ssDE](../../../includes/ssde-md.md)]、テーブル モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 、および多次元モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] だけです。 他のコンポーネントをオンにした場合、それらのコンポーネントは、セットアップを実行している現在のノードでフェールオーバー機能のないスタンドアロン機能として実行されます。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] モードの詳細については、「 [Analysis Services インスタンスのサーバー モードの決定](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)」をご覧ください。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。  
  
     このページの下部にあるフィールドを使用して、共有コンポーネントのカスタム ディレクトリを指定できます。 共有コンポーネントのインストール パスを変更するには、ダイアログ ボックスの下部に示されているフィールドのパスを更新するか、参照ボタンをクリックしてインストール ディレクトリに移動します。 既定のインストール パスは、C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\です。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] サービス機能をオンにすると、レプリケーションとフルテキスト検索の両方が自動的にオンになります。 これらのサブ機能をいずれかをオフにすると、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] サービス機能もオフになります。  
  
11. [インスタンスの構成] ページで、既定のインスタンスまたは名前付きインスタンスをインストールするかどうかを指定します。
  
     **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** ボックスを選択して、値を指定します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の標準的なスタンドアロン インスタンスでは、既定のインスタンスの場合も名前付きインスタンスの場合も、 **[インスタンス ID]** ボックスの値として既定値以外は使用しないでください。  
  
    > [!IMPORTANT]  
    >  フェールオーバー クラスターに対して準備されるすべてのノードに対して同じインスタンス ID を使用してください。  
  
     **[インスタンス ルート ディレクトリ]** : 既定では、インスタンス ルート ディレクトリは、C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\ になります。 既定以外のルート ディレクトリを指定するには、表示されたフィールドを使用するか、参照ボタンをクリックしてインストール フォルダーを検索します。  
  
     **[インストール済みのインスタンス]** : セットアップを実行中のコンピューター上にある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスがグリッドに表示されます。 既定のインスタンスが既にコンピューターにインストールされている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の名前付きインスタンスをインストールする必要があります。 **[次へ]** をクリックして次に進みます。  
  
12. [必要なディスク領域] ページでは、指定した機能に必要なディスク領域が計算され、セットアップを実行中のコンピューター上の空き領域と比較されます。  
  
13. このページでクラスターのセキュリティ ポリシーを指定します。  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 以降のバージョン: サービス SID (サーバー セキュリティ ID) が推奨設定であり、既定の設定です。 これをセキュリティ グループに変更することはできません。 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]のサービス SID 機能については、「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」をご覧ください。 これは、 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]のスタンドアロンおよびクラスター セットアップでテストが行われています。  
  
    -   [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスにドメイン グループを指定します。 すべてのリソースの権限は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがグループ メンバーとして含まれる、ドメイン レベルのグループによって制御されます。  
  
     **[次へ]** をクリックして次に進みます。  
  
14. このトピックの残りの部分のワーク フローは、インストールするように指定した機能に応じて異なります。 選択した機能によっては、表示されないページもあります。  
  
15. [サーバーの構成 - サービス アカウント] ページで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。  
  
     すべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスに同じログイン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 スタートアップの種類は、すべてのクラスター対応サービス (フルテキスト検索および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントを含む) に対して手動に設定され、インストール時に変更することはできません。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、各サービスに最小の権限を与えるためにはサービス アカウントを個別に構成することをお勧めします。サービス アカウントを個別に構成すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスには、サービスでのタスクの実行に必要な最小権限が付与されます。 詳細については、「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のこのインスタンスに含まれるすべてのサービス アカウントに同じログオン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
     **セキュリティに関する注意** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン情報を指定したら、 **[次へ]** をクリックします。  
  
16. **[サーバーの構成 - 照合順序]** タブを使用して、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] および [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]に既定以外の照合順序を指定します。  
  
17. **[サーバーの構成 - FILESTREAM]** ページを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対する FILESTREAM を有効にします。  **[次へ]** をクリックして次に進みます。  
  
18. 作成する [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インストールの種類を指定するには、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [の構成] ページを使用します。 フェールオーバー クラスター インストールの場合、このオプションは未構成の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インストールに設定されます。 インストールの完了後に、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービスを構成する必要があります。  
   
19. [エラー レポート] ページで、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
20. システム構成チェッカーによって別のルール セットが実行され、構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
21. [インストールの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[インストール]** をクリックします。 セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
     インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、[インストールの進行状況] ページに状態が表示されます。 インストールが終了すると、 **[完了]** ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。  
  
22. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
23. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」をご覧ください。  
  
24. 前の手順を繰り返して、フェールオーバー クラスターの他のノードを準備します。 自動生成された構成ファイルを使用して他のノードの準備を行うこともできます。 詳細については、「 [構成ファイルを使用した SQL Server 2016 のインストール](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)」を参照してください。  
  
## <a name="complete"></a>[完了]  
  
#### <a name="advancedenterprise-failover-cluster-install-step-2-complete"></a>高度/エンタープライズ フェールオーバー クラスターのインストール手順 2: [完了]  
  
1.  [準備手順](#prepare)に示されたとおりにすべてのノードの準備を終えたら、準備したノードのいずれかでセットアップを実行します。可能であれば、共有ディスクを所有するノードで実行します。 **インストール センターの** [詳細設定] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ページで、 **[高度なクラスター構成の完了]** をクリックします。  
  
2.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
3.  [セットアップ サポート ファイル] ページで **[インストール]** をクリックして、セットアップ サポート ファイルをインストールします。  
  
4.  セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 確認が完了したら、 **[次へ]** をクリックして続行します。 画面に詳細を表示するには、 **[詳細の表示]** をクリックするか、または **[詳細レポートの表示]** をクリックして HTML レポートを表示します。  
  
5.  ローカライズされたオペレーティング システムでのインストールで、インストール メディアに英語とそのオペレーティング システムに対応する言語の両方の言語パックが含まれている場合は、[言語の選択] ページで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの言語を指定できます。 言語間サポートとインストールに関する注意点の詳細については、「 [SQL Server のローカル言語版](../../../sql-server/install/local-language-versions-in-sql-server.md)」を参照してください。  
  
     続行するには、 **[次へ]** をクリックします。  
  
6.  [クラスター ノードの構成] ページを使用して、クラスタリングに対して準備されたインスタンス名を選択し、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターのネットワーク名を指定します。 これは、ネットワーク上でフェールオーバー クラスターを識別するために使用される名前です。  
  
    > [!NOTE]  
    >  このネットワーク名は、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターでは、仮想 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 名と呼ばれていました。  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによって、構成を検証するために選択した機能に基づく別のルール セットが実行されます。  
  
8.  [クラスター リソース グループ] ページを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仮想サーバー リソースが配置されるクラスター リソース グループ名を指定します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター リソース グループ名を指定するには、 次の 2 つの方法があります。  
  
    -   リストを使用して、使用する既存のグループを指定します。  
  
    -   作成する新しいグループの名前を入力します。 "使用可能記憶域" という名前はグループ名として有効ではないことに注意してください。  
  
9. [クラスター ディスクの選択] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの共有クラスター ディスク リソースを選択します。 クラスター ディスクは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データが配置される場所です。 複数のディスクを指定できます。 [使用可能な共有ディスク] グリッドには、使用可能なディスクの一覧、各ディスクが共有ディスクに適しているかどうか、および各ディスク リソースの説明が表示されます。 **[次へ]** をクリックして次に進みます。  
  
    > [!NOTE]  
    >  最初のドライブはすべてのデータベースの既定のドライブとして使用されますが、これは [!INCLUDE[ssDE](../../../includes/ssde-md.md)] または [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 構成ページで変更できます。  
  
10. [クラスター ネットワークの構成] ページで、次のように、フェールオーバー クラスター インスタンスのネットワーク リソースを指定します。  
  
    -   **[ネットワークの設定]** : フェールオーバー クラスター インスタンスのすべてのノードおよびサブネットについて IP の種類と IP アドレスを指定します。 マルチサブネット フェールオーバー クラスターの場合は複数の IP アドレスを指定できますが、サポートされる IP アドレスは、1 つのサブネットにつき 1 つだけです。 準備の対象となるすべてのノードは、少なくとも 1 つの IP アドレスを所有している必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター内に複数のサブネットが存在する場合、IP アドレス リソースの依存関係を OR に設定するように求められます。  
  
     **[次へ]** をクリックして次に進みます。  
  
11. このトピックの残りの部分のワーク フローは、インストールするように指定した機能に応じて異なります。 選択した機能によっては、表示されないページもあります。  
  
12. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [の構成 - アカウントの準備] ページを使用して、次の項目を指定します。  
  
    -   [セキュリティ モード] : [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス用に Windows 認証または混合モード認証を選択します。 混合モード認証を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力する必要があります。  
  
         デバイスが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]との接続を正常に確立した後のセキュリティ メカニズムは Windows 認証モード、混合モードのどちらの場合も同じです。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [管理者] - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスの 1 人以上のシステム管理者を指定する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
     一覧の編集が完了したら、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
13. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 データ ディレクトリは、フェールオーバー クラスターの共有クラスター ディスク上に配置されるようにしてください。  
  
  
14. [[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の構成 - アカウントの準備] ページを使用して、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザーまたはアカウントを指定します。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のシステム管理者を少なくとも 1 人指定する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の管理者権限を持つユーザー、グループ、またはコンピューターの一覧を編集します。  
  
     一覧の編集が完了したら、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
15. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 データ ディレクトリは、フェールオーバー クラスターの共有クラスター ディスク上に配置されるようにしてください。  
  
  
16. システム構成チェッカーによって別のルール セットが実行され、構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
17. [インストールの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[インストール]** をクリックします。 セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
18. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、[インストールの進行状況] ページに状態が表示されます。  
  
19. インストールが終了すると、 **[完了]** ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。 この手順により、同じフェールオーバー クラスターに対して準備されたすべてのノードが、完成した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの一部となります。  
  
## <a name="next-steps"></a>Next Steps  
 **新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール内容の構成**: システムのセキュリティを向上させるため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、有効化できるようになっています。 詳細については、「 [Surface Area Configuration](../../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
 ログ ファイルの場所の詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトからの SQL Server 2016 のインストール](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
