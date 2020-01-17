---
title: SQL Server 2016 をインストール ウィザードからインストールする (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 32f7c238a08a7da31d455421ca9fc00d0f8d6bdb
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962370"
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>SQL Server をインストール ウィザードからインストールする (セットアップ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、インストール ウィザードを使用して SQL Server をインストールする方法について説明します。 これは [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] および [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)] に適用されます。

この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ インストール ウィザードを使って [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスをインストールする手順について詳しく説明します。 インストール ウィザードでは、1 つの機能ツリーを使用してすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをインストールできるため、それらを個別にインストールする必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントを個別にインストールするには、「[SQL Server をインストールする](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components)」を参照してください。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする他の方法については、以下を参照してください。  

* [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
* [構成ファイルを使用した SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
* [SysPrep を使用した SQL Server のインストール](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
* [新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
* [インストール ウィザードを使用した SQL Server のアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

## <a name="get-the-installation-media"></a>インストール メディアを入手する

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>Prerequisites

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする前に、「[SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)」を確認してください。  
  
> [!NOTE]  
> ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。  

::: monikerRange=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

###  <a name="bkmk_ga_instalpatch"></a> インストールのパッチ要件

SQL Server 2016 および 2017 の前提条件としてインストールされる Microsoft Visual C++ 2013 ランタイム バイナリに問題が見つかりました。 更新プログラムを利用してこの問題を修正できます。 Visual C++ ランタイム バイナリに対するこの更新プログラムをインストールしないと、特定のシナリオにおいて、SQL Server で安定性の問題が発生する可能性があります。 SQL Server をインストールする前に、「[SQL Server リリース ノート](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)」にある手順に従って、ご使用のコンピューターに Visual C++ ランタイム バイナリのパッチが必要かどうかを確認してください。 

これは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] には適用されません。

## <a name="to-install-sql-server-2016-and-2017"></a>SQL Server 2016 および 2017 をインストールするには  

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの **Setup.exe**をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、**Setup.exe** をダブルクリックします。  
  
1. インストール ウィザードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターが実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインストールを作成するには、左側のナビゲーション領域の **[インストール]** を選択し、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** を選択します。  

1. **[プロダクト キー]** ページで、オプションを選択して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の無償のエディション、または PID キーを持つ製品版のどちらをインストールするかを指定します。 詳しくは、「[SQL Server 2017 の各エディションとサポートされている機能](../../sql-server/editions-and-components-of-sql-server-2017.md)」をご覧ください。  
  
   続けるには、 **[次へ]** を選択します。

1. **[ライセンス条項]** ページで、ライセンス条項を確認します。 同意する場合は、 **[ライセンス条項に同意します]** チェック ボックスをオンして、 **[次へ]** を選択します。  

   >[!NOTE]
   > SQL Server は、インストールの状態に関する情報および製品の機能向上に役立つその他の利用状況データとパフォーマンス データを送信します。 SQL Server のデータ処理とプライバシー管理の詳細については、「[プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」および「[SQL Server を構成して Microsoft にフィードバックを送信する](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016)」を参照してください。

1. **[グローバル ルール]** ウィンドウでは、ルール エラーがない場合は、セットアップは自動的に **[製品の更新プログラム]** ページに進みます。  
  
1. **[コントロール パネル]**  >  **[すべてのコントロール パネル項目]**  >  **[Windows Update]**  >  **[設定の変更]** で **[Microsoft Update]** チェック ボックスがオフになっている場合は、次に **[Microsoft Update]** ページが表示されます。 **[Microsoft Update]** チェック ボックスをオンにすると、Windows 更新プログラムをスキャンするときに、すべての Microsoft 製品の最新の更新プログラムを含めるように、コンピューターの設定が変更されます。  

1. **[製品の更新プログラム]** ページに、使用できる最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品の更新プログラムが表示されます。 製品の更新プログラムが検出されない場合、セットアップではこのページは表示されず、 **[セットアップ ファイルのインストール]** ページに自動的に移動します。  

1. **[セットアップ ファイルのインストール]** ページのセットアップには、セットアップ ファイルのダウンロード、抽出、およびインストールの進行状況が表示されます。 セットアップの更新プログラムが検出され、それを含むように指定してある場合は、その更新プログラムもインストールされます。 更新プログラムが見つからない場合、セットアップが自動的に進行します。
  
1. **[インストール ルール]** ページでは、セットアップの実行中に発生する可能性がある潜在的な問題に関するチェックが行われます。 エラーが発生した場合、詳細な情報を見るには、 **[状態]** 列の項目を選択します。 その以外の場合は、 **[次へ]** を選択します。

1. コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を初めてインストールする場合は、 **[インストールの種類]** ページがスキップされて、直接 **[機能の選択]** ページに移動します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシステムに既にインストールされている場合は、 **[インストールの種類]** ページで、新規インストールを実行するか、既存のインストール環境に機能を追加するかを選択できます。 続けるには、 **[次へ]** を選択します。
  
1. **[機能の選択]** ページで、インストールするコンポーネントを選択します。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]の新しいインスタンスをインストールするには、 **[データベース エンジン サービス]** を選択します。

    機能名を選択すると、 **[機能の説明]** ペインに各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできます。 詳細については、[SQL Server 2016 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2016.md)に関するセクション、または [SQL Server 2017 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2017.md)に関するセクションを参照してください。
  
     選択した機能の必須コンポーネントが、 **[選択した機能に必要なコンポーネント]** ペインに表示されます。 セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントがインストールされます。  
  
     **[機能の選択]** ページの下部にあるフィールドを使用して、共有コンポーネントのカスタム ディレクトリを指定することもできます。 共有コンポーネントのインストール パスを変更するには、ダイアログ ボックスの下部にあるフィールドのパスを更新するか、 **[参照]** を選択してインストール ディレクトリに移動します。 既定のインストール パスは [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]です。  
  
     > [!NOTE]
     > 共有コンポーネントには絶対パスを指定する必要があります。 フォルダーを圧縮または暗号化しないでください。 マップされたドライブはサポートされていません。  
  
     SQL Server は、共有機能の 2 つのディレクトリを使用します。
  
     * 共有機能ディレクトリ  
     * 共有機能ディレクトリ (x86)  
  
     > [!NOTE]
     > 前の各オプションには異なるパスを指定する必要があります。  
  
1. すべてのルールに合格した場合、 **[機能ルール]** ページは自動的に進行します。  
  
1. **[インスタンスの構成]** ページで、既定のインスタンスまたは名前付きインスタンスをインストールするかどうかを指定します。 詳細については、「[インスタンスの構成](../../sql-server/install/instance-configuration.md#instance-configuration-page)」を参照してください。  
  
     * **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 この ID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 既定のインスタンスの場合も名前付きインスタンスの場合も、同じ動作が発生します。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** テキスト ボックスで異なる値を指定します。  
  
       > [!NOTE]  
       > [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の標準的なスタンドアロン インスタンスでは、既定のインスタンスの場合も名前付きインスタンスの場合も、インスタンス ID の値として既定値以外は使用しないでください。  
  
       すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack とアップグレードが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの各コンポーネントに適用されます。  
  
     * **[インストール済みのインスタンス]** : セットアップが実行されているコンピューター上にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが、グリッドに表示されます。 既定のインスタンスが既にコンピューターにインストールされている場合、 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]の名前付きインスタンスをインストールする必要があります。  
  
     インストールの残りの部分のワークフローは、インストールするように指定した機能に応じて異なります。 選択によっては、表示されないページもあります。 

1. Polybase 機能をインストールすることを選択すると、 **[インスタンスの構成]** ページの後に表示される SQL Server の設定に **[PolyBase の構成]** ページが追加されます。 PolyBase には、Oracle JRE 7 更新プログラム 51 (少なくとも) が必要です。これがまだインストールされていない場合、インストールはブロックされます。 **[PolyBase の構成]** ページでは、SQL Server をスタンドアロンの Polybase 対応インスタンスとして使用するか、それともこの SQL Server を PolyBase スケールアウト グループの一部として使用するかを選択できます。 スケールアウト グループを使用することを選択した場合は、最大 6 つ以上のポートのポート範囲を指定する必要があります。 


1. **[サーバーの構成] - [サービス アカウント]** ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。 構成設定の詳細については、「[インストール ウィザードのヘルプ](../../sql-server/install/instance-configuration.md#serverconfig)」を参照してください。
  
     すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに同じログオン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 サービスを自動的に開始するか、手動で開始するか、または無効にするかを指定することもできます。 サービス アカウントを個別に構成し、各サービスに最低限の特権を提供することをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに、タスクの実行に必要な最小値のアクセス許可を付与します。 詳細については、「[Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのインスタンスに含まれるすべてのサービス アカウントに同じログオン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービス アカウントで[データベースのファイル瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を使用するには、 **[SQL Server データベース エンジン サービスにボリューム メンテナンス タスクを実行する特権を付与する]** チェック ボックスをオンにします。
  
1. **[サーバーの構成 - 照合順序]** ページを使用して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に既定以外の照合順序を指定します。    

   既定のインストール設定はオペレーティング システム (OS) ロケールによって決定されます。 サーバーレベルの照合順序はセットアップ中に変更するか、インストール前に OS ロケールを変更することで変更できます。 既定の照合順序は、特定のロケール別に関連付けられている中で最も古いバージョンに設定されます。 これは下位互換性によるものです。 そのため、これが常に推奨される照合順序になるとは限りません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を活用するには、Windows 照合順序を使用するように既定のインストール設定を変更します。 たとえば、OS のロケールが**英語 (米国)** (コード ページ 1252) の場合、セットアップ中、既定の照合順序は **SQL_Latin1_General_CP1_CI_AS** になります。これは Windows 照合順序でそれに最も近い **Latin1_General_100_CI_AS_SC** に変更できます。

   詳細については、「[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
1. **[データベース エンジンの構成 - サーバーの構成]** ページを使用して、次のオプションを指定します。  
  
    * **セキュリティ モード**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対して **Windows 認証**または**混合モード認証**を選択します。 **混合モード認証**を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力する必要があります。  
  
       デバイスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との接続を正常に確立した後のセキュリティ メカニズムは、Windows 認証モードでも混合モード認証でも同じです。 詳細については、「[[データベース エンジンの構成] - [サーバー構成] ページ](../../sql-server/install/instance-configuration.md#serverconfig)」を参照してください。
  
    * **SQL サーバー管理者**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの 1 人以上のシステム管理者を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** を選択します。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** を選択し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
     **[データベース エンジンの構成] - [データ ディレクトリ]** ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** を選択します。  
  
    > [!IMPORTANT]  
    > 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  
  
     詳細については、「[[データベース エンジンの構成] - [データ ディレクトリ] ページ](../../sql-server/install/instance-configuration.md#datadir)」を参照してください。

     **[データベース エンジンの構成] - [TempDB]** ページを使用して、ファイル サイズ、ファイルの数、既定以外のインストール ディレクトリ、および **tempdb** のファイル拡張設定を構成します。 詳細については、「[[データベース エンジンの構成] - [TempDB] ページ](../../sql-server/install/instance-configuration.md#tempdb)」を参照してください。 

 
     **[データベース エンジンの構成] - [FILESTREAM]** ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対する FILESTREAM を有効にします。 詳細については、「[[データベース エンジンの構成] - [FILESTREAM] ページ](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page)」を参照してください。  
  
1. **[Analysis Services の構成] - [アカウントの準備]** ページを使用して、サーバー モードと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザーまたはアカウントを指定します。 サーバー モードによって、サーバーで使用されるメモリとストレージ サブシステムが決まります。 サーバー モードによって、実行されるソリューションの種類も異なります。 サーバーで多次元キューブ データベースを実行する場合は、既定のサーバー モード オプション **[多次元およびデータ マイニング モード]** を選択します。

    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のシステム管理者を少なくとも 1 人指定する必要があります。

    * SQL Server セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** を選択します。

    * システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** を選択し、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。

    サーバー モードと管理者権限の詳細については、「[[Analysis Services の構成] - [アカウントの準備] ページ](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page)」を参照してください。

    一覧の編集が完了したら、 **[OK]** を選択します。 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** を選択します。

    **[Analysis Services の構成] - [データ ディレクトリ]** ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** を選択します。  

    > [!IMPORTANT]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールするときに、INSTANCEDIR と SQLUSERDBDIR に同じディレクトリ パスを指定した場合、SQL Server エージェントとフルテキスト検索は、アクセス許可がないために開始されません。  
    >  
    > 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  

    詳細については、「[[Analysis Service の構成] - [データ ディレクトリ] ページ](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page)」を参照してください。  

1. **[Distributed Replay Controller Configuration]\(分散再生コントローラーの構成\)** ページを使用して、分散再生コントローラー サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生コントローラー サービスへの無制限のアクセス許可が与えられます。  
  
     * SQL Server のセットアップを実行しているユーザーに、分散再生コントローラー サービスに対するアクセス許可を付与するには、 **[現在のユーザーの追加]** ボタンを選択します。

     * 他のユーザーに、分散再生コントローラー サービスに対するアクセス許可を付与するには、 **[追加]** ボタンを選択します。

     * 分散再生コントローラー サービスからアクセス許可を削除するには、 **[削除]** ボタンを選択します。

     * 続けるには、 **[次へ]** を選択します。  
  
1. **[Distributed Replay Client Configuration]\(分散再生クライアントの構成\)** ページを使用して、分散再生クライアント サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生クライアント サービスへの無制限のアクセス許可が与えられます。  
  
     * **[コントローラー名]** は省略可能です。 既定値は \<*空白*> です。 分散再生クライアント サービスと通信するクライアント コンピューターであるコントローラーの名前を入力します。  
  
       * コントローラーを既にセットアップしてある場合は、各クライアントを構成するときにコントローラーの名前を入力します。  
  
       * コントローラーをまだセットアップしていない場合は、コントローラー名を空白にしておくことができます。 ただし、コントローラー名を **クライアント構成** ファイルに手動で入力する必要があります。  
  
     * 分散再生クライアント サービス用の **[作業ディレクトリ]** を指定します。 既定の作業ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\ です。  
  
     * 分散再生クライアント サービス用の **[結果ディレクトリ]** を指定します。 既定の結果ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\ です。  
  
     * 続けるには、 **[次へ]** を選択します。  
  
1. **[インストールの準備完了]** ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 このページで、セットアップは**製品の更新プログラム**機能が有効/無効であるか、および最終バージョンの更新プログラムであるかどうかを示します。  
  
     続行するには、 **[インストール]** を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、選択した機能の必須の前提条件が最初にインストールされた後、選択した機能がインストールされます。  
  
1. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、 **[インストールの進行状況]** ページに状態の更新が表示されます。  
  
1. インストールが終了すると、 **[完了]** ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。
  
    > [!IMPORTANT]
    > セットアップが完了した時点で、インストール ウィザードからのメッセージを確認します。 詳細については、「[SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** を選択します。  
  
1. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
## <a name="to-install-sql-server-2019"></a>SQL Server 2019 をインストールするには 
  
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの **Setup.exe**をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、**Setup.exe** をダブルクリックします。  
  
1. インストール ウィザードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターが実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインストールを作成するには、左側のナビゲーション領域の **[インストール]** を選択し、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** を選択します。  

1. **[プロダクト キー]** ページで、オプションを選択して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の無償のエディション、または PID キーを持つ製品版のどちらをインストールするかを指定します。 詳しくは、「[SQL Server 2017 の各エディションとサポートされている機能](../../sql-server/editions-and-components-of-sql-server-2017.md)」をご覧ください。  
  
   続けるには、 **[次へ]** を選択します。

  
1. **[ライセンス条項]** ページで、ライセンス条項を確認します。 同意する場合は、 **[ライセンス条項と[プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)に同意します]** チェック ボックスをオンして、 **[次へ]** を選択します。  

   >[!NOTE]
   > SQL Server は、インストールの状態に関する情報および製品の機能向上に役立つその他の利用状況データとパフォーマンス データを送信します。 SQL Server のデータ処理とプライバシー管理の詳細については、「[プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」および「[SQL Server を構成して Microsoft にフィードバックを送信する](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016)」を参照してください。

1. **[グローバル ルール]** ウィンドウでは、ルール エラーがない場合は、セットアップは自動的に **[製品の更新プログラム]** ページに進みます。  
  
1. **[コントロール パネル]**  >  **[すべてのコントロール パネル項目]**  >  **[Windows Update]**  >  **[設定の変更]** で **[Microsoft Update]** チェック ボックスがオフになっている場合は、次に **[Microsoft Update]** ページが表示されます。 **[Microsoft Update]** チェック ボックスをオンにすると、Windows 更新プログラムをスキャンするときに、すべての Microsoft 製品の最新の更新プログラムを含めるように、コンピューターの設定が変更されます。  

1. **[製品の更新プログラム]** ページに、使用できる最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品の更新プログラムが表示されます。 製品の更新プログラムが検出されない場合、セットアップではこのページは表示されず、 **[セットアップ ファイルのインストール]** ページに自動的に移動します。  

1. **[セットアップ ファイルのインストール]** ページのセットアップには、セットアップ ファイルのダウンロード、抽出、およびインストールの進行状況が表示されます。 セットアップの更新プログラムが検出され、それを含むように指定してある場合は、その更新プログラムもインストールされます。 更新プログラムが見つからない場合、セットアップが自動的に進行します。
  
1. **[インストール ルール]** ページでは、セットアップの実行中に発生する可能性がある潜在的な問題に関するチェックが行われます。 エラーが発生した場合、詳細な情報を見るには、 **[状態]** 列の項目を選択します。 その以外の場合は、 **[次へ]** を選択します。

1. コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を初めてインストールする場合は、 **[インストールの種類]** ページがスキップされて、直接 **[機能の選択]** ページに移動します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシステムに既にインストールされている場合は、 **[インストールの種類]** ページで、新規インストールを実行するか、既存のインストール環境に機能を追加するかを選択できます。 続けるには、 **[次へ]** を選択します。
  
1. **[機能の選択]** ページで、インストールするコンポーネントを選択します。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]の新しいインスタンスをインストールするには、 **[データベース エンジン サービス]** を選択します。

    機能名を選択すると、 **[機能の説明]** ペインに各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできます。 詳細については、[SQL Server 2016 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2016.md)に関するセクション、または [SQL Server 2017 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2017.md)に関するセクションを参照してください。
  
     選択した機能の必須コンポーネントが、 **[選択した機能に必要なコンポーネント]** ペインに表示されます。 セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントがインストールされます。  
  
     **[機能の選択]** ページの下部にあるフィールドを使用して、共有コンポーネントのカスタム ディレクトリを指定することもできます。 共有コンポーネントのインストール パスを変更するには、ダイアログ ボックスの下部にあるフィールドのパスを更新するか、 **[参照]** を選択してインストール ディレクトリに移動します。 既定のインストール パスは [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]です。  
  
     > [!NOTE]
     > 共有コンポーネントには絶対パスを指定する必要があります。 フォルダーを圧縮または暗号化しないでください。 マップされたドライブはサポートされていません。  
  
     SQL Server は、共有機能の 2 つのディレクトリを使用します。
  
     * 共有機能ディレクトリ  
     * 共有機能ディレクトリ (x86)  
  
     > [!NOTE]
     > 前の各オプションには異なるパスを指定する必要があります。  
  
1. すべてのルールに合格した場合、 **[機能ルール]** ページは自動的に進行します。  
  
1. **[インスタンスの構成]** ページで、既定のインスタンスまたは名前付きインスタンスをインストールするかどうかを指定します。 詳細については、「[インスタンスの構成](../../sql-server/install/instance-configuration.md#instance-configuration-page)」を参照してください。  
  
     * **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 この ID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 既定のインスタンスの場合も名前付きインスタンスの場合も、同じ動作が発生します。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** テキスト ボックスで異なる値を指定します。  
  
       > [!NOTE]  
       > [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の標準的なスタンドアロン インスタンスでは、既定のインスタンスの場合も名前付きインスタンスの場合も、インスタンス ID の値として既定値以外は使用しないでください。  
  
       すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack とアップグレードが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの各コンポーネントに適用されます。  
  
     * **[インストール済みのインスタンス]** : セットアップが実行されているコンピューター上にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが、グリッドに表示されます。 既定のインスタンスが既にコンピューターにインストールされている場合、 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]の名前付きインスタンスをインストールする必要があります。  
  
     インストールの残りの部分のワークフローは、インストールするように指定した機能に応じて異なります。 選択によっては、表示されないページもあります。 

1. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、Polybase の機能をインストールする前に、コンピューターに (少なくとも) Oracle JRE 7 Update 51 を事前にインストールしておく必要がなくなりました。 Polybase 機能をインストールすることを選択すると、 **[インスタンスの構成]** ページの後に表示される SQL Server の設定に **[Java のインストール場所]** ページが追加されます。 [Java のインストール場所] ページでは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] のインストールに含まれる Azul Zulu Open JRE をインストールすることも、コンピューターに既にインストールされている別の JRE または JDK の場所を指定することも選択できます。

1. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、言語拡張機能と共に Java が追加されています。 Java 機能をインストールすることを選択すると、SQL Server 設定ダイアログ ウィンドウに **[Java のインストール場所]** ページが追加されます。このページは、 **[インスタンスの構成]** ページの後に表示されます。 **[Java のインストール場所]** ページでは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] のインストールに含まれる Zulu Open JRE をインストールすることも、コンピューターに既にインストールされている別の JRE または JDK の場所を指定することも選択できます。

1. **[サーバーの構成] - [サービス アカウント]** ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。 構成設定の詳細については、「[インストール ウィザードのヘルプ](../../sql-server/install/instance-configuration.md#serverconfig)」を参照してください。
  
     すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに同じログオン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 サービスを自動的に開始するか、手動で開始するか、または無効にするかを指定することもできます。 サービス アカウントを個別に構成し、各サービスに最低限の特権を提供することをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに、タスクの実行に必要な最小値のアクセス許可を付与します。 詳細については、「[Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのインスタンスに含まれるすべてのサービス アカウントに同じログオン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービス アカウントで[データベースのファイル瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を使用するには、 **[SQL Server データベース エンジン サービスにボリューム メンテナンス タスクを実行する特権を付与する]** チェック ボックスをオンにします。
  
     **[サーバーの構成] - [照合順序]** ページを使用して、[!INCLUDE[ssDE](../../includes/ssde-md.md)]および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に既定以外の照合順序を指定します。 詳細については、「[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
1. **[データベース エンジンの構成 - サーバーの構成]** ページを使用して、次のオプションを指定します。  
  
    * **セキュリティ モード**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対して **Windows 認証**または**混合モード認証**を選択します。 **混合モード認証**を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力する必要があります。  
  
       デバイスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との接続を正常に確立した後のセキュリティ メカニズムは、Windows 認証モードでも混合モード認証でも同じです。 詳細については、「[[データベース エンジンの構成] - [サーバー構成] ページ](../../sql-server/install/instance-configuration.md#serverconfig)」を参照してください。
  
    * **SQL サーバー管理者**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの 1 人以上のシステム管理者を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** を選択します。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** を選択し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
     **[データベース エンジンの構成] - [データ ディレクトリ]** ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** を選択します。  
  
    > [!IMPORTANT]  
    > 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  
  
     詳細については、「[[データベース エンジンの構成] - [データ ディレクトリ] ページ](../../sql-server/install/instance-configuration.md#datadir)」を参照してください。

     **[データベース エンジンの構成] - [TempDB]** ページを使用して、ファイル サイズ、ファイルの数、既定以外のインストール ディレクトリ、および **tempdb** のファイル拡張設定を構成します。 詳細については、「[[データベース エンジンの構成] - [TempDB] ページ](../../sql-server/install/instance-configuration.md#tempdb)」を参照してください。

     **[[!INCLUDE[ssDE](../../includes/ssde-md.md)]の構成 - MaxDOP]** ページを使用して、並列処理の最大限度を指定します。 この設定により、1 つのステートメントが実行中に使用できるプロセッサの数が決まります。 推奨値はインストール時に自動的に計算されます。 
     
    > [!NOTE]  
    > このページは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降のセットアップでのみ使用できます。 
    
    詳細については、「[[データベース エンジンの構成] - [MAXDOP] ページ](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)」を参照してください。 

     **[データベース エンジンの構成] - [メモリ]** ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのインスタンスで起動後に使用される**最小サーバー メモリ**および**最大サーバー メモリ**の値を指定します。 **[推奨]** オプションを選択した後、既定値を使用するか、計算された推奨値を使用するか、独自の値を手動で指定することができます。
     
    > [!NOTE]  
    > このページは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降のセットアップでのみ使用できます。 
    
    詳細については、「[[データベース エンジンの構成] - [メモリ] ページ](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)」を参照してください。 

     **[データベース エンジンの構成] - [FILESTREAM]** ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対する FILESTREAM を有効にします。 詳細については、「[[データベース エンジンの構成] - [FILESTREAM] ページ](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page)」を参照してください。  
  
1. **[Analysis Services の構成] - [アカウントの準備]** ページを使用して、サーバー モードと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザーまたはアカウントを指定します。 サーバー モードによって、サーバーで使用されるメモリとストレージ サブシステムが決まります。 サーバー モードによって、実行されるソリューションの種類も異なります。 サーバーで多次元キューブ データベースを実行する場合は、既定のサーバー モード オプション **[多次元およびデータ マイニング モード]** を選択します。

    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のシステム管理者を少なくとも 1 人指定する必要があります。

    * SQL Server セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** を選択します。

    * システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** を選択し、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。

    サーバー モードと管理者権限の詳細については、「[[Analysis Services の構成] - [アカウントの準備] ページ](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page)」を参照してください。

    一覧の編集が完了したら、 **[OK]** を選択します。 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** を選択します。

    **[Analysis Services の構成] - [データ ディレクトリ]** ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** を選択します。  

    > [!IMPORTANT]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールするときに、INSTANCEDIR と SQLUSERDBDIR に同じディレクトリ パスを指定した場合、SQL Server エージェントとフルテキスト検索は、アクセス許可がないために開始されません。  
    >  
    > 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  

    詳細については、「[[Analysis Service の構成] - [データ ディレクトリ] ページ](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page)」を参照してください。  

1. **[Distributed Replay Controller Configuration]\(分散再生コントローラーの構成\)** ページを使用して、分散再生コントローラー サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生コントローラー サービスへの無制限のアクセス許可が与えられます。  
  
     * SQL Server のセットアップを実行しているユーザーに、分散再生コントローラー サービスに対するアクセス許可を付与するには、 **[現在のユーザーの追加]** ボタンを選択します。

     * 他のユーザーに、分散再生コントローラー サービスに対するアクセス許可を付与するには、 **[追加]** ボタンを選択します。

     * 分散再生コントローラー サービスからアクセス許可を削除するには、 **[削除]** ボタンを選択します。

     * 続けるには、 **[次へ]** を選択します。  
  
1. **[Distributed Replay Client Configuration]\(分散再生クライアントの構成\)** ページを使用して、分散再生クライアント サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生クライアント サービスへの無制限のアクセス許可が与えられます。  
  
     * **[コントローラー名]** は省略可能です。 既定値は \<*空白*> です。 分散再生クライアント サービスと通信するクライアント コンピューターであるコントローラーの名前を入力します。  
  
       * コントローラーを既にセットアップしてある場合は、各クライアントを構成するときにコントローラーの名前を入力します。  
  
       * コントローラーをまだセットアップしていない場合は、コントローラー名を空白にしておくことができます。 ただし、コントローラー名を **クライアント構成** ファイルに手動で入力する必要があります。  
  
     * 分散再生クライアント サービス用の **[作業ディレクトリ]** を指定します。 既定の作業ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\ です。  
  
     * 分散再生クライアント サービス用の **[結果ディレクトリ]** を指定します。 既定の結果ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\ です。  
  
     * 続けるには、 **[次へ]** を選択します。  
  
1. **[インストールの準備完了]** ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 このページで、セットアップは**製品の更新プログラム**機能が有効/無効であるか、および最終バージョンの更新プログラムであるかどうかを示します。  
  
     続行するには、 **[インストール]** を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、選択した機能の必須の前提条件が最初にインストールされた後、選択した機能がインストールされます。  
  
1. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、 **[インストールの進行状況]** ページに状態の更新が表示されます。  
  
1. インストールが終了すると、 **[完了]** ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。
  
    > [!IMPORTANT]
    > セットアップが完了した時点で、インストール ウィザードからのメッセージを確認します。 詳細については、「[SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** を選択します。  
  
1. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。

::: moniker-end

## <a name="next-steps"></a>次の手順

[新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールを構成します。](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-instances-sql-server?view=sql-server-2017)  
  
システムのセキュリティを向上させるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、有効化できるようになっています。 詳細については、「[セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照
  
* [SQL Server のインストールの検証](../../database-engine/install-windows/validate-a-sql-server-installation.md)  
* [失敗した SQL Server のインストールの修復](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)
* [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
* [インストール ウィザードを使用した SQL Server のアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 
