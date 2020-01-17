---
title: Machine Learning Server のインストール (スタンドアロン)
description: RevoScaleR、revoscalepy、MicrosoftML、およびその他のパッケージを使用した R および Python 開発用に、インスタンス対応でないスタンドアロンの機械学習サーバーをセットアップします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 02df024801dad815b640f4ef4222a0c8face485b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727641"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>SQL Server セットアップを使用して Machine Learning Server (スタンドアロン) または R Server (スタンドアロン) をインストールする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server セットアップには、SQL Server の外部で実行される、インスタンス対応でないスタンドアロンの機械学習サーバーをインストールするための**共有機能**オプションが含まれています。 これは **Machine Learning Server (スタンドアロン)** と呼ばれ、R と Python が含まれています。 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server セットアップには、SQL Server の外部で実行される、インスタンス対応でないスタンドアロンの機械学習サーバーをインストールするための**共有機能**オプションが含まれています。 SQL Server 2016 では、この機能は **R Server (スタンドアロン)** と呼ばれます。  
::: moniker-end

SQL Server セットアップによってインストールされるスタンドアロン サーバーは、[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) の非 SQL ブランド バージョンと機能的に同等であり、次のような同じユース ケースとシナリオがサポートされています。

+ リモート実行、同じコンソールでのローカル セッションとリモート セッションの切り替え
+ Web ノードとコンピューティング ノードを使用した運用可能化
+ Web サービスの配置: R および Python スクリプトを Web サービスにパッケージ化する機能
+ R および Python 関数ライブラリの完全なコレクション

SQL Server から切り離された独立したサーバーとしての R と Python の環境は、SQL Server ではなく、スタンドアロン サーバー上に用意された基盤のオペレーティング システムとツールを使用して構成、セキュリティ保護、およびアクセスされます。

スタンドアロン サーバーは、SQL Server を補完するものとして、サポートされているすべてのデータ プラットフォームに対してリモート コンピューティング コンテキストを使用できる、ハイ パフォーマンスの機械学習ソリューションを開発する必要がある場合に役立ちます。 ローカル サーバーから、Spark クラスター上または別の SQL Server インスタンス上のリモートの機械学習サーバーに実行をシフトできます。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

SQL Server 2016 R Server (スタンドアロン) や Microsoft R Server などの以前のバージョンをインストール済みである場合は、続行する前に既存のインストールをアンインストールしてください。

一般的なルールとして、スタンドアロン サーバーのインストールとデータベース エンジンのインスタンス対応インストールは、リソースの競合を避けるために相互に排他的なものとして扱うことをお勧めしますが、十分なリソースがある場合は、同じ物理コンピューター上に両方をインストールすることは禁止されていません。

そのコンピューターには、SQL Server Machine Learning Server (スタンドアロン) または SQL Server R Server (スタンドアロン) のいずれかのスタンドアロン サーバーを 1 つだけセットアップできます。 必ず 1 つのバージョンをアンインストールしてから、新しいバージョンを追加してください。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>インストールのパッチ要件 

SQL Server 2016 の場合のみ:SQL Server の前提条件としてインストールされる特定のバージョンの Microsoft VC++ 2013 ランタイム バイナリに問題が見つかりました。 VC ランタイム バイナリに対するこの更新プログラムをインストールしないと、特定のシナリオにおいて、SQL Server で安定性の問題が発生する可能性があります。 SQL Server をインストールする前に、「[SQL Server リリース ノート](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)」にある手順に従って、ご使用のコンピューターに VC ランタイム バイナリのパッチが必要かどうかを確認してください。  
::: moniker-end

## <a name="get-the-installation-media"></a>インストール メディアを入手する

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>セットアップの実行

ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。

1. インストール ウィザードを開始します。

2. **[インストール]** タブをクリックし、 **[Machine Learning Server (スタンドアロン) の新規インストール]** を選択します。
    
   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Machine Learning Server スタンドアロンのインストール](media/2017setup-installation-page-mlsvr.png "Machine Learning Server スタンドアロンのインストールを開始する")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Machine Learning Server スタンドアロンのインストール](media/2019setup-installation-page-mlsvr.png "Machine Learning Server スタンドアロンのインストールを開始する")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

3. ルール チェックが完了したら、SQL Server ライセンス条項に同意し、新規インストールを選択します。

