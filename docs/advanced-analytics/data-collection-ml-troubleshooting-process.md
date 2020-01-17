---
title: データ収集のトラブルシューティング
description: 問題を自分で、または Microsoft カスタマー サポートの支援を受けながら解決するときに使用する必要があるデータ収集方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15c570594f84bf8d1d61abac4bc4e4c372f18784
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727606"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>機械学習のためのデータ収集のトラブルシューティング

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、問題を自分で、または Microsoft カスタマー サポートの支援を受けながら解決するときに使用する必要があるデータ収集方法について説明します。

## <a name="sql-server-version-and-edition"></a>SQL Server のバージョンおよびエディション

SQL Server 2016 R Services は、R の統合サポートが含まれる SQL Server の最初のリリースです。 SQL Server 2016 Service Pack 1 (SP1) には、外部スクリプトを実行する機能など、いくつかの重要な機能強化が含まれています。 SQL Server 2016 を使用している場合は、SP1 以降をインストールすることを検討してください。

SQL Server 2017 以降には Python 言語が統合されています。 以前のリリースでは、Python 機能を統合できません。

エディションとバージョンの取得については、[SQL Server バージョン](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)ごとのビルド番号が一覧表示されている、こちらの記事を参照してください。

使用している SQL Server のエディションによっては、一部の機械学習機能が使用できないか、制限される場合があります。 次の記事では、Enterprise、Developer、Standard、および Express の各エディションの機械学習機能の一覧を示します。

