---
title: Launchpad に関する一般的な問題
description: この記事では、SQL Server Trusted Launchpad サービスの開始を妨げるさまざまな問題のトラブルシューティングの指針を示します。これには、構成の問題または変更や、不足するネットワーク プロトコルなどが含まれます。
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68c731767a83acbd4b7df84843f2c140c5a63d3e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727708"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>SQL Server での Launchpad サービスと外部スクリプト実行に関する一般的な問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Trusted Launchpad サービスでは、R および Python の外部スクリプト実行がサポートされています。 

構成の問題または変更や、不足するネットワーク プロトコルなどの複数の問題により、Launchpad が起動しないことがあります。 この記事では、さまざまな問題のトラブルシューティングの指針を示します。 記載がない件については、[Machine Learning Server フォーラム](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)に質問を投稿できます。

## <a name="determine-whether-launchpad-is-running"></a>Launchpad が実行されているかどうかを判断する

1. **[サービス]** パネル (services.msc) を開きます。 または、コマンド ラインで「**Sqlservermanager13.msc**」または「**SQLServerManager14**」と入力して、[SQL Server 構成マネージャー](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)を開きます。

2. Launchpad が実行されているサービス アカウントをメモします。 R または Python が有効になっている各インスタンスには、Launchpad サービスの独自のインスタンスが必要です。 たとえば、名前付きインスタンスのサービスは、_MSSQLLaunchpad$InstanceName_ のようになります。

3. サービスが停止している場合は再起動します。 再起動時に構成に問題がある場合は、システム イベント ログにメッセージが発行され、サービスが再度停止されます。 システム イベント ログで、サービスが停止した理由の詳細を確認します。

4. RSetup.log の内容を確認し、セットアップでエラーが発生していないことを確認します。 たとえば、メッセージ "*Exiting with code 0*" (コード0 で終了します) は、サービスの開始に失敗したことを示します。

5. 他のエラーを検索するには、rlauncher.log の内容を確認します。

## <a name="check-the-launchpad-service-account"></a>Launchpad のサービス アカウントを確認する

既定のサービス アカウントは、"NT Service\$SQL2016" や "NT Service\$SQL2017" になります。 最後の部分は、SQL インスタンス名によって異なる場合があります。

Launchpad サービス (Launchpad.exe) は、低い特権のサービス アカウントを使用して実行されます。 ただし、R と Python を起動してデータベース インスタンスと通信するには、Launchpad サービス アカウントに次のユーザー権限が必要です。

- サービスとしてログオン (SeServiceLogonRight)
- プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)
- スキャン チェックを行わない (SeChangeNotifyPrivilege)
- プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaSizePrivilege)