4. **[機能の選択]** ページで、次のオプションが既に選択されています。

    - **Microsoft Machine Learning Server (スタンドアロン)**

    - **R** と **Python** の両方が既定で選択されています。 どちらの言語も選択解除できますが、サポートされている言語の少なくとも 1 つをインストールすることをお勧めします。

   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![R または Python の機能の選択](media/2017setup-features-page-mlsvr-rpy.png "Machine Learning Server スタンドアロンのインストールを開始する")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![R または Python の機能の選択](media/2019setup-features-page-mlsvr-rpy.png "Machine Learning Server スタンドアロンのインストールを開始する")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
    
   その他のオプションはすべて無視します。 
    
   > [!NOTE]
   > コンピューターに SQL Server データベース内分析用の Machine Learning Services が既にインストールされている場合、**共有機能**のインストールは行わないようにしてください。 これを行うと、重複するライブラリが作成されます。
   > 
   > また、SQL Server で実行される R または Python スクリプトは、他のデータベース エンジン サービスで使用されるメモリと競合しないように SQL Server によって管理されますが、スタンドアロンの機械学習サーバーにはそのような制約がないため、他のデータベース操作の妨げになる可能性があります。 最後に、RDP セッション経由のリモート アクセス (運用可能化によく使用される) は、通常、データベース管理者によってブロックされます。
   > 
   > このような理由から、通常は SQL Server Machine Learning Services とは別のコンピューターに Machine Learning Server (スタンドアロン) をインストールすることをお勧めします。

5. 基本言語ディストリビューションのダウンロードとインストールに関するライセンス条項に同意します。 **[同意する]** ボタンが使用できない状態になっている場合は、 **[次へ]** をクリックします。 

6. **[インストールの準備完了]** ページで、選択内容を確認し、 **[インストール]** をクリックします。

インストールが完了したら、[SQL Server R Services のカスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md)に関するページを参照してください。エラーと警告については、[アップグレードとインストールに関する FAQ - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md) のページを参照してください。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>セットアップの実行

ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。

1. インストール ウィザードを開始します。

2. **[インストール]** タブで、 **[新規 R サーバー (スタンドアロン) のインストール]** をクリックします。
    
   ![R Server スタンドアロンのセットアップを開始する](media/2016-setup-installation-rsvr.png "R Server スタンドアロンのセットアップを開始する")

3. ルール チェックが完了したら、SQL Server ライセンス条項に同意し、新規インストールを選択します。

4. **[機能の選択]** ページで、次のオプションが既に選択されています。
    
   - **R Server (スタンドアロン)**  
    
   ![R Server スタンドアロンの機能の選択](media/2016setup-rserver-features.png "R Server スタンドアロンの機能の選択")
    
   その他のすべてのオプションは無視できます。 
    
   > [!NOTE]
   > SQL Server のデータベース内分析用に R Services が既にインストールされているコンピューター上でセットアップを実行している場合、**共有機能**のインストールは行わないようにしてください。 これを行うと、重複するライブラリが作成されます。
   > 
   > SQL Server で実行される R スクリプトは、他のデータベース エンジン サービスで使用されるメモリと競合しないように SQL Server によって管理されますが、スタンドアロンの R Server にはそのような制約がないため、他のデータベース操作の妨げになる可能性があります。
   > 
   > 通常、R Server (スタンドアロン) は、SQL Server R Services (データベース内) とは別のコンピューターにインストールすることをお勧めします。

5. 基本言語ディストリビューションのダウンロードとインストールに関するライセンス条項に同意します。 **[同意する]** ボタンが使用できない状態になっている場合は、 **[次へ]** をクリックします。 

6. **[インストールの準備完了]** ページで、選択内容を確認し、 **[インストール]** をクリックします。

インストールが完了したら、[SQL Server R Services のカスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md)に関するページを参照してください。エラーと警告については、[アップグレードとインストールに関する FAQ - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md) のページを参照してください。
::: moniker-end

## <a name="set-environment-variables"></a>環境変数の設定

R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの[一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)する必要があります。

1. コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。

2. 新しいユーザー変数またはシステム変数を作成します。 

  + 変数名を `MKL_CBWR` に設定する
  + 変数値を `AUTO` に設定する

3. サーバーを再起動します。

<a name="install-path"></a>

### <a name="default-installation-folders"></a>既定のインストール フォルダー

R と Python の開発では、同じコンピューター上に複数のバージョンがあることが一般的です。 SQL Server セットアップによってインストールされるように、基本ディストリビューションは、セットアップに使用した SQL Server バージョンに関連付けられているフォルダーにインストールされます。

次の表は、Microsoft インストーラーによって作成される R および Python ディストリビューションのパスを示しています。 完全を期すために、この表には、SQL Server セットアップと Microsoft Machine Learning Server のスタンドアロン インストーラーによって生成されるパスが含まれています。