* [SQL Server の各エディションとサポートされている機能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [SQL Server のエディションごとの R および Python の機能](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 言語とツールのバージョン

一般に、R Services 機能または Machine Learning Services 機能を選択したときにインストールされる Microsoft R のバージョンは、SQL Server のビルド番号によって決まります。 SQL Server をアップグレードまたは修正する場合は、その R コンポーネントもアップグレードまたは修正する必要があります。

R コンポーネントのダウンロードに関するリリースとリンクの一覧については、[インターネット アクセスを使用しない機械学習コンポーネントのインストール](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)に関する記事を参照してください。 インターネットにアクセスできるコンピューターでは、必要なバージョンの R が自動的に識別され、インストールされます。

バインドと呼ばれるプロセスでは、R Server コンポーネントを SQL Server データベース エンジンとは別にアップグレードすることができます。 そのため、SQL Server で R コードを実行するときに使用する R のバージョンは、インストールされている SQL Server のバージョンと、サーバーを最新の R バージョンに移行したかどうかによって異なる場合があります。

### <a name="determine-the-r-version"></a>R バージョンを確認する

R バージョンを確認する最も簡単な方法は、次のようなステートメントを実行してランタイム プロパティを取得することです。

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> R Services が動作していない場合は、RGui から R スクリプトの部分のみを実行してみてください。

最後の手段として、サーバー上のファイルを開いて、インストールされているバージョンを確認できます。 これを行うには、rlauncher.config ファイルを見つけて、R ランタイムの場所と現在の作業ディレクトリを調べます。 プロパティを誤って変更しないように、ファイルのコピーを作成して開くことをお勧めします。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

R バージョンと RevoScaleR バージョンを調べるには、R のコマンド プロンプトを開くか、インスタンスに関連する RGui を開きます。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R コンソールには、スタートアップ時にバージョン情報が表示されます。 たとえば、次のバージョンは、SQL Server 2017 の既定の構成を表しています。

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python のバージョン

Python のバージョンを調べるには、いくつかの方法があります。 最も簡単な方法は、Management Studio またはその他の SQL クエリ ツールからこのステートメントを実行することです。

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

Machine Learning Services が実行されていない場合は、pythonlauncher.config ファイルを参照して、インストールされている Python のバージョンを確認できます。 プロパティを誤って変更しないように、ファイルのコピーを作成して開くことをお勧めします。

1. SQL Server 2017 の場合のみ: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. **PYTHON HOME** の値を取得します。
3. 現在の作業ディレクトリの値を取得します。

> [!NOTE]
> SQL Server 2017 に Python と R の両方をインストールした場合、作業ディレクトリとワーカー アカウントのプールは、R 言語と Python 言語で共有されます。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>R または Python の複数のインスタンスがインストールされていますか?

R ライブラリの複数のコピーがコンピューターにインストールされているかどうかを確認します。 この重複は、次の場合に発生する可能性があります。

* セットアップ中に、R Services (データベース内) と R Server (スタンドアロン) の両方を選択した。
* SQL Server に加えて Microsoft R Client をインストールした。
* R Tools for Visual Studio、R Studio、Microsoft R Client、または別の R IDE を使用して、別の R ライブラリ セットをインストールした。
* コンピューターが SQL Server の複数のインスタンスをホストし、複数のインスタンスが機械学習を使用する。

Python にも同じ条件が適用されます。

複数のライブラリまたはランタイムがインストールされていることが判明した場合は、SQL Server インスタンスで使用されている Python または R ランタイムに関連するエラーのみを取得してください。

## <a name="origin-of-errors"></a>エラーの発生元

R コードを実行しようとすると、次のいずれかのソースからエラーが発生する可能性があります。

* SQL Server データベース エンジン (ストアド プロシージャ sp_execute_external_script を含む)
* SQL Server Trusted Launchpad
* 拡張機能フレームワークのその他のコンポーネント (R および Python ランチャー、サテライト プロセスを含む)
* Microsoft Open Database Connectivity (ODBC) などのプロバイダー
* R 言語

サービスを初めて使用するときは、どのメッセージがどのサービスから発信されたものかを判断するのが難しい場合があります。 正確なメッセージ テキストだけでなく、メッセージが表示されたコンテキストも取得することをお勧めします。 機械学習コードを実行するために使用しているクライアント ソフトウェアを確認します。

* Management Studio を使用していますか? 外部アプリケーションですか?
* R コードをリモート クライアントで実行していますか、それともストアド プロシージャで直接実行していますか?

## <a name="sql-server-log-files"></a>SQL Server のログ ファイル

最新の SQL Server ERRORLOG を取得します。 エラー ログの完全なセットは、次の既定のログ ディレクトリのファイルで構成されます。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 正確なフォルダー名は、インスタンス名によって異なります。

## <a name="errors-returned-by-sp_execute_external_script"></a>sp_execute_external_script によって返されるエラー

sp_execute_external_script コマンドの実行時に返されるエラー (存在する場合) の完全なテキストを取得します。

R または Python の問題を考慮の対象から除外するには、このスクリプトを実行します。これにより、R または Python ランタイムが起動し、データをやり取りします。

**R の場合**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python の場合**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>拡張機能フレームワークによって生成されるエラー

SQL Server では、外部スクリプト言語ランタイムごとに個別のログが生成されます。 これらのエラーは Python 言語または R 言語では生成されません。 これらは、言語固有のランチャーとそのサテライト プロセスなど、SQL Server の拡張機能コンポーネントから生成されます。

これらのログは、次の既定の場所から取得できます。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 正確なフォルダー名は、インスタンス名によって異なります。 構成によっては、フォルダーが別のドライブにある場合があります。

たとえば、次のログ メッセージは拡張機能フレームワークに関連しています。

* *LogonUser Failed for user MSSQLSERVER01 (ユーザー MSSQLSERVER01 の LogonUser に失敗しました)*
  
  これは、外部スクリプトを実行するワーカー アカウントがインスタンスにアクセスできないことを示している可能性があります。

* *InitializePhysicalUsersPool Failed (InitializePhysicalUsersPool が失敗しました)*
  
  このメッセージは、セキュリティ設定が原因で、外部スクリプトを実行するために必要なワーカー アカウントのプールが作成されないことを意味している可能性があります。

* *Security Context Manager initialization failed (セキュリティ コンテキスト マネージャーの初期化に失敗しました)*

* *Satellite Session Manager initialization failed (サテライト セッション マネージャーの初期化に失敗しました)*

## <a name="system-events"></a>システム イベント

1. Windows イベント ビューアーを開き、**システム イベント** ログで、文字列 *Launchpad* を含むメッセージを検索します。
2. ExtLaunchErrorlog ファイルを開き、文字列 *ErrorCode* を探します。 ErrorCode に関連するメッセージを確認します。

たとえば、次のメッセージは SQL Server 拡張機能フレームワークに関連する一般的なシステム エラーです。

* *SQL Server Launchpad (MSSQLSERVER) サービスは次のエラーのため開始できませんでした: <text>*

* *そのサービスは指定時間内に開始要求または制御要求に応答しませんでした。*

* *A timeout was reached (120000 milliseconds) while waiting for the SQL Server Launchpad (MSSQLSERVER) service to connect. (SQL Server Launchpad (MSSQLSERVER) サービスの接続待機中にタイムアウトになりました (120000 ミリ秒)。)*

## <a name="dump-files"></a>ダンプ ファイル

デバッグに精通している場合は、ダンプ ファイルを使用して Launchpad のエラーを分析できます。

1. SQL Server のセットアップ ブートストラップ ログが格納されているフォルダーを見つけます。 たとえば SQL Server 2016 では、既定のパスは C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log でした。
2. 拡張機能に固有のブートストラップ ログ サブフォルダーを開きます。
3. サポート リクエストを送信する必要がある場合は、このフォルダーの内容全体を ZIP ファイルに追加します。 たとえば、C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog です。
  
正確な場所はシステムによって異なる場合があり、C ドライブ以外のドライブに配置されている場合があります。 必ず機械学習がインストールされているインスタンスのログを取得してください。

## <a name="configuration-settings"></a>構成設定

このセクションでは、R または Python スクリプトを実行したときにエラーの原因となる可能性がある追加のコンポーネントまたはプロバイダーを示します。

### <a name="what-network-protocols-are-available"></a>どのようなネットワーク プロトコルを使用できますか?

Machine Learning Services では、拡張機能コンポーネント間の内部通信、および外部の R クライアントまたは Python クライアントとの通信に次のネットワーク プロトコルが必要です。

* 名前付きパイプ
* TCP/IP

SQL Server 構成マネージャーを開いて、プロトコルがインストールされているかどうかを確認し、インストールされている場合は有効になっているかどうかを確認します。

### <a name="security-configuration-and-permissions"></a>セキュリティの構成およびアクセス許可

ワーカー アカウントの場合:

1. コントロール パネルで、 **[ユーザーとグループ]** を開き、外部スクリプト ジョブを実行するために使用するグループを探します。 既定では、そのグループは **SQLRUserGroup** です。
2. そのグループが存在し、少なくとも 1 つのワーカー アカウントが含まれていることを確認してください。
3. SQL Server Management Studio で、R ジョブまたは Python ジョブを実行するインスタンスを選択し、 **[セキュリティ]** を選択して、SQLRUserGroup のログオンがあるかどうかを確認します。
4. ユーザー グループのアクセス許可を確認します。

個々のユーザー アカウントの場合:

1. インスタンスが混合モード認証、SQL ログインのみ、または Windows 認証のみのいずれをサポートするかを判断します。 この設定は、R または Python のコード要件に影響します。
2. R コードを実行する必要があるユーザーごとに、R からオブジェクトが書き込まれる、データにアクセスする、またはオブジェクトが作成される各データベースで必要なアクセス許可のレベルを決定します。
3. スクリプトの実行を有効にするには、必要に応じて、ロールを作成するか、次のロールにユーザーを追加します。

   - *db_owner* を除くすべて:EXECUTE ANY EXTERNAL SCRIPT が必要です。
   - *db_datawriter*:R または Python から結果を書き込む。
   - *db_ddladmin*:新しいオブジェクトを作成する。
   - *db_datareader*:R または Python のコードによって使用されるデータを読み取る。
4. SQL Server 2016 をインストールしたときに、既定のスタートアップ アカウントを変更したかどうかに注意してください。
5. ユーザーが新しい R パッケージをインストールする必要がある場合、または他のユーザーによってインストールされた R パッケージを使用する必要がある場合は、インスタンスでパッケージ管理を有効にしてから、追加のアクセス許可を割り当てることが必要な場合があります。 詳細については、[R パッケージ管理の有効化または無効化](r/r-package-how-to-enable-or-disable.md)に関する記事を参照してください。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>ウイルス対策ソフトウェアによるロックの対象となるフォルダーは何ですか?

ウイルス対策ソフトウェアによってフォルダーがロックされる可能性があり、それにより機械学習機能のセットアップとスクリプトの正常な実行の両方が妨げられます。 SQL Server ツリー内のフォルダーがウイルス スキャンの対象になるかどうかを判断してください。

ただし、1 つのインスタンスに複数のサービスまたは機能がインストールされている場合、そのインスタンスで使用されている可能性のあるすべてのフォルダーを列挙することは困難な場合があります。 たとえば、新しい機能が追加されたときに、新しいフォルダーを識別して除外する必要があります。

また、実行時に新しいフォルダーを動的に作成する機能もあります。 たとえば、インメモリ OLTP テーブル、ストアド プロシージャ、および関数はすべて、実行時に新しいディレクトリを作成します。 これらのフォルダー名には多くの場合 GUID が含まれており、予測できません。 SQL Server Trusted Launchpad は、R および Python のスクリプト ジョブ用の新しい作業ディレクトリを作成します。

SQL Server プロセスとその機能に必要なすべてのフォルダーを除外することはできない場合があるため、SQL Server インスタンス ディレクトリ ツリー全体を除外することをお勧めします。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>ファイアウォールは SQL Server に対して開いていますか? インスタンスはリモート接続をサポートしていますか?

1. SQL Server がリモート接続をサポートしているかどうかを判断するには、[リモート サーバー接続の構成](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)に関する記事を参照してください。

2. SQL Server に対してファイアウォール規則が作成されているかどうかを確認します。 セキュリティ上の理由から、既定のインストールでは、リモート R または Python クライアントがインスタンスに接続できない場合があります。 詳細については、[SQL Server への接続のトラブルシューティング](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)に関する記事を参照してください。

## <a name="see-also"></a>参照

[SQL Server での機械学習のトラブルシューティング](machine-learning-troubleshooting-faq.md)