これらのユーザー権限の詳細については、「[Windows サービス アカウントと権限の構成](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」の「Windows の特権および権限」を参照してください。

> [!TIP]
> SQL Server 診断のための Support Diagnostics Platform (SDP) ツールの使用に慣れている場合は、SDP を使用して、MachineName_UserRights.txt という名前の出力ファイルを確認できます。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Launchpad のユーザー グループがローカルにログオンできない

Machine Learning Services のセットアップ中に、SQL Server は Windows ユーザー グループ **SQLRUserGroup** を作成し、Launchpad が SQL Server に接続して外部スクリプト ジョブを実行するために必要なすべての権限を付けてそれをプロビジョニングします。 このユーザー グループが有効になっている場合、これは Python スクリプトの実行にも使用されます。

ただし、より制限の厳しいセキュリティ ポリシーが適用されている組織では、このグループに必要な権限が手動で削除されているか、ポリシーによって自動的に失効にされている可能性があります。 権限が削除されている場合、Launchpad は SQL Server に接続できなくなり、SQL Server は外部ランタイムを呼び出せません。

問題を解決するには、グループ **SQLRUserGroup** に**ローカルのログオンを許可する**システム権限があることを確認します。

詳細については、「[Windows サービス アカウントと権限の構成](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。

## <a name="permissions-to-run-external-scripts"></a>外部スクリプトを実行する権限

Launchpad が正しく構成されていても、ユーザーに R または Python のスクリプトを実行する権限がない場合、エラーが返されます。

データベース管理者として SQL Server をインストールした場合、またはデータベース所有者である場合は、この権限が自動的に付与されます。 ただし、他のユーザーは通常、より限定された権限を持ちます。 これらのユーザーが R スクリプトを実行しようとすると、Launchpad エラーが表示されます。

この問題を解決するには、セキュリティ管理者は SQL Server Management Studio で次のスクリプトを実行して、SQL ログインまたは Windows ユーザー アカウントを変更します。

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

詳細については、「[GRANT (Transact-SQL)](../t-sql/statements/grant-transact-sql.md)」を参照してください。

## <a name="common-launchpad-errors"></a>Launchpad の一般的なエラー

このセクションでは、Launchpad が返す最も一般的なエラー メッセージを示します。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>"R スクリプトのランタイムを起動できません"

R ユーザーの Windows グループ (Python にも使用) が R Services を実行しているインスタンスにログオンできない場合は、次のエラーが表示されることがあります。

- R スクリプトを実行しようとすると生成されるエラー:

    * *'R' スクリプトのランタイムを起動できません。'R' ランタイムの構成を確認してください。*

    * *外部スクリプト エラーが発生しました。ランタイムを起動できません。*

- [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] サービスによって生成されるエラー:

    * *ランチャー RLauncher.dll を初期化できませんでした*

    * *ランチャー dll が登録されていません!*

    * *セキュリティ ログに、NT SERVICE アカウントがログインできなかったことが示される*

このユーザー グループに必要なアクセス許可を付与する方法については、[SQL Server R Services のインストール](install/sql-r-services-windows-install.md)に関する記事を参照してください。

> [!NOTE]
> SQL ログインを利用し、リモート ワークステーションから R スクリプトを実行する場合、この制限は適用されません。
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"ログオン失敗: 要求された種類のログオンは、ユーザーに許可されていません"

既定では、[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] は起動時に `NT Service\MSSQLLaunchpad` アカウントを使用します。 このアカウントは、必要なすべてのアクセス許可を持つように [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] セットアップによって構成されます。

Launchpad に別のアカウントを割り当てたか、SQL Server コンピューターのポリシーによって権限が削除された場合、アカウントが必要なアクセス許可を持たず、次のエラーが発生する可能性があります。

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Logon failure: the user has not been granted the requested logon type at this computer*

新しいサービス アカウントに必要なアクセス許可を与えるには、 ローカル セキュリティ ポリシー アプリケーションを使用し、アカウントのアクセス許可を更新して次のアクセス許可を追加します。

+ プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)
+ スキャン チェックを行わない (SeChangeNotifyPrivilege)
+ サービスとしてログオン (SeServiceLogonRight)
+ プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Launchpad サービスと通信できません"

機械学習をインストールして有効にしたが、R または Python スクリプトを実行しようとするとこのエラーが発生する場合は、インスタンスの Launchpad サービスが実行を停止した可能性があります。

1. Windows コマンド プロンプトから SQL Server 構成マネージャーを開きます。 詳細については、「 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)」を参照してください。

2. インスタンスの SQL Server Launchpad を右クリックし、 **[プロパティ]** を選択します。

3. **[サービス]** タブを選択し、サービスが実行されていることを確認します。 実行されていない場合は、 **[開始モード]** を **[自動]** に変更し、 **[適用]** を選択します。

4. 通常、サービスを再起動すると、問題が解決して、機械学習スクリプトを実行できるようになります。 再起動によって問題が解決しない場合は、 **[バイナリ パス]** プロパティのパスと引数を確認し、次の手順を実行します。

    A. ランチャーの .config ファイルを確認し、作業ディレクトリが有効であることを確認します。

    B. Launchpad によって使用される Windows グループが SQL Server インスタンスに接続できることを確認します。

    c. サービス プロパティを 1 つでも変更した場合は、Launchpad サービスを再起動します。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"致命的なエラー tmpFile の作成に失敗しました"