|Version| インストール方法 | 既定のフォルダー|
|----|----|----|
|SQL Server 2019 Machine Learning Server (スタンドアロン) |  SQL Server 2019 セットアップ ウィザード |`C:\Program Files\Microsoft SQL Server\150\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\150\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Server (スタンドアロン) |  SQL Server 2017 セットアップ ウィザード |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (スタンドアロン) |  Windows スタンドアロン インストーラー |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (データベース内) |R 言語オプションを含む SQL Server 2019 セットアップ ウィザード|`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\PYTHON_SERVICES` |
|SQL Server Machine Learning Services (データベース内) |R 言語オプションを含む SQL Server 2017 セットアップ ウィザード|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (スタンドアロン) |  SQL Server 2016 セットアップ ウィザード |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (データベース内) |SQL Server 2016 セットアップ ウィザード|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>更新プログラムの適用

最新の累積的な更新プログラムをデータベース エンジンと機械学習コンポーネントの両方に適用することをお勧めします。 累積的な更新プログラムは、セットアップ プログラムによってインストールされます。 

インターネットに接続されたデバイスでは、自己解凍形式の実行可能ファイルをダウンロードできます。 データベース エンジンの更新プログラムを適用すると、既存の R および Python の機能の累積的な更新内容が自動的に取り込まれます。 

接続されていないサーバーでは、追加の手順が必要です。 データベース エンジンの累積的な更新プログラムと、機械学習機能の CAB ファイルを入手する必要があります。 すべてのファイルを分離されたサーバーに転送し、手動で適用する必要があります。

1. ベースライン インスタンスを使用して開始します。 累積的な更新プログラムは、既存のインストールのみに適用できます。

  + SQL Server 2019 初回リリースの Machine Learning Server (スタンドアロン)
  + SQL Server 2017 初回リリースの Machine Learning Server (スタンドアロン)
  + SQL Server 2016 初回リリース、SQL Server 2016 SP 1、または SQL Server 2016 SP 2 の R Server (スタンドアロン)

2. 開いている R または Python セッションがあれば終了し、システムでまだ実行中のプロセスがあれば停止します。

3. Web サービスの配置用の Web ノードとコンピューティング ノードとして実行するために運用可能化を有効にした場合は、**AppSettings.json** ファイルを念のためにバックアップします。 SQL Server 2017 CU13 以降を適用すると、このファイルが改訂されるため、元のバージョンを保持するためにバックアップ コピーが必要になる場合があります。

4. インターネットに接続されているデバイスで、使用しているバージョンの SQL Server 用の累積更新プログラムのリンクをクリックします。

  + SQL Server 2019 更新プログラム *(利用可能な更新プログラムはまだありません)*
  + [SQL Server 2017 更新プログラム](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新プログラム](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 最新の累積的な更新プログラムをダウンロードします。 それは実行可能ファイルです。

6. インターネットに接続されているデバイスで、.exe をダブルクリックしてセットアップを実行し、ウィザードの手順に従ってライセンス条項に同意し、影響を受ける機能を確認して、完了するまで進行状況を監視します。

7. インターネットに接続されていないサーバーの場合:

   + R および Python 用の対応する CAB ファイルを入手します。 ダウンロード リンクについては、「[SQL Server データベース内分析インスタンスの累積的な更新プログラムの CAB ダウンロード](sql-ml-cab-downloads.md)」を参照してください。

   + すべてのファイル (メインの実行可能ファイルと CAB ファイル) をオフライン コンピューター上のフォルダーに転送します。

   + .exe ファイルをダブルクリックしてセットアップを実行します。 インターネットに接続されていないサーバーに累積的な更新プログラムをインストールする場合は、R と Python の .cab ファイルの場所を選択するように求められます。

8. インストール後、Web ノードとコンピューティング ノードを使用した運用可能化を有効にしたサーバーで **AppSettings.json** を編集し、"MMLNativePath" のすぐ下に "MMLResourcePath" エントリを追加します。 例:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [管理 CLI ユーティリティを実行](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)して、Web ノードとコンピューティング ノードを再起動します。 手順と構文については、「[Web ノードとコンピューティング ノードの監視、開始、停止](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)」を参照してください。

## <a name="development-tools"></a>開発ツール

開発 IDE は、セットアップの段階でインストールされません。 開発環境の構成の詳細については、[R ツールのセットアップ](../r/set-up-a-data-science-client.md)に関するページと [Python ツールのセットアップ](../python/setup-python-client-tools-sql.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクをご覧ください。

+ [チュートリアル: T-SQL での R の実行](../tutorials/quickstart-r-create-script.md)
+ [チュートリアル: R 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [チュートリアル: T-SQL での Python の実行](../tutorials/run-python-using-t-sql.md)
+ [チュートリアル: Python 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

実際のシナリオに基づいた機械学習の例については、[機械学習のチュートリアル](../tutorials/machine-learning-services-tutorials.md)を参照してください。
