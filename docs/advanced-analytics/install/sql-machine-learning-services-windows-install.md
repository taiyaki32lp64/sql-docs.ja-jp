---
title: Windows へのインストール
description: この記事では、Windows に SQL Server Machine Learning Services をインストールする方法について説明します。 Machine Learning Services を使用して、データベース内で Python または R スクリプトを実行できます。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 8d51c147cfe5895356f8af270f62443643caa8f1
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727644"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-windows"></a>Windows に SQL Server Machine Learning Services (Python と R) をインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、Windows に SQL Server Machine Learning Services をインストールする方法について説明します。 Machine Learning Services を使用して、データベース内で Python または R スクリプトを実行できます。

## <a name="bkmk_prereqs"> </a> インストール前のチェックリスト

+ データベース エンジンのインスタンスが必要です。 R または Python の機能だけをインストールすることはできませんが、既存のインスタンスにそれらを段階的に追加することはできます。

+ ビジネス継続性のために、Machine Learning Services では [Always On 可用性グループ](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)がサポートされています。 各ノードに Machine Learning Services をインストールし、パッケージを構成する必要があります。

+ Machine Learning Services のインストールは、SQL Server 2017 のフェールオーバー クラスターでは*サポートされていません*。 ただし、SQL Server 2019 では*サポートされています*。 
 
+ Machine Learning Services をドメイン コントローラーにインストールしないでください。 セットアップの Machine Learning Services の部分が失敗します。

+ **共有機能** > **Machine Learning Server (スタンドアロン)** を、データベース内インスタンスを実行しているのと同じコンピューターにインストールしないでください。 スタンドアロン サーバーが同じリソースの奪い合いをするため、両方のインストールのパフォーマンスが低下することになります。

+ R および Python の他のバージョンとのサイドバイサイド インストールはサポートされていますが、推奨されません。 これがサポートされているのは、SQL Server インスタンスでは、オープンソースの R および Anaconda ディストリビューションの独自のコピーが使用されるからです。 しかし、SQL Server の外部の SQL Server コンピューターで R および Python を使用するコードを実行すると、さまざまな問題が発生する可能性があるため、お勧めしません。
    
  + SQL Server で実行しているときとは異なるライブラリと実行可能ファイルを使用すると、異なる結果になります。
  + 外部ライブラリで実行されている R および Python スクリプトは、SQL Server で管理できないため、リソースの競合が発生します。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
+ Machine Learning Services は、既定で SQL Server ビッグ データ クラスターにインストールされます。 ビッグ データ クラスターを使用する場合、この記事の手順を実行する必要はありません。 詳細については、[ビッグ データ クラスターでの Machine Learning Services (Python および R) の使用](../../big-data-cluster/machine-learning-services.md)に関するページを参照してください。
::: moniker-end

> [!IMPORTANT]
> セットアップが完了したら、この記事で説明されている構成後の手順を必ず完了してください。 これらの手順には、SQL Server で外部スクリプトを使用できるようにすることや、ユーザーに代わって SQL Server が R ジョブや Python ジョブを実行するために必要なアカウントを追加することが含まれます。 通常、構成を変更するには、インスタンスを再起動するか、Launchpad サービスを再起動する必要があります。

## <a name="get-the-installation-media"></a>インストール メディアを入手する

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>セットアップの実行

ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。

1. SQL Server のセットアップ ウィザードを開始します。
  
1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![SQL Server の新規スタンドアロン インストール](media/2017setup-installation-page-mlsvcs.png)
   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![SQL Server の新規スタンドアロン インストール](media/2019setup-installation-page-mlsvcs.png)
   ::: moniker-end

