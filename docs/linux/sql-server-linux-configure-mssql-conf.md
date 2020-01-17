---
title: Linux 上の SQL Server 設定の構成
description: この記事では、mssql-conf ツールを使用して Linux 上で SQL Server 設定を構成する方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 07/30/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 8e36eb9bccd183c8c38ebbfeafcc4ace7e025960
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783398"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>mssql-conf ツールを使用して SQL Server on Linux を構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql-conf** は、Red Hat Enterprise Linux、SUSE Linux Enterprise Server、Ubuntu 用に SQL Server 2017 と共にインストールされる構成スクリプトです。 このユーティリティを使用すると、次のパラメーターを設定できます。

|||
|---|---|
| [エージェント](#agent) | SQL Server エージェントを有効にします。 |
| [[照合順序]](#collation) | SQL Server on Linux に新しいコロケーションを設定します。 |
| [カスタマー フィードバック](#customerfeedback) | SQL Server が Microsoft にフィードバックを送信するかどうかを選択します。 |
| [[データベース メール プロファイル]](#dbmail) | SQL Server on Linux の既定のデータベース メール プロファイルを設定します。 |
| [既定のデータ ディレクトリ](#datadir) | 新しい SQL Server データベースのデータ ファイル (.mdf) の既定のディレクトリを変更します。 |
| [既定のログ ディレクトリ](#datadir) | 新しい SQL Server データベースのログ (.ldf) ファイルの既定のディレクトリを変更します。 |
| [既定のマスター データベース ディレクトリ](#masterdatabasedir) | マスター データベース ファイルとログ ファイルの既定のディレクトリを変更します。|
| [既定のマスター データベース ファイル名](#masterdatabasename) | マスター データベース ファイルの名前を変更します。 |
| [既定のダンプ ディレクトリ](#dumpdir) | 新しいメモリ ダンプおよびその他のトラブルシューティング ファイルの既定のディレクトリを変更します。 |
| [既定のエラー ログ ディレクトリ](#errorlogdir) | 新しい SQL Server エラー ログ、既定のプロファイラー トレース、システム正常性セッション XE、および Hekaton セッション XE ファイルの既定のディレクトリを変更します。 |
| [既定のバックアップ ディレクトリ](#backupdir) | 新しいバックアップ ファイルの既定のディレクトリを変更します。 |
| [ダンプの種類](#coredump) | 収集するダンプ メモリのダンプ ファイルの種類を選択します。 |
| [高可用性](#hadr) | 可用性グループを有効にします。 |
| [Local Audit ディレクトリ](#localaudit) | ディレクトリを設定して Local Audit ファイルを追加します。 |
| [ロケール](#lcid) | SQL Server で使用するロケールを設定します。 |
| [メモリの制限](#memorylimit) | SQL Server のメモリ制限を設定します。 |
| [TCP ポート](#tcpport) | SQL Server が接続をリッスンするポートを変更します。 |
| [TLS](#tls) | トランスポート層セキュリティを構成します。 |
| [トレースフラグ](#traceflags) | サービスが使用するトレースフラグを設定します。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql-conf** は、Red Hat Enterprise Linux、SUSE Linux Enterprise Server、Ubuntu 用に [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] と共にインストールされる構成スクリプトです。 このユーティリティを使用すると、次のパラメーターを設定できます。

|||
|---|---|
| [エージェント](#agent) | SQL Server エージェントを有効にします |
| [[照合順序]](#collation) | SQL Server on Linux に新しいコロケーションを設定します。 |
| [カスタマー フィードバック](#customerfeedback) | SQL Server が Microsoft にフィードバックを送信するかどうかを選択します。 |
| [[データベース メール プロファイル]](#dbmail) | SQL Server on Linux の既定のデータベース メール プロファイルを設定します。 |
| [既定のデータ ディレクトリ](#datadir) | 新しい SQL Server データベースのデータ ファイル (.mdf) の既定のディレクトリを変更します。 |
| [既定のログ ディレクトリ](#datadir) | 新しい SQL Server データベースのログ (.ldf) ファイルの既定のディレクトリを変更します。 |
| [既定のマスター データベース ファイルのディレクトリ](#masterdatabasedir) | 既存の SQL インストール上のマスター データベース ファイルの既定のディレクトリを変更します。|
| [既定のマスター データベース ファイル名](#masterdatabasename) | マスター データベース ファイルの名前を変更します。 |
| [既定のダンプ ディレクトリ](#dumpdir) | 新しいメモリ ダンプおよびその他のトラブルシューティング ファイルの既定のディレクトリを変更します。 |
| [既定のエラー ログ ディレクトリ](#errorlogdir) | 新しい SQL Server エラー ログ、既定のプロファイラー トレース、システム正常性セッション XE、および Hekaton セッション XE ファイルの既定のディレクトリを変更します。 |
| [既定のバックアップ ディレクトリ](#backupdir) | 新しいバックアップ ファイルの既定のディレクトリを変更します。 |
| [ダンプの種類](#coredump) | 収集するダンプ メモリのダンプ ファイルの種類を選択します。 |
| [高可用性](#hadr) | 可用性グループを有効にします。 |
| [Local Audit ディレクトリ](#localaudit) | ディレクトリを設定して Local Audit ファイルを追加します。 |
| [ロケール](#lcid) | SQL Server で使用するロケールを設定します。 |
| [メモリの制限](#memorylimit) | SQL Server のメモリ制限を設定します。 |
| [Microsoft 分散トランザクション コーディネーター](#msdtc) | Linux で MSDTC の構成とトラブルシューティングを行います。 |
| [MLServices の EULA](#mlservices-eula) | mlservices パッケージ用の R および Python の EULA に同意します。 これは SQL Server 2019 のみに適用されます。|
| [outboundnetworkaccess](#mlservices-outbound-access) |[mlservices](sql-server-linux-setup-machine-learning.md) R、Python、および Java 拡張機能の送信ネットワーク アクセスを有効にします。|
| [TCP ポート](#tcpport) | SQL Server が接続をリッスンするポートを変更します。 |
| [TLS](#tls) | トランスポート層セキュリティを構成します。 |
| [トレースフラグ](#traceflags) | サービスが使用するトレースフラグを設定します。 |

::: moniker-end

> [!TIP]
> これらの設定の一部は、環境変数を使って構成することもできます。 詳細については、[環境変数を使った SQL Server 設定の構成](sql-server-linux-configure-environment-variables.md)に関するページを参照してください。

## <a name="usage-tips"></a>使用上のヒント

* Always On 可用性グループと共有ディスク クラスターの場合は、常に、各ノードで同じ構成の変更を行います。

* 共有ディスク クラスターのシナリオでは、変更を適用するために **mssql サーバー** サービスを再起動しないでください。 SQL Server がアプリケーションとして実行されています。 代わりに、リソースをオフラインにしてからオンラインに戻します。

* 以下の例では、完全なパス ( **/opt/mssql/bin/mssql-conf**) を指定して mssql-conf を実行します。 代わりにそのパスに移動する場合は、現在のディレクトリのコンテキスト ( **./mssql-conf**) で mssql-conf を実行します。

## <a id="agent"></a> SQL Server エージェントを有効にする

**sqlagent.enabled** の設定では、[SQL Server エージェント](sql-server-linux-run-sql-server-agent-job.md)を有効にします。 既定では、SQL Server エージェントは無効になっています。 **sqlagent.enabled** が mssql.conf 設定ファイルに存在しない場合、SQL Server では内部的に、SQL Server エージェントが無効になっていると見なします。

この設定を変更するには、次の手順を実行します。

1. SQL Server エージェントを有効にします。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> SQL Server の照合順序を変更する

**set-collation** オプションは、照合順序の値を、サポートされている任意の照合順序に変更します。

1. 最初に、サーバー上の[すべてのユーザー データベースをバックアップ](sql-server-linux-backup-and-restore-database.md)します。

1. 次に、[sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) ストアド プロシージャを使用してユーザー データベースをデタッチします。

1. **set-collation** オプションを実行し、画面の指示に従います。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. mssql-conf ユーティリティにより、指定された照合順序の値への変更とサービスの再開が試みられます。 エラーが発生した場合は、照合順序が前の値にロールバックされます。

1. ユーザー データベースのバックアップを復元します。

サポートされている照合順序の一覧については、[sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 関数: `SELECT Name from sys.fn_helpcollations()` を実行してください。

## <a id="customerfeedback"></a> カスタマー フィードバックを構成する

**telemetry.customerfeedback** 設定により、SQL Server が Microsoft にフィードバックを送信するかどうかが変更されます。 既定では、この値はすべてのエディションで **true** に設定されます。 値を変更するには、次のコマンドを実行します。

> [!IMPORTANT]
> SQL Server、Express、Developer の無償のエディションに関するカスタマー フィードバックをオフにすることはできません。

1. **telemetry.customerfeedback** の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。 次の例では、**false** を指定することによってカスタマー フィードバックをオフにします。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

詳細については、[SQL Server on Linux に関するカスタマー フィードバック](sql-server-linux-customer-feedback.md)および [SQL Server のプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)に関するページを参照してください。

## <a id="datadir"></a> 既定のデータまたはログのディレクトリの場所を変更する

**filelocation.defaultdatadir** と **filelocation.defaultlogdir** の設定により、新しいデータベース ファイルとログ ファイルが作成される場所が変更されます。 既定では、この場所は /var/opt/mssql/data です。 これらの設定を変更するには、次の手順を実行します。

1. 新しいデータベースのデータ ファイルとログ ファイルのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/data** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/data
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. mssql-conf を使用して、**set** コマンドで既定のデータ ディレクトリを変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

1. これで、新しく作成されたデータベースのすべてのデータベース ファイルが、この新しい場所に格納されます。 新しいデータベースのログ (.ldf) ファイルの場所を変更する場合は、次の "set" コマンドを使用できます。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. このコマンドは、/tmp/log ディレクトリが存在し、ユーザーとグループ **mssql** の下にあることも前提としています。


## <a id="masterdatabasedir"></a> 既定のマスター データベース ファイルのディレクトリの場所を変更する

**filelocation.masterdatafile** と **filelocation.masterlogfile** の設定により、SQL Server エンジンがマスター データベース ファイルを検索する場所が変更されます。 既定では、この場所は /var/opt/mssql/data です。

これらの設定を変更するには、次の手順を実行します。

1. 新しいエラー ログ ファイルのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/masterdatabasedir** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. mssql-conf を使用して、**set** コマンドでマスター データ ファイルとログ ファイルの既定のマスター データベース ディレクトリを変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > マスター データ ファイルとログ ファイルを移動するだけでなく、他のすべてのシステム データベースの既定の場所も移動します。

1. SQL Server サービスを停止します。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. master.mdf と masterlog.ldf を移動します。

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. SQL Server サービスを開始します。

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > SQL Server で指定されたディレクトリに master.mdf ファイルと mastlog.ldf ファイルが見つからない場合は、指定されたディレクトリにシステム データベースのテンプレート化されたコピーが自動的に作成され、SQL Server が正常に起動します。 ただし、ユーザー データベース、サーバー ログイン、サーバー証明書、暗号化キー、SQL エージェント ジョブ、古い SA ログイン パスワードなどのメタデータは、新しいマスター データベースでは更新されません。 引き続き既存のメタデータを使用するには、SQL Server を停止して、古い master.mdf と mastlog.ldf を指定した新しい場所に移動し、SQL Server を起動する必要があります。
 
## <a id="masterdatabasename"></a> マスター データベース ファイルの名前を変更する

**filelocation.masterdatafile** と **filelocation.masterlogfile** の設定により、SQL Server エンジンがマスター データベース ファイルを検索する場所が変更されます。 これを使用して、マスター データベース ファイルとログ ファイルの名前を変更することもできます。 

これらの設定を変更するには、次の手順を実行します。

1. SQL Server サービスを停止します。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. mssql-conf を使用して、**set** コマンドでマスター データ ファイルとログ ファイルのマスター データベースの想定される名前を変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > マスター データベース ファイルとログ ファイルの名前は、SQL Server が正常に起動された後でのみ変更できます。 SQL Server では、最初の実行まではファイルの名前が master.mdf と mastlog.ldf であると想定されます。

1. マスター データベース ファイルとログ ファイルの名前を変更する 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. SQL Server サービスを開始します。

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> 既定のダンプ ディレクトリの場所を変更する

**filelocation.defaultdumpdir** の設定により、クラッシュが発生するたびにメモリと SQL ダンプが生成される既定の場所が変更されます。 既定では、これらのファイルは /var/opt/mssql/log 内に生成されます。

この新しい場所を設定するには、次のコマンドを使用します。

1. 新しいダンプ ファイルのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/dump** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/dump
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. mssql-conf を使用して、**set** コマンドで既定のデータ ディレクトリを変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 既定のエラー ログ ファイルのディレクトリの場所を変更する

**filelocation.errorlogfile** の設定により、新しいエラー ログ、既定のプロファイラー トレース、システム正常性セッション XE ファイルと、および Hekaton セッション XE ファイルが作成される場所が変更されます。 既定では、この場所は /var/opt/mssql/log です。 SQL エラー ログ ファイルが設定されているディレクトリが、他のログの既定のログ ディレクトリになります。

これらの設定を変更するには、次の操作を行います。

1. 新しいエラー ログ ファイルのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/logs** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/logs
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. mssql-conf を使用して、**set** コマンドで既定のエラー ログ ファイル名を変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 既定のバックアップ ディレクトリの場所を変更する

**filelocation.defaultbackupdir** の設定により、バックアップ ファイルが生成される既定の場所が変更されます。 既定では、これらのファイルは /var/opt/mssql/data に生成されます。

この新しい場所を設定するには、次のコマンドを使用します。

1. 新しいバックアップ ファイルのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/backup** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/backup
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. mssql-conf を使用して、"set" コマンドで既定のバックアップ ディレクトリを変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> コア ダンプ設定を指定する

SQL Server のいずれかのプロセスで例外が発生した場合、SQL Server によってメモリ ダンプが作成されます。

SQL Server によって収集されるメモリ ダンプの種類を制御するための 2 つのオプション (**coredump.coredumptype** と **coredump.captureminiandfull**) があります。 これらは、コア ダンプ キャプチャの 2 つのフェーズに関連しています。 

最初のフェーズのキャプチャは、例外の発生時に生成されるダンプ ファイルの種類を決定する **coredump.coredumptype** 設定によって制御されます。 2 番目のフェーズは、**coredump.captureminiandfull** の設定時に有効になります。 **coredump.captureminiandfull** が true に設定されている場合は、**coredump.coredumptype** によって指定されたダンプ ファイルが生成され、2 番目のミニ ダンプも生成されます。 **coredump.captureminiandfull** を false に設定すると、2 回目のキャプチャの試行が無効になります。

1. **coredump.captureminiandfull** の設定を使用して、ミニ ダンプと完全ダンプを両方ともキャプチャするかどうかを決定します。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    既定値: **false**

1. **coredump.coredumptype** の設定を使用して、ダンプ ファイルの種類を指定します。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    既定値: **miniplus**

    指定できる **coredump.coredumptype** の値の一覧を次の表に示します。

    | 型 | [説明] |
    |-----|-----|
    | **mini** | mini は、最も小さいダンプ ファイルの種類です。 これは、Linux システム情報を使用して、プロセス内のスレッドとモジュールを特定します。 ダンプには、ホスト環境のスレッド スタックとモジュールのみが含まれます。 間接的なメモリ参照またはグローバルは含まれません。 |
    | **miniplus** | miniplus は mini に似ていますが、追加のメモリが含まれています。 これは、SQLPAL とホスト環境の内部構造を認識して、次のメモリ領域をダンプに追加します。</br></br> - さまざまなグローバル</br> - 64 TB を超えるすべてのメモリ</br> - **/proc/$pid/maps** で見つかったすべての名前付きリージョン</br> - スレッドとスタックからの間接メモリ</br> - スレッド情報</br> - 関連付けられている Teb と Peb</br> - モジュール情報</br> - VMM および VAD ツリー |
    | **filtered** | filtered では、明示的に除外しない限りプロセス内のすべてのメモリが含まれる、減算ベースの設計を使用します。 この設計では、特定のリージョンをダンプから除外して、SQLPAL とホスト環境の内部構造を認識します。
    | **full** | full は、 **/proc/$pid/maps** にあるすべてのリージョンを含む完全なプロセス ダンプです。 これは **coredump.captureminiandfull** の設定によって制御されません。 |

## <a id="dbmail"></a> SQL Server on Linux の既定のデータベース メール プロファイルを設定する

**sqlpagent.databasemailprofile** を使用すると、メール アラートの既定の DB メール プロファイルを設定できます。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 高可用性

**hadr.hadrenabled** オプションは、SQL Server インスタンスで可用性グループを有効にします。 次のコマンドは、**hadr.hadrenabled** を 1 に設定することで可用性グループを有効にします。 設定を有効にするには、SQL Server を再起動する必要があります。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

可用性グループでの使用方法については、次の 2 つのトピックを参照してください。

- [SQL Server on Linux の Always On 可用性グループを構成する](sql-server-linux-availability-group-configure-ha.md)
- [SQL Server on Linux の読み取りスケール可用性グループを構成する](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> ローカル監査ディレクトリを設定する

**telemetry.userrequestedlocalauditdirectory** の設定により、Local Audit が有効になり、Local Audit ログが作成されるディレクトリを設定できます。

1. 新しい Local Audit ログのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/audit** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/audit
   ```

1. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. **telemetry.userrequestedlocalauditdirectory** の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

詳細については、[SQL Server on Linux に関するカスタマー フィードバック](sql-server-linux-customer-feedback.md)に関するページを参照してください。

## <a id="lcid"></a> SQL Server のロケールを変更する

**language.lcid** の設定により、SQL Server のロケールが、サポートされている言語識別子 (LCID) に変更されます。 

1. 次の例では、ロケールをフランス語 (1036) に変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. SQL Server サービスを再起動して、変更を適用します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> メモリ制限を設定する

**memory.memorylimitmb** の設定により、SQL Server で使用できる物理メモリの量 (MB 単位) を制御します。 既定値は、物理メモリの 80% です。

1. **memory.memorylimitmb** の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。 次の例では、SQL Server で使用可能なメモリを 3.25 GB (3328 MB) に変更します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. SQL Server サービスを再起動して、変更を適用します。

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> MSDTC を構成する

Microsoft 分散トランザクション コーディネーター (MSDTC) を構成するには、**network.rpcport** および **distributedtransaction.servertcpport** の設定を使用します。 これらの設定を変更するには、次のコマンドを実行します。

1. "network.rpcport" の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. 次に、"distributedtransaction.servertcpport" の設定を設定します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

これらの値を設定するだけでなく、ルーティングを構成し、ポート 135 のファイアウォールを更新する必要があります。 これを行う方法の詳細については、[Linux で MSDTC を構成する方法](sql-server-linux-configure-msdtc.md)に関するページを参照してください。

mssql-conf には、MSDTC の監視とトラブルシューティングに使用できるその他のいくつかの設定があります。 次の表では、これらの設定について簡単に説明しています。 使用方法の詳細については、[MS DTC の診断トレースを有効にする方法](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute)に関する Windows サポートの記事を参照してください。

| mssql-conf setting | [説明] |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | 分散トランザクションに対して、セキュリティで保護された RPC のみを構成します |
| distributedtransaction.fallbacktounsecurerpcifnecessary | 分散トランザクションに対して、セキュリティ専用の RPC 呼び出しを構成します |
| distributedtransaction.maxlogsize | DTC トランザクション ログ ファイル サイズ (MB)。 既定値は 64 MB です |
| distributedtransaction.memorybuffersize | トレースが格納される循環バッファーのサイズ。 このサイズは MB 単位で、既定値は 10 MB です |
| distributedtransaction.servertcpport | MSDTC rpc サーバーのポート |
| distributedtransaction.trace_cm | 接続マネージャーでのトレース |
| distributedtransaction.trace_contact | 連絡先プールと連絡先をトレースします |
| distributedtransaction.trace_gateway | ゲートウェイのソースをトレースします |
| distributedtransaction.trace_log | ログのトレース |
| distributedtransaction.trace_misc | 他のカテゴリに分類できないトレース |
| distributedtransaction.trace_proxy | MSDTC プロキシで生成されるトレース |
| distributedtransaction.trace_svc | サービスと .exe ファイルのスタートアップをトレースします |
| distributedtransaction.trace_trace | トレース インフラストラクチャ自体 |
| distributedtransaction.trace_util | 複数の場所から呼び出されるユーティリティ ルーチンをトレースします |
| distributedtransaction.trace_xa | XA トランザクション マネージャー (XATM) のトレースのソース |
| distributedtransaction.tracefilepath | トレース ファイルを格納するフォルダー |
| distributedtransaction.turnoffrpcsecurity | 分散トランザクションの RPC セキュリティを有効または無効にします |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> MLServices の EULA に同意する

[Machine Learning R または Python パッケージ](sql-server-linux-setup-machine-learning.md)をデータベース エンジンに追加するには、R および Python のオープンソース ディストリビューションのライセンス条項に同意する必要があります。 次の表に、mlservices の EULA に関連するすべての使用可能なコマンドまたはオプションを列挙します。 インストールされている内容によっては、R と Python で同じ EULA パラメーターが使用されます。

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

[mssql.conf ファイル](#mssql-conf-format)に EULA の同意を直接追加することもできます。

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> 送信ネットワーク アクセスを有効にする

[SQL Server Machine Learning Services](sql-server-linux-setup-machine-learning.md) 機能の R、Python、および Java 拡張機能の送信ネットワーク アクセスは、既定では無効になっています。 送信要求を有効にするには、mssql-conf を使用して "outboundnetworkaccess" ブール型プロパティを設定します。

プロパティの設定後、SQL Server Launchpad サービスを再起動して、INI ファイルから更新後の値を読み込みます。 拡張機能に関連する設定が変更されるたびに、再起動のメッセージが表示されます。

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

[mssql.conf ファイル](#mssql-conf-format)に "outboundnetworkaccess" を直接追加することもできます。

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> TCP ポートを変更する

**network.tcpport** 設定は、SQL Server が接続をリッスンする TCP ポートを変更します。 既定では、このポート番号は 1433 に設定されています。 ポートを変更するには、次のコマンドを実行します。

1. "network.tcpport" の "set" コマンドを使用して、mssql-conf スクリプトを root として実行します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

3. この時点で SQL Server に接続する場合は、ホスト名または IP アドレスの後にコンマ (,) を付けてカスタム ポートを指定する必要があります。 たとえば、SQLCMD を使用して接続するには、次のコマンドを使用します。

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> TLS 設定を指定する

次のオプションでは、Linux で実行されている SQL Server のインスタンスに対して TLS を構成します。

|オプション |[説明] |
|--- |--- |
|**network.forceencryption** |1 の場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はすべての接続を強制的に暗号化します。 既定では、このオプションは 0 になっています。 |
|**network.tlscert** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が TLS に使用する証明書ファイルへの絶対パス。 例: `/etc/ssl/certs/mssql.pem` 証明書ファイルには、mssql アカウントがアクセスできる必要があります。 Microsoft では、`chown mssql:mssql <file>; chmod 400 <file>` を使用してファイルへのアクセスを制限することをお勧めします。 |
|**network.tlskey** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が TLS に使用する秘密キーへの絶対パス。 例:`/etc/ssl/private/mssql.key` 証明書ファイルには、mssql アカウントがアクセスできる必要があります。 Microsoft では、`chown mssql:mssql <file>; chmod 400 <file>` を使用してファイルへのアクセスを制限することをお勧めします。 |
|**network.tlsprotocols** |SQL Server によって許可される TLS プロトコルのコンマ区切りのリスト。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、許可されている最も強いプロトコルのネゴシエートを常に試行します。 クライアントが許可されているプロトコルをサポートしていない場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は接続試行を拒否します。  互換性のために、サポートされているすべてのプロトコルが既定で許可されています (1.2、1.1、1.0)。  クライアントが TLS 1.2 をサポートしている場合、Microsoft では TLS 1.2 のみを許可することをお勧めします。 |
|**network.tlsciphers** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が TLS に対して許可する暗号を指定します。 この文字列は、[OpenSSL の暗号リスト形式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)に従った形式にする必要があります。 一般に、このオプションを変更する必要はありません。 <br /> 既定では、次の暗号が許可されます。 <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab ファイルへのパス |

TLS 設定の使用例については、[SQL Server on Linux への接続の暗号化](sql-server-linux-encrypted-connections.md)に関するページを参照してください。

## <a id="traceflags"></a> トレースフラグを有効/無効にする

この **traceflag** オプションは、SQL Server サービスを起動するためのトレースフラグを有効または無効にします。 トレースフラグを有効または無効にするには、次のコマンドを使用します。

1. 次のコマンドを使用してトレースフラグを有効にします。 たとえば、トレースフラグ 1234 の場合は次のようになります。

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 複数のトレースフラグは個別に指定することで有効にすることができます。

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 同様の方法で、1 つ以上の有効なトレースフラグは、それらを指定して **off** パラメーターを追加することによって無効にすることができます。

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. SQL Server サービスを再起動して、変更を適用します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>設定を削除する

`mssql-conf set` で行われた設定を設定解除するには、`unset` オプションと設定の名前を指定して **mssql-conf** を呼び出します。 これにより設定がクリアされ、実質的に既定値に戻ります。

1. 次の例では、**network.tcpport** オプションをクリアします。

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>現在の設定を表示する

構成されている設定を表示するには、次のコマンドを実行して **mssql.conf** ファイルの内容を出力します。

```bash
sudo cat /var/opt/mssql/mssql.conf
```

このファイルに示されていない設定では、既定値が使用されていることに注意してください。 次のセクションで、**mssql.conf** ファイルのサンプルを示します。


## <a id="mssql-conf-format"></a> mssql.conf format

次の **/var/opt/mssql/mssql.conf** ファイルは、各設定の例を示しています。 この形式を使用すると、必要に応じて **mssql.conf** ファイルに手動で変更を加えることができます。 ファイルを手動で変更する場合は、変更を適用する前に SQL Server を再起動する必要があります。 Docker で **mssql** ファイルを使用するには、Docker が[データを保持](sql-server-linux-configure-docker.md)している必要があります。 まず、完全な **mssql.conf** ファイルをホスト ディレクトリに追加してから、コンテナーを実行します。 この例は[カスタマー フィードバック](sql-server-linux-customer-feedback.md)に含まれています。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>次の手順

代わりに環境変数を使用してこれらの構成の変更を行う場合は、[環境変数を使用した SQL Server 設定の構成](sql-server-linux-configure-environment-variables.md)に関するページを参照してください。

その他の管理ツールとシナリオについては、[SQL Server on Linux の管理](sql-server-linux-management-overview.md)に関するページを参照してください。