このシナリオでは、機械学習機能が正常にインストールされ、Launchpad が実行されています。 いくつかの単純な R または Python コードを実行しようとしても、Launchpad は次のようなエラーで失敗します。 

>*R スクリプトのランタイムと通信できませんでした。R ランタイムの要件を確認してください。*

同時に、外部スクリプト ランタイムは、STDERR メッセージの一部として次のメッセージを書き込みます。 

>*Fatal error: creation of tmpfile failed. (致命的なエラー: tmpfile の作成に失敗しました。)*

このエラーは、Launchpad が使用しようとしているアカウントに、データベースにログオンする権限がないことを示します。 この状況は、厳密なセキュリティ ポリシーが実装されている場合に発生する可能性があります。 これに該当するかどうか判断するには、SQL Server ログを確認し、ログイン時に MSSQLSERVER01 アカウントが拒否されたかどうかをチェックします。 R\_SERVICES または PYTHON\_SERVICES に固有のログにも同じ情報が記載されています。 ExtLaunchError.log を探してください。

既定では、MSSQLSERVER01 から MSSQLSERVER20 という名前で 20 個のアカウントがセットアップされ、Launchpad.exe プロセスに関連付けられます。 R または Python を頻繁に使用する場合は、アカウント数を増やすことができます。

この問題を解決するには、グループに、機械学習機能がインストールされて有効になっているローカル インスタンスに対する *[ローカル ログオンを許可する]* アクセス許可があることを確認します。 環境によっては、このアクセス許可レベルで、ネットワーク管理者からの GPO 例外が必要になる場合があります。

## <a name="not-enough-quota-to-process-this-command"></a>"このコマンドを実行するのに十分なクォータがありません"

このエラーは、次のいずれかのことを意味します。

- 外部クエリを実行する外部ユーザーが Launchpad で不足している可能性があります。 たとえば、20 個を超える外部クエリを同時に実行していて、既定の 20 ユーザーしかない場合、1 つ以上のクエリが失敗する可能性があります。

- R タスクを処理するのに十分なメモリがありません。 このエラーは、ほとんどの場合、既定の環境で、SQL Server がコンピューターのリソースの 70% まで使用している場合に発生します。 R によるリソースの使用の拡大をサポートするようにサーバー構成を変更する方法の詳細については、[R コードの運用](r/operationalizing-your-r-code.md)に関する記事を参照してください。

## <a name="cant-find-package"></a>"パッケージが見つかりません"

SQL Server で R コードを実行してこのメッセージが表示されたが、SQL Server の外部で同じコードを実行したときにはメッセージが表示されなかった場合は、SQL Server によって使用されるライブラリの既定の場所にパッケージがインストールされなかったことを意味します。

このエラーは、さまざまな方法で発生する可能性があります。

- ユーザーがサーバーに新しいパッケージをインストールしましたが、アクセスが拒否されたため、R によってユーザー ライブラリにパッケージがインストールされました。

- ユーザーが R Services をインストールした後、別の R ツールまたは一連のライブラリ (Microsoft R Server (スタンドアロン)、Microsoft R Client、RStudio など) をインストールしました。

インスタンスによって使用される R パッケージ ライブラリの場所を確認するには、SQL Server Management Studio (またはその他のデータベース クエリ ツール) を開き、インスタンスに接続して、次のストアド プロシージャを実行します。

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>サンプルの結果

*外部スクリプトからの STDOUT メッセージ:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

この問題を解決するには、パッケージを SQL Server インスタンス ライブラリに再インストールする必要があります。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>最新バージョンの Microsoft R を使用するために SQL Server 2016 のインスタンスをアップグレードした場合、既定のライブラリの場所は異なります。 詳細については、[SqlBindR を使用した R サービスのインスタンスのアップグレード](install/upgrade-r-and-python.md)に関する記事を参照してください。
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>DLL が一致しないために Launchpad がシャットダウンする