1. **[機能の選択]** ページで、次のオプションを選択します。

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

   - **データベース エンジン サービス**
     
     SQL Server で R および Python を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 既定のインスタンスまたは名前付きインスタンスを使用できます。

   - **Machine Learning Services (データベース内)**
     
     このオプションを選択すると、R および Python スクリプトの実行をサポートするデータベース サービスがインストールされます。

   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

   - **データベース エンジン サービス**
     
     SQL Server で R、Python、および Java を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 既定のインスタンスまたは名前付きインスタンスを使用できます。

   - **Machine Learning Services (データベース内)**
     
     このオプションを選択すると、R、Python、および Java スクリプトの実行をサポートするデータベース サービスがインストールされます。

   ::: moniker-end

   - **R**
     
     Microsoft R パッケージ、インタープリター、およびオープンソース R を追加するには、このオプションをオンにします。 
     
   - **Python**
     
     Microsoft Python パッケージ、Python 3.5 実行可能ファイルを追加したり、Anaconda ディストリビューションからライブラリを選択したりするには、このオプションをオンにします。
     
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   - **Java**
     
     SQL に付属する Open JRE をインストールしたり、別のバージョンの JDK または JRE の場所を指定したりするには、このオプションをオンにします。
   ::: moniker-end
   
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![R および Python の機能オプション](media/2017setup-features-page-mls-rpy.PNG "R および Python のセットアップ オプション")
   ::: moniker-end
   
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![R、Python の機能オプション](media/2019setup-features-page-mls-rpy.png "R、Python、Java のセットアップ オプション")
   ::: moniker-end
   
   > [!NOTE]
   > 
   > **[Machine Learning Server (スタンドアロン)]** のオプションは選択しないでください。 **[共有機能]** の下の Machine Learning Server をインストールするオプションは、別のコンピューターでの使用を目的としています。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

4. **[Microsoft R Open のインストールに同意する]** ページで、 **[同意する]** 、 **[次へ]** の順に選択します。 このライセンス契約は、Microsoft R Open を対象としており、これには、オープンソース R 基本パッケージとツール、Microsoft 開発チームから提供された R パッケージおよび接続プロバイダーのディストリビューションが含まれています。

1. **[Python のインストールに同意する]** ページで、 **[同意する]** 、 **[次へ]** の順に選択します。 Python のオープンソース ライセンス契約では、Anaconda および関連するツールに加えて、Microsoft 開発チームからのいくつかの新しい Python ライブラリも対象となっています。

   > [!NOTE]
   >  ご使用のコンピューターがインターネットにアクセスできない場合は、この時点でセットアップを一時停止して、個別にインストーラーをダウンロードできます。 詳細については、[インターネットへのアクセスなしで機械学習コンポーネントをインストールする](../install/sql-ml-component-install-without-internet-access.md)に関するページを参照してください。

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
   + データベース エンジン サービス
   + Machine Learning Services (データベース内)
   + R または Python、あるいはその両方

   構成ファイルが格納されている `..\Setup Bootstrap\Log` パスの下にあるフォルダーの場所をメモしておきます。 セットアップが完了したら、インストールされたコンポーネントを概要ファイルで確認できます。

1. セットアップが完了し、コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)」を参照してください。

::: moniker-end

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

1. **[Microsoft R Open のインストールに同意する]** ページで、 **[同意する]** 、 **[次へ]** の順に選択します。 このライセンス契約は、Microsoft R Open を対象としており、これには、オープンソース R 基本パッケージとツール、Microsoft 開発チームから提供された R パッケージおよび接続プロバイダーのディストリビューションが含まれています。

1. **[Python のインストールに同意する]** ページで、 **[同意する]** 、 **[次へ]** の順に選択します。 Python のオープンソース ライセンス契約では、Anaconda および関連するツールに加えて、Microsoft 開発チームからのいくつかの新しい Python ライブラリも対象となっています。

