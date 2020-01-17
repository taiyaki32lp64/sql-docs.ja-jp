---
title: コマンド プロンプトからのインストール
description: SQL Server のコマンド ライン セットアップを実行して、R 言語と Python の統合を SQL Server データベース エンジンのインスタンスに追加します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2bc231a064862c5e2a16f60d85a5166fd4765566
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727587"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>コマンド ラインから SQL Server Machine Learning R および Python コンポーネントをインストールする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、コマンド ラインから SQL Server の機械学習コンポーネントをインストールする手順について説明します。

+ [新しい In-Database インスタンス](#indb)
+ [既存のデータベース エンジンのインスタンスに追加する](#add-existing)
+ [サイレント インストール](#silent)
+ [新しいスタンドアロン サーバー](#shared-feature)

セットアップのユーザー インターフェイスには、サイレント、基本、または完全な対話方式を指定できます。 この記事では、「[コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を補足し、R および Python の機械学習コンポーネントに固有のパラメーターについて説明します。

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

+ 管理者特権でのコマンド プロンプトでコマンドを実行してください。 

+ In-Database のインストールには、データベース エンジンのインスタンスが必要です。 R または Python の機能だけをインストールすることはできませんが、[既存のインスタンスにそれらを段階的に追加することはできます](#add-existing)。 データベース エンジンなしで R と Python のみが必要な場合は、[スタンドアロン サーバー](#shared-feature)をインストールします。

+ フェールオーバー クラスターにはインストールしないでください。 R および Python のプロセスの分離に使用されるセキュリティ上のメカニズムは、Windows Server フェールオーバー クラスター環境との互換性がありません。

+ ドメイン コントローラーにはインストールしないでください。 セットアップの Machine Learning Services の部分が失敗します。

+ 同じコンピューター上に、スタンドアロン インスタンスと In-Database インスタンスをインストールすることは避けてください。 スタンドアロン サーバーが同じリソースの奪い合いをするため、両方のインストールのパフォーマンスが低下することになります。


## <a name="command-line-arguments"></a>コマンド ライン引数

ライセンス条項の契約と同様に、FEATURES 引数は必須です。 

コマンド プロンプトを使用してインストールする場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、/Q パラメーターを使用した非表示モード、または /QS パラメーターを使用した簡易非表示モードがサポートされます。 /QS スイッチでは、進捗状況のみが表示され、入力はできません。また、該当する場合でもエラー メッセージは表示されません。 /QS パラメーターは、/Action=install を指定した場合にのみサポートされます。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| 引数 | [説明] |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | In-Database バージョンをインストールします:SQL Server R Services (In-Database)。  |
| /FEATURES = SQL_SHARED_MR | スタンドアロン バージョンの R 機能をインストールします:SQL Server R Server (スタンドアロン)。 スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。|
| /IACCEPTROPENLICENSETERMS  | オープンソースの R コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTPYTHONLICENSETERMS | Python コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server を使用するためのライセンス条項に同意したことを示します。|
| /MRCACHEDIRECTORY | オフライン セットアップでは、R コンポーネントの CAB ファイルを含んだフォルダーを設定します。 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
| 引数 | [説明] |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | In-Database バージョンをインストールします:SQL Server Machine Learning Services (In-Database)。  |
| /FEATURES = SQL_INST_MR | AdvancedAnalytics と組み合わせて使用します。 Microsoft R Open や R の専用パッケージなど、(In-Database) R 機能をインストールします。 |
| /FEATURES = SQL_INST_MPY | AdvancedAnalytics と組み合わせて使用します。 Anaconda や Python の専用パッケージなど、(In-Database) Python 機能をインストールします。 |
| /FEATURES = SQL_SHARED_MR | スタンドアロン バージョンの R 機能をインストールします:SQL Server Machine Learning Server (スタンドアロン)。 スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。|
| /FEATURES = SQL_SHARED_MPY | スタンドアロン バージョンの Python 機能をインストールします:SQL Server Machine Learning Server (スタンドアロン)。 スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。|
| /IACCEPTROPENLICENSETERMS  | オープンソースの R コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTPYTHONLICENSETERMS | Python コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server を使用するためのライセンス条項に同意したことを示します。|
| /MRCACHEDIRECTORY | オフライン セットアップでは、R コンポーネントの CAB ファイルを含んだフォルダーを設定します。 |
| /MPYCACHEDIRECTORY | 将来の使用のために予約されています。 インターネットに接続されていないコンピューターへのインストール用に、%TEMP% を使って Python コンポーネントの CAB ファイルを格納します。 |
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
| 引数 | [説明] |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | In-Database バージョンをインストールします:SQL Server Machine Learning Services (In-Database)。  |
| /FEATURES = SQL_INST_MR | AdvancedAnalytics と組み合わせて使用します。 Microsoft R Open や R の専用パッケージなど、(In-Database) R 機能をインストールします。 |
| /FEATURES = SQL_INST_MPY | AdvancedAnalytics と組み合わせて使用します。 Anaconda や Python の専用パッケージなど、(In-Database) Python 機能をインストールします。 |
| /FEATURES = SQL_INST_MJAVA | AdvancedAnalytics と組み合わせて使用します。 Open JRE など、(In-Database) Java 機能をインストールします。 |
| /FEATURES = SQL_SHARED_MR | スタンドアロン バージョンの R 機能をインストールします:SQL Server Machine Learning Server (スタンドアロン)。 スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。|
| /FEATURES = SQL_SHARED_MPY | スタンドアロン バージョンの Python 機能をインストールします:SQL Server Machine Learning Server (スタンドアロン)。 スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。|
| /IACCEPTROPENLICENSETERMS  | オープンソースの R コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTPYTHONLICENSETERMS | Python コンポーネントを使用するためのライセンス条項に同意したことを示します。 |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server を使用するためのライセンス条項に同意したことを示します。|
| /MRCACHEDIRECTORY | オフライン セットアップでは、R コンポーネントの CAB ファイルを含んだフォルダーを設定します。 |
| /MPYCACHEDIRECTORY | 将来の使用のために予約されています。 インターネットに接続されていないコンピューターへのインストール用に、%TEMP% を使って Python コンポーネントの CAB ファイルを格納します。 |
::: moniker-end

## <a name="indb"></a> In-Database インスタンスのインストール

データベース エンジンのインスタンスでは、In-Database 分析を利用できます。これは、インストールに **AdvancedAnalytics** 機能を追加するために必須です。 高度な分析と共にデータベース エンジンのインスタンスをインストールすることも、[それを既存のインスタンスに追加する](#add-existing)ことも可能です。 

対話型の画面の指示なしで進行状況を表示するには、/qs 引数を使用します。

> [!IMPORTANT]
> インストール後も、追加の構成手順が 2 つ残っています。 これらのタスクを実行するまで、統合は完了しません。 手順については、[インストール後のタスク](#post-install)に関する記事をご覧ください。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Machine Learning Services: Python および R を使用したデータベース エンジンと高度な分析

データベース エンジンのインスタンスの同時インストール用に、インスタンス名と管理者 (Windows) ログインを指定します。 コア コンポーネントと言語コンポーネントをインストールするための機能に加えて、すべてのライセンス条項への同意も含めます。

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

次は同じコマンドですが、混合認証を使用し、データベース エンジンに対する SQL Server ログインが含まれています。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Python のみの次の例では、機能を 1 つ省略することで、言語を 1 つ追加できることを示しています。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: R を使用したデータベース エンジンと高度な分析

データベース エンジンのインスタンスの同時インストール用に、インスタンス名と管理者 (Windows) ログインを指定します。 コア コンポーネントと言語コンポーネントをインストールするための機能に加えて、すべてのライセンス条項への同意も含めます。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install"></a> インストール後の構成 (必須)

In-Database インストールにのみ適用されます。

セットアップが完了すると、R および Python を使用したデータベース エンジンのインスタンス、Microsoft の R および Python のパッケージ、Microsoft R Open、Anaconda、ツール、サンプル、およびディストリビューションの一部であるスクリプトが揃います。 

インストールを完了するには、さらに 2 つのタスクが必要です。


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. データベース エンジン サービスを再起動します。

1. SQL Server Machine Learning Services:機能を使用する前に、外部スクリプトを有効にする必要があります。 次の手順として、[SQL Server Machine Learning Services (In-Database) のインストール](sql-machine-learning-services-windows-install.md)に関する記事に記載されている手順に従ってください。 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. データベース エンジン サービスを再起動します。

1. SQL Server R Services:機能を使用する前に、外部スクリプトを有効にする必要があります。 次の手順として、[SQL Server R Services (In-Database) のインストール](sql-r-services-windows-install.md)に関する記事に記載されている手順に従ってください。 
::: moniker-end

## <a name="add-existing"></a> 既存のデータベース エンジンのインスタンスに高度な分析を追加する

既存のデータベース エンジンのインスタンスに In-Database の高度な分析を追加する場合は、インスタンス名を指定します。 たとえば、以前に SQL Server 2017 以降のデータベース エンジンと Python をインストールした場合、次のコマンドを使用して R を追加できます。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent"></a> サイレント インストール

サイレント インストールでは、.cab ファイルの場所のチェックが抑制されます。 このため、.cab ファイルがアンパックされる場所を指定する必要があります。 Python の場合、CAB ファイルは %TEMP* に配置する必要があります。 R の場合、この一時ディレクトリを使用してフォルダー パスを設定できます。
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> スタンドアロン サーバーのインストール

スタンドアロン サーバーは、データベース エンジンのインスタンスにバインドされない "共有機能" です。 スタンドアロン サーバーをインストールするための有効な構文を、以下の例に示します。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server では、スタンドアロン サーバー上で Python と R がサポートされています。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Server は R のみです。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

セットアップが完了すると、サーバー、Microsoft のパッケージ、R と Python のオープンソース ディストリビューション、ツール、サンプル、およびディストリビューションの一部であるスクリプトが揃います。 

R のコンソール ウィンドウを開くには、`\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64` に移動し、**RGui.exe** をダブルクリックします。 R は初めてですか。 次のチュートリアルをお試しください:「[基本的な R コマンドと RevoScaleR 関数:25 個の一般的な例](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)」。

Python コマンドを開くには、`\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64` に移動し、**python.exe** をダブルクリックします。

## <a name="get-help"></a>ヘルプの参照

インストールまたはアップグレードに関するヘルプが必要ですか。 一般的な質問と既知の問題に対する回答については、次の記事を参照してください。

* [アップグレードとインストールの FAQ - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

インスタンスのインストール状態を確認し、よくある問題を解決するには、次のカスタム レポートをお試しください。

* [SQL Server のカスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>次の手順

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクをご覧ください。

+ [チュートリアル: T-SQL での R の実行](../tutorials/quickstart-r-create-script.md)
+ [チュートリアル: R 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [チュートリアル: T-SQL での Python の実行](../tutorials/run-python-using-t-sql.md)
+ [チュートリアル: Python 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

実際のシナリオに基づいた機械学習の例については、[機械学習のチュートリアル](../tutorials/machine-learning-services-tutorials.md)を参照してください。