他の機能を使用してデータベース エンジンをインストールして、サーバーに修正プログラムを適用した後、元のメディアを使用して Machine Learning 機能を追加すると、正しくないバージョンの Machine Learning コンポーネントがインストールされることがあります。 Launchpad は、バージョンの不一致を検出すると、シャットダウンしてダンプ ファイルを作成します。

この問題を回避するには、必ず新機能をサーバー インスタンスと同じ修正レベルでインストールしてください。

**誤ったアップグレード方法:**

1. R Services なしで SQL Server 2016 をインストールします。
2. SQL Server 2016 Cumulative Update 2 をアップグレードします。
3. RTM メディアを使用して、R Services (データベース内) をインストールします。

**正しいアップグレード方法:**

1. R Services なしで SQL Server 2016 をインストールします。
2. 2016 SQL Server を目的の修正レベルにアップグレードします。 たとえば、Service Pack 1 をインストールしてから、Cumulative Update 2 をインストールします。
3. 適切な修正レベルで機能を追加するには、SP1 および CU2 セットアップを再度実行してから、[R Services (データベース内)] を選択します。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>8dot3 表記が必要な場合に Launchpad が起動できない

> [!NOTE] 
> 古いシステムでは、8dot3 表記の要件がある場合、Launchpad が起動できないことがあります。 この要件はその後のリリースで削除されました。 SQL Server 2016 R Services のユーザーは、次のいずれかをインストールする必要があります。
> * SQL Server 2016 SP1 と CU1:[SQL Server 用の Cumulative Update 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、Cumulative Update 3、およびオンデマンドで利用可能なこちらの[修正プログラム](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)。

R との互換性を確保するために、SQL Server 2016 R Services (データベース内) には、"*8dot3 表記*" を使用することで短いファイル名の作成をサポートする機能がインストールされているドライブが必要でした。 8\.3 ファイル名は "*短いファイル名*" とも呼ばれ、以前のバージョンの Microsoft Windows との互換性のため、または長いファイル名の代替ファイル名として使用されます。

R をインストールするボリュームが短いファイル名に対応していない場合、SQL Server から R を起動するプロセスで正しい実行可能ファイルが見つからないことがあり、Launchpad が起動しません。

回避策として、SQL Server がインストールされ、R Services がインストールされているボリュームで 8dot3 表記を有効にできます。 次に、R Services 構成ファイルに作業ディレクトリの短い名前を指定する必要があります。

1. 8dot3 表記を有効にするには、「[fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)」で説明されているように、*8dot3name* 引数を指定して fsutil ユーティリティを実行します。

2. 8dot3 表記が有効になったら、RLauncher.config ファイルを開き、`WORKING_DIRECTORY` のプロパティを確認します。 このファイルを見つける方法の詳細については、[Machine Learning のトラブルシューティングのためのデータ収集](data-collection-ml-troubleshooting-process.md)に関する記事を参照してください。

3. *file* 引数を指定した fsutil ユーティリティを使用して、WORKING_DIRECTORY に指定されているフォルダーに短いファイル パスを指定します。

4. 構成ファイルを編集して、WORKING_DIRECTORY プロパティに入力した作業ディレクトリと同じものを指定します。 あるいは、別の作業ディレクトリを指定して、8dot3 表記と互換性がある既存のパスを選択することもできます。
::: moniker-end

## <a name="next-steps"></a>次の手順

[Machine Learning Services のトラブルシューティングと既知の問題](machine-learning-troubleshooting-faq.md)

[機械学習のトラブルシューティングのためのデータ収集](data-collection-ml-troubleshooting-process.md)

[アップグレードとインストールに関してよく寄せられる質問](r/upgrade-and-installation-faq-sql-server-r-services.md)

[データベース エンジンの接続のトラブルシューティング](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