1. **[Java のインストール場所]** ページでは、SQL に付属しているオープン JRE のバージョンをインストールすることも、JDK または JRE の独自のインストール場所を指定することもできます。 **[次へ]** を選択します。

   > [!NOTE]
   >  ご使用のコンピューターがインターネットにアクセスできない場合は、この時点でセットアップを一時停止して、個別にインストーラーをダウンロードできます。 詳細については、[インターネットへのアクセスなしで機械学習コンポーネントをインストールする](../install/sql-ml-component-install-without-internet-access.md)に関するページを参照してください。

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
   + データベース エンジン サービス
   + Machine Learning Services (データベース内)
   + R、Python、Java

   構成ファイルが格納されている `..\Setup Bootstrap\Log` パスの下にあるフォルダーの場所をメモしておきます。 セットアップが完了したら、インストールされたコンポーネントを概要ファイルで確認できます。

1. セットアップが完了し、コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)」を参照してください。

::: moniker-end

## <a name="set-environment-variables"></a>環境変数の設定

R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの[一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)する必要があります。

1. コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。

2. 新しいユーザー変数またはシステム変数を作成します。 

   + 変数名を `MKL_CBWR` に設定する
   + 変数値を `AUTO` に設定する

この手順では、サーバーを再起動する必要があります。 スクリプトの実行を有効にしようとしている場合は、すべての構成作業が完了するまで再起動を遅らせることができます。

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>スクリプトの実行を有効にする

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。 

    > [!TIP]
    > 次のページから適切なバージョンをダウンロードしてインストールできます。[SQL Server Management Studio (SSMS) をダウンロードしてください](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > SQL Server に対する管理タスクとクエリをサポートする [Azure Data Studio](../../azure-data-studio/what-is.md) を使用することもできます。
  
2. Machine Learning Services をインストールしたインスタンスに接続し、 **[新しいクエリ]** をクリックしてクエリ ウィンドウを開き、次のコマンドを実行します。

    ```sql
    sp_configure
    ```

    プロパティ `external scripts enabled` の値は、この時点では **0** であることが必要です。 これは、機能が既定で無効になっているためです。 この機能は、R または Python スクリプトを実行する前に、管理者が明示的に有効にする必要があります。
    
3.  外部スクリプト機能を有効にするには、次のステートメントを実行します。
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    R 言語に対してこの機能を既に有効にしている場合は、Python に対して再構成を再度実行しないでください。 基になる拡張機能プラットフォームでは、両方の言語がサポートされています。

## <a name="restart-the-service"></a>サービスを再起動します。

インストールが完了したら、次のスクリプトの実行を有効にする前に、データベース エンジンを再起動します。

サービスを再起動すると、関連する [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスも自動的に再起動されます。

サービスの再起動は、SSMS でインスタンスの **[再起動]** コマンドを右クリックするか、コントロール パネルの **[サービス]** パネルまたは [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)を使って行うことができます。

## <a name="verify-installation"></a>インストールの確認

[カスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md) またはセットアップ ログで、インスタンスのインストール状態を確認します。

次の手順に従って、外部スクリプトの起動に使用されるすべてのコンポーネントが実行されていることを確認します。

1. SQL Server Management Studio で、新しい [クエリ] ウィンドウを開き、次のコマンドを実行します。
    
   ```sql
   EXECUTE sp_configure  'external scripts enabled'
   ```

   この時点で、**run_value** が 1 に設定されている必要があります。
    
2. **[サービス]** パネルまたは SQL Server 構成マネージャーを開き、**SQL Server Launchpad サービス**が実行されていることを確認します。 R または Python がインストールされているすべてのデータベース エンジンのインスタンスに対して 1 つのサービスがある必要があります。 サービスの詳細については、[機能拡張フレームワーク](../concepts/extensibility-framework.md)に関するページを参照してください。 
   
3. Launchpad が実行されている場合は、外部スクリプト ランタイムが SQL Server と通信できることを確認するため、単純な R スクリプトと Python スクリプトを実行できる必要があります。

   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で新しい **[クエリ]** ウィンドウを開き、次のようなスクリプトを実行します。
   
   + R の場合
   
     ```sql
     EXEC sp_execute_external_script  @language =N'R',
     @script=N'
     OutputDataSet <- InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
     
   + Python の場合
     
     ```sql
     EXEC sp_execute_external_script  @language =N'Python',
     @script=N'
     OutputDataSet = InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
   
   **結果**

   スクリプトの実行には、最初に外部スクリプト ランタイムが読み込まれるときに少し時間がかかります。 結果は次のようになります。

   | hello |
   |----|
   | 1|

> [!NOTE]
> 設計上、Python スクリプトで使用される列または見出しは返されません。 出力に列名を追加するには、戻り値のデータ セットに対してスキーマを指定する必要があります。 これを行うには、ストアド プロシージャの WITH RESULTS パラメーターを使用して、列に名前を付け、SQL データ型を指定します。
> 
> たとえば、次の行を追加して、任意の列名を生成できます。`WITH RESULT SETS ((Col1 AS int))`

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
<!-- There are no updates yet available for 2019, and there's no 2019 update list site. When updates become available, add 2019 information to this section. -->

<a name="apply-cu"></a>

## <a name="apply-updates"></a>更新プログラムの適用

最新の累積的な更新プログラムをデータベース エンジンと機械学習コンポーネントの両方に適用することをお勧めします。

インターネットに接続されているデバイスでは、通常、累積的な更新プログラムは Windows Update によって適用されますが、管理された更新には、次の手順を使用することもできます。 データベース エンジンに更新プログラムを適用すると、同じインスタンスにインストールしたすべての R または Python 機能の累積更新プログラムがセットアップによってプルされます。 

接続されていないサーバーでは、追加の手順が必要です。 詳細については、[インターネット アクセスなしでコンピューターにインストールする > 累積的な更新プログラムを適用する](sql-ml-component-install-without-internet-access.md#apply-cu)を参照してください。

1. 既にインストールされているベースライン インスタンスを使用して開始します。SQL Server 2017 の初回リリース

2. 累積的な更新プログラムの一覧に移動します。[SQL Server 2017 の更新プログラム](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 最新の累積的な更新プログラムを選択します。 実行可能ファイルがダウンロードされ、自動的に抽出されます。

4. セットアップを実行します。 ライセンス条項に同意し、[機能の選択] ページで、累積的な更新プログラムが適用される機能を確認します。 機械学習機能を含む、現在のインスタンスにインストールされているすべての機能が表示されます。 セットアップにより、すべての機能を更新するために必要な CAB ファイルがダウンロードされます。

   ![インストールされている機能の概要](media/cumulative-update-feature-selection.png)

5. ウィザードを続行し、R および Python ディストリビューションのライセンス条項に同意します。 

::: moniker-end

## <a name="additional-configuration"></a>その他の構成

外部スクリプトの検証手順が成功した場合は、SQL Server Management Studio、Visual Studio Code、または T-SQL ステートメントをサーバーに送信できる他の任意のクライアントから、R または Python コマンドを実行できます。

コマンドの実行中にエラーが発生した場合は、このセクションの追加の構成手順を確認してください。 場合によっては、サービスまたはデータベースに対して追加の適切な構成を行う必要があります。

インスタンス レベルでは、追加の構成には次のものが含まれます。

* [SQL Server Machine Learning Services のファイアウォール構成](../../advanced-analytics/security/firewall-configuration.md)
* [追加のネットワーク プロトコルの有効化](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [リモート接続の有効化](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [SQLRUserGroup のログインの作成](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* ディスク領域を消費するタスクを外部スクリプトで実行しないようにするための[ディスク クォータの管理](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Windows の SQL Server 2019 では、分離メカニズムが変更されています。 これは **SQLRUserGroup**、ファイアウォール規則、ファイルのアクセス許可、および暗黙の認証に影響します。 詳細については、[Machine Learning Services の分離の変更](sql-server-machine-learning-services-2019.md)に関するページを参照してください。
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

データベースでは、次の構成の更新が必要になる場合があります。

* [SQL Server Machine Learning Services にユーザー アクセス許可を付与する](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> 追加の構成が必要かどうかは、SQL Server をインストールしたセキュリティ スキーマと、ユーザーをどのようにデータベースに接続して外部スクリプトを実行させるかによって異なります。

## <a name="suggested-optimizations"></a>推奨される最適化

これですべてが機能するようになったので、機械学習をサポートするようにサーバーを最適化したり、事前トレーニング済みのモデルをインストールしたりすることもできます。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>ワーカー アカウントを追加する

多くのユーザーが同時にスクリプトを実行する場合は、Launchpad サービスに割り当てられるワーカー アカウントの数を増やすことができます。 詳細については、「[SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](../administration/scale-concurrent-execution-external-scripts.md)」を参照してください。
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>スクリプトの実行用にサーバーを最適化する

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップの既定の設定では、データベース エンジンによってサポートされているさまざまなサービスのバランスを最適化することを目的としています。サービスには、抽出 (Extract)、変換 (Transform)、および読み込み (Load) の ETL プロセス、レポート、監査、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データを使うアプリケーションなどが含まれます。 そのため、既定の設定では、場合によっては機械学習用のリソースが制限または調整されることがあります (特に、メモリを大量に使用する操作の場合)。

確実に機械学習ジョブの優先順位が適切に設定され、リソースが提供されるようにするには、SQL Server Resource Governor を使って外部リソース プールを構成することをお勧めします。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンに割り当てられるメモリの量を変更したり、[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスで実行するアカウントの数を増やしたりすることもできます。

- 外部リソースを管理するためのリソース プールを構成するには、[CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) に関するページを参照してください。
  
- データベース用に予約されているメモリの量を変更するには、「[サーバー メモリの構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」を参照してください。
  
- [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] によって開始できる R アカウントの数を変更するには、「[SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](../administration/scale-concurrent-execution-external-scripts.md)」を参照してください。

Standard Edition を使用していて、Resource Governor がない場合は、動的管理ビュー (DMV) と拡張イベントに加え、Windows イベント監視を使用してサーバー リソースを管理できます。 詳細については、[R Services の監視と管理](../r/managing-and-monitoring-r-solutions.md)および [Python Services の監視と管理](../python/managing-and-monitoring-python-solutions.md)に関するページを参照してください。

### <a name="install-additional-python-and-r-packages"></a>Python と R の追加パッケージをインストールする

SQL Server 用に作成する Python および R ソリューションでは、基本関数、SQL Server と共にインストールされた独自のパッケージの関数、SQL Server によってインストールされたオープンソースの Python および R のバージョンと互換性のあるサードパーティ製のパッケージを呼び出すことができます。

SQL Server で使用するパッケージは、インスタンスによって使用される既定のライブラリにインストールする必要があります。 コンピューター上に Python または R の別のインストールがある場合、またはパッケージをユーザー ライブラリにインストールした場合は、これらのパッケージが T-SQL から使用できなくなります。

追加のパッケージをインストールして管理するには、ユーザー グループを設定してデータベース レベルでパッケージを共有するか、ユーザーが独自のパッケージをインストールできるようにデータベース ロールを構成します。 詳細については、[Python パッケージのインストール](../package-management/install-additional-python-packages-on-sql-server.md)と[新しい R パッケージのインストール](../package-management/install-additional-r-packages-on-sql-server.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクをご覧ください。

+ [チュートリアル: T-SQL での R の実行](../tutorials/quickstart-r-create-script.md)
+ [チュートリアル: R 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [チュートリアル: T-SQL での Python の実行](../tutorials/run-python-using-t-sql.md)
+ [チュートリアル: Python 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

実際のシナリオに基づいた機械学習の例については、[機械学習のチュートリアル](../tutorials/machine-learning-services-tutorials.md)を参照してください。
