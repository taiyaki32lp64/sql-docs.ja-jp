---
title: Python と R に関する既知の問題
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f5627a5e35039420725795f53a7fc63d5582ab9
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706848"
---
# <a name="known-issues-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services での既知の問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[SQL Server Machine Learning Services](what-is-sql-server-machine-learning.md) および [SQL Server 2016 R Services](r/sql-server-r-services.md) でオプションとして提供される機械学習コンポーネントでの既知の問題または制限事項について説明します。

## <a name="setup-and-configuration-issues"></a>セットアップと構成に関する問題

初期セットアップと構成に関連するプロセスおよび一般的な質問については、[アップグレードとインストールに関する FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md) の記事をご覧ください。 新しい R または Python のコンポーネントのアップグレード、サイドバイサイド インストール、およびインストールに関する情報が含まれています。

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1.環境変数がないことによる MKL の計算結果の不整合

**適用対象:** R_SERVER バイナリ 9.0、9.1、9.2、9.3。

R_SERVER では Intel Math Kernel Library (MKL) が使われます。 システムに環境変数がない場合、MKL に関する計算で、一貫性のない結果が発生する可能性があります。 

R_SERVER で条件付きの数値が確実に再現されるようにするには、環境変数 `'MKL_CBWR'=AUTO` を設定します。 詳しくは、「[Introduction to Conditional Numerical Reproducibility (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)」(条件付き数値の再現性 (CNR) の概要) をご覧ください。

**回避策**

1. コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。

2. 新しいユーザー変数またはシステム変数を作成します。 

   + [変数名] を "MKL_CBWR" に設定します。
   + [変数値] を "AUTO" に設定します。

3. R_SERVER を再起動します。 SQL Server では、SQL Server Launchpad サービスを再起動できます。

> [!NOTE]
> Linux で SQL Server 2019 を実行している場合は、ユーザー ホーム ディレクトリの *.bash_profile* を編集または作成し、`export MKL_CBWR="AUTO"` という行を追加します。 bash コマンド プロンプトで「`source .bash_profile`」と入力して、このファイルを実行します。 R のコマンド プロンプトで「`Sys.getenv()`」と入力して、R_SERVER を再起動します。

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2.R スクリプトのランタイム エラー (SQL Server 2017 CU5-CU7 の回帰)

SQL Server 2017 の累積更新プログラム 5 から 7 では、**rlauncher.config** ファイルに、一時ディレクトリのファイル パスにスペースが含まれるという回帰があります。 この回帰は、CU8 で修正されています。

R スクリプトを実行すると、次のようなメッセージが含まれるエラーが表示されます。

> *'R' スクリプトのランタイムと通信できませんでした。'R' ランタイムの要件を確認してください。*
>
> 外部スクリプトからの STDERR メッセージ: 
>
> *致命的なエラー: 'R_TempDir' を作成できません*

**回避策**

CU8 が使用可能になったら適用します。 または、管理者特権でのコマンド プロンプトでアンインストール/インストールを行って **registerrext** を実行することにより、**rlauncher.config** を作成し直してもかまいません。 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

次の例では、既定のインスタンス "MSSQL14.MSSQLSERVER" が "C:\Program Files\Microsoft SQL Server\" にインストールされている場合のコマンドを示します。

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3.SQL Server の機械学習機能をドメイン コントローラーにインストールできない

SQL Server 2016 R Services または SQL Server Machine Learning Services をドメイン コントローラーにインストールしようとすると、次のエラーが発生し、セットアップが失敗します。

> *機能のセットアップ処理中にエラーが発生しました*
>
> *ID のグループが見つかりません*
>
> *コンポーネント エラー コード: 0x80131509*

エラーが発生するのは、ドメイン コントローラーでは、機械学習を実行するために必要な 20 個のローカル アカウントをサービスが作成できないためです。 一般に、ドメイン コントローラーに SQL Server をインストールすることはお勧めしません。 詳しくは、[サポート情報 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont) をご覧ください。

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4.最新のサービス リリースをインストールして Microsoft R Client との互換性を確保する

最新バージョンの Microsoft R Client をインストールし、それを使用してリモート コンピューティング コンテキストの SQL Server で R を実行すると、次のようなエラーが発生する場合があります。

> *You are running version 9.x.x of Microsoft R Client on your computer, which is incompatible with Microsoft R Server version 8.x.x. (Microsoft R Server バージョン 8.x.x と互換性のない、バージョン 9.x.x の Microsoft R Client をコンピューター上で実行しています。)互換性のあるバージョンをダウンロードしてインストールしてください。*

SQL Server 2016 では、クライアント上の R ライブラリがサーバー上の R ライブラリと完全に一致している必要があります。 その制限は、Microsoft R Server 9.0.1 より後のリリースではなくなっています。 それでも、このエラーが発生する場合は、クライアントとサーバーで使われている R ライブラリのバージョンを確認し、必要に応じて、サーバーのバージョンに合わせてクライアントを更新します。

SQL Server のサービス リリースをインストールすると常に、SQL Server R Services でインストールされる R のバージョンは更新されます。 確実に最新バージョンの R コンポーネントを使用するためには、すべてのサービス パックをインストールしてください。

Microsoft R Client 9.0.0 との互換性を確保するには、この[サポート記事](https://support.microsoft.com/kb/3210262)で説明されている更新プログラムをインストールします。

R パッケージに関する問題を回避するには、モダン ライフサイクル サポート ポリシーを使用するようにサービス契約を変更することで、サーバーにインストールされている R ライブラリのバージョンをアップグレードすることもできます。詳細については、[次のセクション](#bkmk_sqlbindr)を参照してください。 そのようにすると、SQL Server でインストールされる R のバージョンは、Machine Learning Server (旧称 Microsoft R Server) の更新と同じスケジュールで更新されます。

**適用対象:** SQL Server 2016 R Services、Microsoft R Server バージョン 9.0.0 以前

### <a name="5-r-components-missing-from-cu3-setup"></a>5.CU3 のセットアップに R コンポーネントがない

限られた数の Azure 仮想マシンは、SQL Server に含める必要がある R インストール ファイルなしでプロビジョニングされました。 この問題は、2018-01-05 から 2018-01-23 の期間にプロビジョニングされた仮想マシンで発生します。 また、2018-01-05 から 2018-01-23 の期間に SQL Server 2017 の CU3 更新プログラムを適用した場合、この問題はオンプレミスのインストールにも影響を与える可能性があります。

正しいバージョンの R インストール ファイルを含むサービス リリースが提供されています。

+ [SQL Server 2017 の累積的な更新プログラム パッケージ 3 - KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

コンポーネントをインストールして SQL Server 2017 CU3 を修復するには、CU3 をアンインストールし、更新後のバージョンを再インストールする必要があります。

1. R インストーラーが含まれる更新された CU3 インストール ファイルをダウンロードします。
2. CU3 をアンインストールします。 コントロール パネルで **[更新プログラムのアンインストール]** を探し、"Hotfix 3015 for SQL Server 2017 (KB4052987) (64-bit)" を選択します。 アンインストールの手順を続けます。
3. ダウンロードした KB4052987 の更新プログラム `SQLServer2017-KB4052987-x64.exe` をダブルクリックして、CU3 更新プログラムを再インストールします。 インストール手順に従います。

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6.SQL Server 2017 CTP 2.0 以降のオフライン インストールで Python コンポーネントをインストールできない

SQL Server 2017 のプレリリース版をインターネットにアクセスできないコンピューターにインストールする場合、ダウンロードした Python コンポーネントの場所の入力を求めるページが、インストーラーで表示されない場合があります。 そのような場合、Machine Learning Services 機能はインストールできますが、Python コンポーネントはインストールできません。

この問題は、リリース バージョンで解決されています。 また、この制限は R コンポーネントでは発生しません。

**適用対象:** SQL Server 2017 と Python

### <a name="bkmk_sqlbindr"></a>[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] を使用してクライアントから古いバージョンの SQL Server R Services に接続すると、互換性のないバージョンであることが警告される

SQL Server 2016 のコンピューティング コンテキストで R コードを実行すると、次のエラーが表示される場合があります。

> *Microsoft R Server バージョン 8.0.3 と互換性のない、バージョン 9.0.0 の Microsoft R Client をコンピューター上で実行しています。互換性のあるバージョンをダウンロードしてインストールしてください。*

このメッセージは、次のいずれかに該当する場合に表示されます。

+ [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] のセットアップ ウィザードを使用して、クライアント コンピューターに Microsoft R Server (スタンドアロン) をインストールした。
+ [別の Windows インストーラー](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)を使用して、Microsoft R Server をインストールした。

サーバーとクライアントで確実に同じバージョンが使用されるようにするには、Microsoft R Server 9.0 以降のリリースでサポートされている "_バインド_" を使用して、SQL Server 2016 インスタンスの R コンポーネントをアップグレードすることが必要な場合があります。 お使いの R Services のバージョンでアップグレードがサポートされているかどうかを判断するには、[SqlBindR.exe を用いた R Services のインスタンスのアップグレード](install/upgrade-r-and-python.md)に関する記事を参照してください。

**適用対象:** SQL Server 2016 R Services、Microsoft R Server バージョン 9.0.0 以前

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7.SQL Server 2016 サービス リリースをセットアップすると、新しいバージョンの R コンポーネントのインストールに失敗する場合がある

累積的な更新プログラムをインストールする場合や、インターネットに接続されていないコンピューターに SQL Server 2016 のサービス パックをインストールする場合、セットアップ ウィザードに、ダウンロードした CAB ファイルを使用して R コンポーネントを更新するためのプロンプトが表示されないことがあります。 通常、このエラーは、データベース エンジンと共に複数のコンポーネントがインストールされている場合に発生します。

回避策としては、CU1 更新プログラムのインストールに関する次の例で示されているように、コマンド ラインで `MRCACHEDIRECTORY` 引数を指定してサービス リリースをインストールすることができます。

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

最新のインストーラーを入手するには、[インターネット アクセスなしでの機械学習コンポーネントのインストール](install/sql-ml-component-install-without-internet-access.md)に関するページを参照してください。

**適用対象:** SQL Server 2016 R Services、Microsoft R Server バージョン 9.0.0 以前

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8.R のバージョンと異なるバージョンの Launchpad サービスを開始できない

データベース エンジンとは別に SQL Server R Services をインストールし、ビルドのバージョンが異なる場合は、システム イベント ログに次のエラーが記録されることがあります。

> *SQL Server Launchpad サービスは次のエラーのため開始できませんでした: そのサービスは指定時間内に開始要求または制御要求に応答しませんでした。*

たとえば、このエラーは、リリース バージョンを使用してデータベース エンジンをインストールし、パッチを適用してデータベース エンジンをアップグレードした後、リリース バージョンを使用して R Services の機能を追加した場合に、発生することがあります。

この問題を回避するには、ファイル マネージャーなどのユーティリティを使用して、Launchpad.exe のバージョンと、sqldk.dll などの SQL バイナリのバージョンを比較します。 すべてのコンポーネントは、同じバージョン番号である必要があります。 1 つのコンポーネントをアップグレードする場合は、インストールされている他のすべてのコンポーネントに必ず同じアップグレードを適用してください。

インスタンスの `Binn` フォルダーで Launchpad を検索します。 たとえば、SQL Server 2016 の既定のインストールでは、パスは `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn` などです。 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9.Azure 仮想マシンで実行されている SQL Server インスタンスのファイアウォールによってリモート コンピューティング コンテキストがブロックされる

[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] が Azure 仮想マシンにインストールされている場合、仮想マシンのワークスペースを使用する必要があるコンピューティング コンテキストを使用できない場合があります。 これは、Azure 仮想マシン上のファイアウォールに、ローカルの R ユーザー アカウントのネットワーク アクセスをブロックする規則が既定で含まれるためです。

回避策としては、Azure VM で **[セキュリティが強化された Windows ファイアウォール]** を開き、 **[送信の規則]** を選択して、次の規則を無効にします。 **[Block network access for R local user accounts in SQL Server instance MSSQLSERVER]\(SQL Server インスタンス MSSQLSERVER の R ローカル ユーザー アカウントに対するネットワーク アクセスをブロックする\)** 。 また、規則を有効のままにして、セキュリティ プロパティを **[Allow if secure]\(セキュリティで保護されているときに許可する\)** に変更するのでもかまいません。

### <a name="10-implied-authentication-in-sqlexpress"></a>10.SQLEXPRESS での暗黙の認証

統合 Windows 認証を使用してリモート データ サイエンス ワークステーションから R ジョブを実行すると、SQL Server では、"*暗黙の認証*" を使用して、スクリプトで必要になる可能性のあるローカル ODBC 呼び出しが生成されます。 ただし、この機能は、SQL Server Express Edition の RTM ビルドでは使用できません。

この問題を解決するために、新しいサービス リリースにアップグレードすることをお勧めします。

アップグレードできない場合の回避策としては、SQL ログインを使用して、埋め込みの ODBC 呼び出しを必要とする可能性のあるリモート R ジョブを実行します。

**適用対象:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11.SQL Server によって使用されるライブラリが他のツールから呼び出される場合のパフォーマンスの制限

RGui などの外部アプリケーションから、SQL Server 用にインストールされている機械学習ライブラリを呼び出すことができます。 そうすることが、新しいパッケージのインストールや、非常に短いコード サンプルでのアドホック テストの実行といった、特定のタスクを実行するための最も便利な方法である場合があります。 ただし、SQL Server の外部では、パフォーマンスが制限される可能性があります。

たとえば、SQL Server の Enterprise Edition を使用している場合でも、外部ツールを使用して R コードを実行すると、R はシングルスレッド モードで実行されます。 SQL Server での優れたパフォーマンスを利用するには、SQL Server 接続を開始し、[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して外部スクリプトのランタイムを呼び出します。

一般に、SQL Server によって使用される機械学習ライブラリを外部ツールから呼び出すことは避けてください。 R または Python のコードをデバッグする必要がある場合は、通常、SQL Server の外部で行う方が簡単です。 SQL Server にあるものと同じライブラリを入手するには、Microsoft R Client、[SQL Server 2017 Machine Learning Server (スタンドアロン)](install/sql-machine-learning-standalone-windows-install.md)、または [SQL Server 2016 R Server (スタンドアロン)](install/sql-r-standalone-windows-install.md) をインストールします。

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12.SQL Server Data Tools では、外部スクリプトで必要なアクセス許可がサポートされていない

Visual Studio または SQL Server Data Tools を使用してデータベース プロジェクトを発行するとき、外部スクリプトの実行に固有のアクセス許可をプリンシパルが持っている場合は、次のようなエラーが表示されることがあります。

> *TSQL モデル: Error detected when reverse engineering the database.The permission was not recognized and was not imported.* (データベースのリバース エンジニアリング中にエラーが検出されました。アクセス許可が認識されず、インポートされませんでした。)

現在、DACPAC モデルでは、GRANT ANY EXTERNAL SCRIPT (任意の外部スクリプトを許可する) や EXECUTE ANY EXTERNAL SCRIPT (任意の外部スクリプトを実行する) など、R Services または Machine Learning Services によって使用されるアクセス許可はサポートされていません。 この問題は今後のリリースで修正される予定です。

回避策としては、追加の GRANT ステートメントを配置後スクリプトで実行します。

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13.リソース ガバナンスの既定値により、外部スクリプトの実行が調整される

Enterprise Edition では、外部スクリプト プロセスを管理するためにリソース プールを使用できます。 一部の早期リリース ビルドでは、R プロセスに割り当てられる最大メモリは 20 パーセントでした。 したがって、サーバーに 32 GB の RAM がある場合、R の実行可能ファイル (RTerm.exe および BxlServer.exe) では 1 つの要求で最大 6.4 GB を使用できました。

リソースの制限に達する場合は、現在の既定値を確認してください。 20 パーセントでは不十分な場合は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のドキュメントで、この値を変更する方法をご覧ください。

**適用対象:** SQL Server 2016 R Services、Enterprise Edition


### <a name="14-error-when-using-sp_execute_external_script-without-libcso-on-linux"></a>14. Linux で `libc++.so` を使用せずに `sp_execute_external_script` を使用するときのエラー

`libc++.so` がインストールされていないクリーンな Linux マシンでは、`commonlauncher.so` で `libc++.so` を読み込めないため、Java または外部言語で `sp_execute_external_script` (SPEES) クエリを実行できません。

例:

```sql
EXECUTE sp_execute_external_script @language = N'Java'
    , @script = N'JavaTestPackage.PassThrough'
    , @parallel = 0
    , @input_data_1 = N'select 1'
WITH RESULT SETS((col1 INT NOT NULL))
GO
```

次のようなメッセージが表示されて失敗します。

```text
Msg 39012, Level 16, State 14, Line 0

Unable to communicate with the runtime for 'Java' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Java' runtime.
```

`mssql-launchpadd` ログには、次のようなエラー メッセージが記録されます。

```text
Oct 18 14:03:21 sqlextmls launchpadd[57471]: [launchpad] 2019/10/18 14:03:21 WARNING: PopulateLauncher failed: Library /opt/mssql-extensibility/lib/commonlauncher.so not loaded. Error: libc++.so.1: cannot open shared object file: No such file or directory
```

**回避策**

次のいずれかの回避策を実行できます。

1. `/opt/mssql/lib` から既定のシステム パス `/lib64` に、`libc++*` をコピーします

1. 次のエントリを `/var/opt/mssql/mssql.conf` に追加して、パスを公開します。

   ```text
   [extensibility]
   readabledirectories = /opt/mssql
   ```

**適用対象:** SQL Server 2019 on Linux

## <a name="r-script-execution-issues"></a>R スクリプトの実行に関する問題

このセクションでは、SQL Server での R の実行に固有の既知の問題と、Microsoft によって公開されている R ライブラリおよびツール (RevoScaleR を含む) に関連するいくつかの問題について説明します。

R ソリューションに影響する可能性があるその他の既知の問題については、[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) のサイトをご覧ください。

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1.既定以外の場所の SQL Server で R スクリプトを実行するときのアクセス拒否警告

SQL Server のインスタンスが既定以外の場所にインストールされている場合 (`Program Files` フォルダーの外部など)、パッケージがインストールされるスクリプトを実行しようとすると、警告 ACCESS_DENIED が発生します。 例:

> *`normalizePath(path.expand(path), winslash, mustWork)` 内: path[2]="~ExternalLibraries/R/8/1": アクセスが拒否されました*

理由は、R 関数でパスの読み取りが試みられ、組み込みのユーザー グループ **SQLRUserGroup** に読み取りアクセス権がない場合は失敗するためです。 発生した警告によって現在の R スクリプトの実行がブロックされることはありませんが、ユーザーが他の R スクリプトを実行するたびに警告が繰り返し発生する可能性があります。

SQL Server が既定の場所にインストールされている場合は、すべての Windows ユーザーが `Program Files` フォルダーに対する読み取りアクセス許可を持っているため、このエラーは発生しません。

この問題は、次のサービス リリースで解決されます。 回避策としては、`ExternalLibraries` のすべての親フォルダーに対する読み取りアクセス権があるグループ **SQLRUserGroup** を指定します。

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2.RevoScaleR の古いバージョンと新しいバージョンの間でのシリアル化エラー

シリアル化された形式を使用しているモデルをリモート SQL Server インスタンスに渡すと、次のエラーが発生する可能性があります。 

> *Error in memDecompress(data, type = decompress) internal error -3 in memDecompress(2).* (memDecompress(data, type = decompress) でのエラー、memDecompress(2) での内部エラー -3。)

このエラーが発生するのは、最新バージョンのシリアル化関数 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) を使用してモデルを保存したにもかかわらず、モデルを逆シリアル化する SQL Server インスタンスに古いバージョンの RevoScaleR API (SQL Server 2017 CU2 以前) が存在する場合です。

この回避策としては、SQL Server 2017 インスタンスを CU3 以降にアップグレードします。

API のバージョンが同じ場合、または古いシリアル化関数で保存されたモデルを、新しいバージョンのシリアル化 API を使用するサーバーに移動する場合は、このエラーは発生しません。

つまり、シリアル化操作と逆シリアル化操作の両方に、同じバージョンの RevoScaleR を使用します。

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3.リアルタイム スコアリングで、ツリー モデルとフォレスト モデルの _learningRate_ パラメーターが正しく処理されない

デシジョン ツリーまたはデシジョン フォレストのメソッドを使用してモデルを作成し、学習速度を指定した場合、`sp_rxpredict` または SQL の `PREDICT` 関数を使用すると、`rxPredict` を使用した場合と比較して、一貫性のない結果が表示されることがあります。

原因は、シリアル化されたモデルを処理する API のエラーであり、[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) などの `learningRate` パラメーターに限定されています。

この問題は、次のサービス リリースで解決されます。

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4.R ジョブのプロセッサ アフィニティに関する制限事項

SQL Server 2016 の初期リリース ビルドでは、最初の k グループの CPU に対してのみ、プロセッサのアフィニティを設定できます。 たとえば、サーバーが 2 k グループの 2 ソケット マシンである場合、最初の k グループのプロセッサのみが R プロセスに使用されます。 R スクリプト ジョブのリソース ガバナンスを構成するときも、同じ制限が適用されます。

この問題は SQL Server 2016 Service Pack 1 で修正されました。 最新のサービス リリースにアップグレードすることをお勧めします。

**適用対象:** SQL Server 2016 R Services RTM バージョン

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5.SQL Server コンピューティング コンテキストでのデータの読み取り時に列の型を変更できない

コンピューティング コンテキストが SQL Server インスタンスに設定されている場合は、 _colClasses_ 引数 (または他の同様の引数) を使用して、R コードで列のデータ型を変更できません。

たとえば、CRSDepTimeStr 列がまだ整数でない場合、次のステートメントでエラーが発生します。

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

回避策としては、CAST または CONVERT を使用し、正しいデータ型を使用して R にデータを提示するように、SQL クエリを書き直します。 一般に、R コードでデータを変更するのではなく、SQL を使用してデータを処理した方が、パフォーマンスが向上します。

**適用対象:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6.シリアル化されたモデルのサイズの制限

モデルを SQL Server のテーブルに保存するときは、モデルをシリアル化し、バイナリ形式で保存する必要があります。 理論的には、この方法で格納できるモデルの最大サイズは 2 GB です。これは SQL Server での varbinary 列の最大サイズです。

さらに大きいモデルを使用する必要がある場合は、次の回避策を使用できます。

+ モデルのサイズを小さくするための手順を実行します。 一部のオープン ソースの R パッケージでは、モデル オブジェクトに大量の情報が収められており、この情報の多くは展開で削除される場合があります。 
+ 機能の選択を使用して不要な列を削除してください。
+ オープン ソースのアルゴリズムを使用している場合は、MicrosoftML または RevoScaleR の対応するアルゴリズムを使用した同様の実装を検討してください。 これらのパッケージは、展開シナリオに合わせて最適化されています。
+ 前の手順を使用してモデルを合理化し、サイズを削減した後は、基の R の [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) 関数を使用して、SQL Server に渡す前にモデルのサイズを縮小できるかどうかを確認します。 このオプションは、モデルが 2 GB の制限に近い場合に最適です。
+ それより大きいモデルでは、varbinary 列を使用するのではなく、SQL Server の [FileTable](../relational-databases/blob/filetables-sql-server.md) 機能を使用してモデルを格納できます。

    FileTable を使用するには、ファイアウォールの例外を追加する必要があります。これは、FileTable に格納されたデータは SQL Server の Filestream ファイル システム ドライバーによって管理され、既定のファイアウォール規則ではネットワーク ファイルへのアクセスがブロックされるためです。 詳しくは、「[FileTable の前提条件の有効化](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)」をご覧ください。

    FileTable を有効にした後、モデルを書き込むには、FileTable API を使用して SQL からパスを取得した後、コードからその場所にモデルを書き込みます。 モデルを読み取る必要がある場合は、SQL からパスを取得した後、そのパスを使用してスクリプトからモデルを呼び出します。 詳しくは、「[ファイル I/O API を使用した FileTable へのアクセス](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)」をご覧ください。

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7.[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンピューティング コンテキストで R コードを実行しているときに、ワークスペースをクリアできない

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンピューティング コンテキストで R コードを実行中に R コマンドを使用してオブジェクトのワークスペースをクリアする場合、または [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して呼び出した R スクリプトの一部としてワークスペースをクリアする場合に、"*ワークスペース オブジェクト revoScriptConnection が見つからない*" というエラーが発生することがあります

`revoScriptConnection` は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]から呼び出される R セッションに関する情報を含む R ワークスペース内のオブジェクトです。 ただし、R コードにワークスペースをクリアするためのコマンド ( `rm(list=ls()))`など) が含まれている場合は、R ワークスペース内のセッションおよび他のオブジェクトに関するすべての情報もクリアされます。

回避策としては、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で R を実行しているときは、変数や他のオブジェクトを無差別にクリアしないようにします。 R コンソールでの操作時にワークスペースをクリアすることはよくありますが、意図しない結果になる場合があります。

+ 特定の変数を削除するには、R の `remove` 関数を使用します (例: `remove('name1', 'name2', ...)`)
+ 削除する変数が複数ある場合は、リストに一時変数の名前を保存し、ガベージ コレクションを定期的に実行します。

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8.R スクリプトの入力として提供できるデータに対する制限事項

次の種類のクエリ結果は、R スクリプトでは使用できません。

- AlwaysEncrypted 列を参照する [!INCLUDE[tsql](../includes/tsql-md.md)] クエリのデータ。
  
- マスクされた列を参照する [!INCLUDE[tsql](../includes/tsql-md.md)] クエリのデータ。
  
     R スクリプトでマスクされたデータを使用する必要がある場合、考えられる次善策として、一時テーブルにデータのコピーを作成し、代わりにそのデータを使用します。

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9.係数として文字列を使用すると、パフォーマンスが低下することがある

係数として文字列型の変数を使用すると、R の演算に使用されるメモリの量が大幅に増えることがあります。 これは、R に関して一般に知られている問題であり、それについての多くの記事があります。 たとえば、「[Factors are not first-class citizens in R](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)」 (R で因子は第一級市民ではない)(John Mount、R-bloggers) や「[stringsAsFactors: An unauthorized biography](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)」(stringsAsFactors:無許可の伝記)(Roger Peng) をご覧ください。 

この問題は SQL Server だけのものではありませんが、SQL Server では R コードの実行のパフォーマンスに大きく影響する可能性があります。 通常、文字列は varchar または nvarchar として格納され、文字列データの列に一意の値が多数含まれている場合、R で内部的にこれらを整数に変換したり文字列に戻したりする処理によって、メモリ割り当てエラーが発生する可能性もあります。

他の操作のために文字列データ型がどうしても必要な場合を除き、データ準備の一部として文字列値を数値 (整数) データ型にマップすると、パフォーマンスとスケーリングの観点で有用です。

この問題とその他のヒントについては、「[R Services のパフォーマンス - データの最適化](r/r-and-data-optimization-r-services.md)」をご覧ください。

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10.引数 *varsToKeep* と *varsToDrop* が SQL Server データ ソースでサポートされていない

rxDataStep 関数を使用してテーブルに結果を書き込む場合、操作の一部として含める列または除外する列を指定する便利な方法として、*varsToKeep* と *Varstokeep* を使用する方法があります。 ただし、これらの引数は SQL Server データ ソースではサポートされていません。

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11.sp\_execute\_external\_script での SQL データ型のサポートの制限

SQL でサポートされているデータ型の一部を R で使用できません。回避策として、サポートされていないデータ型をサポートされているデータ型にキャストしてから、sp\_execute\_external\_script にデータを渡すことを検討してください。

詳しくは、[R のライブラリとデータ型](r/r-libraries-and-data-types.md)に関する記事をご覧ください。

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12.varchar 列で Unicode 文字列を使用すると、文字列が破損する可能性がある

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から R/Python に varchar 列で Unicode データを渡すと、文字列が破損する可能性があります。 これは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の照合順序でのこれらの Unicode 文字列に対するエンコードが、R/Python で使用される既定の UTF-8 エンコードと一致しない可能性があるためです。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から R/Python に ASCII 以外の文字列データを送るには、UTF-8 エンコード ([!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] で使用可能) を使用するか、nvarchar 型を使用します。

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13.`sp_execute_external_script` からは `raw` 型の値を 1 つしか返せない

R から binary データ型 (R の **raw** データ型) を返すときは、出力データ フレームで値を送る必要があります。

**raw** 以外のデータ型では、OUTPUT キーワードを追加することにより、ストアド プロシージャの結果と共にパラメーター値を返すことができます。 詳しくは、「[パラメーター](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)」をご覧ください。

**raw** 型の値が含まれる複数の出力セットを使用する必要がある場合、可能な回避策は、ストアド プロシージャの呼び出しを複数回行うか、ODBC を使用して結果セットを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に返送することです。

### <a name="14-loss-of-precision"></a>14. 精度の損失

[!INCLUDE[tsql](../includes/tsql-md.md)] と R ではさまざまなデータ型がサポートされているため、変換時に数値データ型の精度が損なわれる可能性があります。

暗黙的なデータ型変換について詳しくは、[R のライブラリとデータ型](r/r-libraries-and-data-types.md)に関する記事をご覧ください。

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. transformFunc パラメーターを使用するときの変数スコープ エラー

モデリングの間にデータを変換するには、`rxLinmod` や `rxLogit` などの関数で *transformFunc* 引数を渡すことができます。 ただし、入れ子になった関数呼び出しでは、呼び出しがローカル コンピューティング コンテキストで正しく機能していても、SQL Server のコンピューティング コンテキストではスコープ エラーが発生する可能性があります。

> *The sample data set for the analysis has no variables* (分析用のサンプル データ セットに変数がありません)

たとえば、ローカル グローバル環境で 2 つの関数 `f` と `g` が定義されており、`g` で `f` を呼び出すものとします。 `g` が含まれる分散またはリモートの呼び出しでは、リモート呼び出しに `f` と `g` の両方を渡した場合でも、`f` が見つからないため、`g` の呼び出しがこのエラーで失敗する可能性があります。

この問題が発生した場合は、 `f` の定義内の、通常 `g`が `g` を呼び出す場所より前の任意の場所に、 `f`の定義を組み込むことで問題を回避できます。

例:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

このエラーを回避するには、次のように定義を書き直します。

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. RevoScaleR を使用したデータのインポートと操作

データベースから **varchar** 列が読み取られるときに、空白文字が削除されます。 これを防ぐには、空白以外の文字で文字列を囲みます。

`rxDataStep` などの関数を使用して **varchar** 列が含まれるデータベース テーブルを作成すると、データのサンプルに基づいて列幅が推定されます。 幅が増減する可能性がある場合、すべての文字列を共通の長さにして空白を埋めることが必要な場合があります。

`rxImport` または `rxTextToXdf` の繰り返しの呼び出しを使用して行のインポートと追加を実行し、複数の入力ファイルを 1 つの .xdf ファイルに結合する場合、変換を使用した変数のデータ型の変更はサポートされていません。

### <a name="17-limited-support-for-rxexec"></a>17. rxExec のサポートの制限

SQL Server 2016 では、RevoScaleR パッケージによって提供される `rxExec` 関数は、シングルスレッド モードでのみ使用できます。

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. rxGetVarInfo をサポートするためにパラメーターの最大サイズを増やす

非常に多くの変数 (40,000 個以上など) が含まれたデータ セットを使用する場合は、`rxGetVarInfo` などの関数を使用するために R を開始するときに、`max-ppsize` フラグを設定する必要があります。 `max-ppsize` フラグは、ポインター保護スタックの最大サイズを指定します。

R コンソール (RGui.exe や RTerm.exe など) を使用している場合、次のように入力することで _max-ppsize_ の値を 500,000 に設定できます。

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. rxDTree 関数に関する問題

`rxDTree` 関数では、式内変換は現在サポートされていません。 特に、係数を即座に作成するための `F()` 構文の使用はサポートされていません。 ただし、数値データは自動的にビン分割されます。

順序付けされた係数は、 `rxDTree`を除くすべての RevoScaleR 分析関数の係数と同様に処理されます。

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. R での OutputDataSet としての Data.table

R で `OutputDataSet` として `data.table` を使用することは、SQL Server 2017 累積的な更新プログラム 13 (CU13) 以前ではサポートされていません。 次のメッセージが表示されることがあります。

``` text
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

R での `OutputDataSet` としての `data.table` は、SQL Server 2017 累積的な更新プログラム 14 (CU14) 以降ではサポートされています。

### <a name="21-running-a-long-script-fails-while-installing-a-library"></a>21. ライブラリのインストール中に長いスクリプトの実行が失敗する

実行時間の長い外部スクリプト セッションを実行し、dbo で並列に別のデータベースにライブラリをインストールしようとすると、スクリプトが終了する場合があります。

たとえば、master に対して次の外部スクリプトを実行します。

```sql
USE MASTER
DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(max) = N'Sys.sleep(100)'
DECLARE @input_data_1 nvarchar(max) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1 with result sets none
go
```

その間に並列に dbo でライブラリを LibraryManagementFunctional にインストールします。

```sql
USE [LibraryManagementFunctional]
go

CREATE EXTERNAL LIBRARY [RODBC] FROM (CONTENT = N'/home/ani/var/opt/mssql/data/RODBC_1.3-16.tar.gz') WITH (LANGUAGE = 'R')
go

DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(14) = N'library(RODBC)'
DECLARE @input_data_1 nvarchar(8) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1
go
```

前の master に対する実行時間の長い外部スクリプトは、次のエラー メッセージで終了します。

> *'sp_execute_external_script' に HRESULT 0x800704d4 を指定して実行中に、'R' スクリプト エラーが発生しました。*

**回避策**

実行時間の長いクエリと並列にライブラリのインストールを実行しないでください。 または、インストールが完了した後で、実行時間の長いクエリを再実行します。

**適用対象:** SQL Server 2019 on Linux とビッグ データ クラスターのみ。

## <a name="python-script-execution-issues"></a>Python スクリプトの実行に関する問題

このセクションでは、SQL Server での Python の実行に固有の既知の問題と、Microsoft によって公開されている Python パッケージ ([revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) や [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package) など) に関連する問題について説明します。

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1.モデルへのパスが長すぎると、事前トレーニング済みモデルの呼び出しが失敗する

SQL Server 2017 の早期リリースに事前トレーニング済みモデルをインストールした場合、トレーニング済みモデル ファイルへの完全なパスが、Python で読み取るには長すぎる可能性があります。 この制限は、後のサービス リリースでは修正されています。

考えられる回避策がいくつかあります。

+ 事前トレーニング済みモデルをインストールするときに、カスタムの場所を選択します。
+ 可能な場合は、C:\SQL\MSSQL14.MSSQLSERVER などの短いパスを使用して、カスタム インストール パスに SQL Server インスタンスをインストールします。
+ Windows ユーティリティ [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) を使用して、モデル ファイルを短いパスにマップするハード リンクを作成します。
+ 最新のサービス リリースに更新します。

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2.シリアル化されたモデルを SQL Server に保存するときのエラー

リモート SQL Server インスタンスにモデルを渡し、[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) で `rx_unserialize` 関数を使用してバイナリモデルを読み取ろうとすると、次のエラーが表示されることがあります。 

> *NameError: 名前 'rx_unserialize_model' が定義されていません*

このエラーが発生するのは、最新バージョンのシリアル化関数を使用してモデルを保存したのに、モデルを逆シリアル化する SQL Server インスタンスでシリアル化 API が認識されない場合です。

問題を解決するには、SQL Server 2017 インスタンスを CU3 以降にアップグレードします。

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3.varbinary 変数を初期化できないと、BxlServer でエラーが発生する

`sp_execute_external_script` を使用して SQL Server で Python コードを実行し、そのコードに varbinary(max)、varchar(max)、またはそれに類する型の出力変数がある場合は、変数を初期化するか、スクリプトの一部として設定する必要があります。 そうしないと、データ交換コンポーネント BxlServer でエラーが発生し、動作が停止します。

この制限は、今後のサービス リリースで修正される予定です。 回避策としては、変数が Python スクリプト内で初期化されていることを確認します。 次の例のように、任意の有効な値を使用できます。

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4.Python コードが正常に実行された場合のテレメトリに関する警告

SQL Server 2017 CU2 以降では、Python コードが正常に実行された場合でも、次のメッセージが表示されることがあります。

> *外部スクリプトからの STDERR メッセージ: *
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state がグローバル宣言の前で使用されています*

この問題は、SQL Server 2017 累積的な更新プログラム 3 (CU3) で修正されました。 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5.数値、10 進、通貨の各データ型がサポートされていない

SQL Server 2017 累積的な更新プログラム 12 (CU12) 以降では、`sp_execute_external_script` で Python を使用する場合、WITH RESULT SETS では数値、10 進、通貨の各データ型がサポートされていません。 次のメッセージが表示されることがあります。

> *[コード: 39004、SQL の状態: S1000] 'sp_execute_external_script' に HRESULT 0x80004004 を指定して実行中に、'Python' スクリプト エラーが発生しました。*
>
> *[コード: 39019、SQL の状態: S1000] 外部スクリプト エラーが発生しました:*
>
> *SqlSatelliteCall エラー: 出力スキーマでサポートされていない型です。サポートされている型: bit、smallint、int、datetime、smallmoney、real、および float。char、varchar は部分的にサポートされています。*

これは、SQL Server 2017 累積的な更新プログラム 14 (CU14) で修正されました。

### <a name="6-bad-interpreter-error-when-installing-python-packages-with-pip-on-linux"></a>6.Linux で pip を使用して Python パッケージをインストールするときの不正インタープリター エラー 

SQL Server 2019 で **pip** を使用しようとした場合。 例:

```bash
/opt/mssql/mlservices/runtime/python/bin/pip -h
```

次のエラーが表示されます。

> *bash:/opt/mssql/mlservices/runtime/python/bin/pip:/opt/microsoft/mlserver/9.4.7/bin/python/python: 不正インタープリター: ファイルまたはディレクトリが存在しません*

**回避策**

[Python Package Authority (PyPA)](https://www.pypa.io) から **pip** をインストールします。

```bash
wget 'https://bootstrap.pypa.io/get-pip.py' 
/opt/mssql/mlservices/bin/python/python ./get-pip.py 
```

**推奨**

「[sqlmlutils を使用して Python パッケージをインストールする](package-management/install-additional-python-packages-on-sql-server.md)」をご覧ください。

**適用対象:** SQL Server 2019 on Linux

### <a name="7-unable-to-install-python-packages-using-pip-after-installing-sql-server-2019-on-windows"></a>7.SQL Server 2019 を Windows にインストールした後、pip を使用して Python パッケージをインストールできない

Windows に SQL Server 2019 をインストールした後、DOS コマンド ラインから **pip** を使用して python パッケージをインストールしようとすると失敗します。 例:

```bash
pip install quantfolio
```

次のエラーが返されます。

> *pip は TLS/SSL を必要とする場所で構成されていますが、Python の SSL モジュールは使用できません。*

これは、Anaconda パッケージに固有の問題です。 今後のサービス リリースで修正される予定です。

**回避策**

次のファイルをコピーします。

+ `libssl-1_1-x64.dll`
+ `libcrypto-1_1-x64.dll`

コピー元フォルダー <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\Library\bin`

コピー先フォルダー <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\DLLs`

その後、新しい DOS コマンド シェル プロンプトを開きます。

**適用対象:** SQL Server 2019 on Windows

### <a name="8-error-when-using-sp_execute_external_script-without-libcaboso-on-linux"></a>8.Linux で `libc++abo.so` を使用せずに `sp_execute_external_script` を使用するときのエラー

`libc++abi.so` がインストールされていないクリーンな Linux マシンでは、`sp_execute_external_script` (SPEES) クエリを実行すると、"そのようなファイルやディレクトリはない" というエラーで失敗します。

例:

```text
EXEC sp_execute_external_script
    @language = N'Python'
    , @script = N'
OutputDataSet = InputDataSet'
    , @input_data_1 = N'select 1'
    , @input_data_1_name = N'InputDataSet'
    , @output_data_1_name = N'OutputDataSet'
    WITH RESULT SETS (([output] int not null));
Msg 39012, Level 16, State 14, Line 0
Unable to communicate with the runtime for 'Python' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Python' runtime.
STDERR message(s) from external script:

Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.

SqlSatelliteCall error: Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.
STDOUT message(s) from external script:
SqlSatelliteCall function failed. Please see the console output for more information.
Traceback (most recent call last):
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/computecontext/RxInSqlServer.py", line 605, in rx_sql_satellite_call
    rx_native_call("SqlSatelliteCall", params)
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/RxSerializable.py", line 375, in rx_native_call
    ret = px_call(functionname, params)
RuntimeError: revoscalepy function failed.
Total execution time: 00:01:00.387
```

**回避策**

次のコマンドを実行します。

```bash
sudo cp /opt/mssql/lib/libc++abi.so.1 /opt/mssql-extensibility/lib/
```

**適用対象:** SQL Server 2019 on Linux

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise と Microsoft R Open

このセクションでは、Revolution Analytics によって提供される R の接続、開発、およびパフォーマンス ツールに固有の問題を示します。 これらのツールは、以前のプレリリース版の [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] で提供されていました。

一般的には、これらの以前のバージョンをアンインストールして、最新バージョンの SQL Server または Microsoft R Server をインストールすることをお勧めします。

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1.Revolution R Enterprise はサポートされていない

Revolution R Enterprise をインストールして任意のバージョンの [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] と共存させることはできません。

Revolution R Enterprise の既存ライセンスがある場合は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスへの接続に使用するワークステーションとは別のコンピューターに、ライセンスを配置する必要があります。

一部のプレリリース版の [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] には、Revolution Analytics によって作成された Windows 用の R 開発環境が含まれていました。 このツールは提供されなくなっており、サポートされていません。

[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] との互換性のため、代わりに Microsoft R Client をインストールすることをお勧めします。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) と [Visual Studio Code](https://code.visualstudio.com/) でも、Microsoft R ソリューションがサポートされています。

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2.SQLite ODBC ドライバーと RevoScaleR に関する互換性の問題

SQLite ODBC ドライバーのリビジョン 0.92 は、RevoScaleR と互換性がありません。 リビジョン 0.88 - 0.91 および 0.93 以降には、互換性があることがわかっています。

## <a name="next-steps"></a>次の手順

[SQL Server での機械学習のトラブルシューティング](machine-learning-troubleshooting-faq.md)
