---
title: SQL Server on Linux のトラブルシューティング
description: SQL Server on Linux の使用に関するトラブルシューティングのヒントについて説明します。
author: VanMSFT
ms.author: vanto
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 6ff5c1c5944e1313d6c95cd35be288ad4d2154c8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032209"
---
# <a name="troubleshoot-sql-server-on-linux"></a>SQL Server on Linux のトラブルシューティング

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このドキュメントでは、Linux 上または Docker コンテナー内で実行される Microsoft SQL Server のトラブルシューティングを行う方法について説明します。 SQL Server on Linux のトラブルシューティングを行う場合は、 [SQL Server on Linux のリリース ノート](sql-server-linux-release-notes.md)で、サポートされている機能と既知の制限事項を必ず確認してください。

> [!TIP]
> よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。

## <a id="connection"></a> 接続エラーのトラブルシューティング
Linux SQL Server に接続するのが困難な場合は、いくつかの点を確認する必要があります。

- **localhost** を使ってローカルに接続できない場合は、代わりに IP アドレス 127.0.0.1 を使ってみてください。 **localhost** がこのアドレスに適切にマップされていない可能性があります。

- クライアント コンピューターからサーバー名または IP アドレスに到達できることを確認します。

   > [!TIP]
   > Ubuntu コンピューターの IP アドレスを確認するには、次の例のように ifconfig コマンドを実行します。
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Red Hat では、次の例のように ip addr を使用できます。
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > この手法の 1 つの例外は、Azure VM に関するものです。 Azure VM の場合は、[Azure portal で VM のパブリック IP アドレスを検索](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)します。

- 該当する場合は、ファイアウォールで SQL Server ポート (既定値は 1433) が開かれていることを確認します。

- Azure VM の場合は、[既定の SQL Server ポートに対するネットワーク セキュリティ グループ規則](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)があることを確認します。

- ユーザー名とパスワードで、入力ミス、余分なスペース、または大文字と小文字の間違いがないことを確認します。

- 次の例のように、サーバー名と共にプロトコルとポート番号を明示的に設定してみます: **tcp:servername,1433**。

- ネットワーク接続の問題により、接続エラーとタイムアウトが発生することもあります。 接続情報とネットワーク接続を確認してから、再度接続してみます。

## <a name="manage-the-sql-server-service"></a>SQL Server サービスを管理する

次のセクションでは、SQL Server サービスの開始、停止、再起動、および状態の確認を行う方法について説明します。 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Red Hat Enterprise Linux (RHEL) と Ubuntu で mssql-server サービスを管理する 

次のコマンドを使って、SQL Server サービスの状態を確認します。

   ```bash
   sudo systemctl status mssql-server
   ```

必要に応じて、次のコマンドを使って、SQL Server サービスを停止、開始、または再起動することができます。

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>mssql Docker コンテナーの実行を管理する

次のコマンドを実行して、作成された最新の SQL Server Docker コンテナーの状態とコンテナー ID を取得できます (ID は **[CONTAINER ID]** 列にあります)。

   ```bash
   sudo docker ps -l
   ```
   
必要に応じて、次のコマンドを使って、SQL Server サービスを停止または再起動することができます。
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Docker のトラブルシューティングのヒントについては、[SQL Server Docker コンテナーのトラブルシューティング](sql-server-linux-configure-docker.md#troubleshooting)に関する記事を参照してください。

## <a name="access-the-log-files"></a>ログ ファイルにアクセスする
   
Linux と Docker の両方のインストールにおいて、SQL Server エンジンでは /var/opt/mssql/log/errorlog ファイルにログが記録されます。 このディレクトリを参照するには、"スーパーユーザー" モードである必要があります。

インストーラーのログは次の場所にあります: /var/opt/mssql/setup-<インストール時刻を表すタイムスタンプ>。次のように、"vim" や "cat" などの UTF-16 互換ツールを使って、errorlog ファイルを参照できます。 

   ```bash
   sudo cat errorlog
   ```

好みに応じて、次のコマンドでファイルを UTF-8 に変換して、"more" または "less" で読み取ることもできます。
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>拡張イベント

拡張イベントのクエリは、SQL コマンドを使用して実行できます。  拡張イベントの詳細については、[こちら](https://technet.microsoft.com/library/bb630282.aspx)を参照してください。

## <a name="crash-dumps"></a>クラッシュ ダンプ 

Linux のログ ディレクトリでダンプを探します。 /var/opt/mssql/log ディレクトリで、Linux コア ダンプ (.tar.gz2 拡張子) または SQL ミニダンプ (.mdmp 拡張子) を調べます

コア ダンプの場合 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

SQL ダンプの場合 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>最小構成またはングル ユーザー モードで SQL Server を起動する

### <a name="start-sql-server-in-minimal-configuration-mode"></a>最小構成モードで SQL Server を起動する
設定値によりサーバーが起動できないとき (たとえば使用できるメモリが不足している場合) などに便利です。
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>シングル ユーザー モードで SQL Server を起動する
特定の状況では、startup option -m を使って、SQL Server のインスタンスをシングル ユーザー モードで起動することが必要になる場合があります。 たとえば、サーバーの構成オプションを変更したり、破損した master データベースや他のシステム データベースを復旧したりすることがあります。 たとえば、サーバーの構成オプションを変更したり、破損した master データベースや他のシステム データベースを復旧したりすることがあります   

シングル ユーザー モードで SQL Server を起動する
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

SQLCMD を使用してシングル ユーザー モードで SQL Server を起動する
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  スタートアップに関する将来の問題を防ぐため、Linux 上の SQL Server は "mssql" ユーザーで起動してください。 たとえば、"sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]" などとします。 

誤って別のユーザーで SQL Server を起動した場合は、systemd を使用して SQL Server を起動する前に、SQL Server データベース ファイルの所有権を "mssql" ユーザーに変更する必要があります。 たとえば、/var/opt/mssql の下にあるすべてのデータベース ファイルの所有権を "mssql" ユーザーに変更するには、次のコマンドを実行します

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>システム データベースを再構築する
最後の手段として、master および model データベースを既定のバージョンに再構築することもできます。

> [!WARNING]
> 次の手順を実行すると、構成した**すべての SQL Server システム データが削除**されます。 これには、ユーザー データベースに関する情報が含まれます (ただし、ユーザー データベース自体は含まれません)。 また、システム データベースに格納されている他の情報も削除されます。これには、マスター キー情報、master に読み込まれたすべての証明書、SA ログイン パスワード、msdb からのジョブ関連情報、msdb からの DB メール情報、および sp_configure オプションが含まれます。 影響を理解している場合にのみ使用してください。

1. SQL Server を停止します。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. **force-setup** パラメーターを指定して **sqlservr** を実行します。 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 前の警告を参照してください。 また、次に示すように、これを **mssql** ユーザーとして実行する必要があります。

1. "復旧が完了した" というメッセージが表示されたら、Ctrl + C キーを押します。 これにより、SQL Server がシャットダウンされます

1. SA パスワードを再構成します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. SQL Server を起動し、サーバーを再構成します。 これには、すべてのユーザー データベースの復元または再アタッチが含まれます。

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>パフォーマンスを向上させる

データベースの設計、ハードウェア、ワークロードの要求など、パフォーマンスに影響を与える要因は多数あります。 パフォーマンスを向上させる場合は、最初に記事「[パフォーマンスのベスト プラクティスと SQL Server on Linux の構成ガイドライン](sql-server-linux-performance-best-practices.md)」のベスト プラクティスを確認してください。 次に、パフォーマンスの問題のトラブルシューティングに使用できるツールを調べます。

- [クエリ ストア](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [システム動的管理ビュー (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [SQL Server Management Studio のパフォーマンス ダッシュボード](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>一般的な問題

1. リモート SQL Server インスタンスに接続できません。

   「[接続エラーのトラブルシューティング](#connection)」セクションの説明を参照してください。

2. エラー: ホスト名は 15 文字以下にする必要があります。

   これは既知の問題であり、SQL Server Debian パッケージをインストールしようとしているコンピューターの名前が 15 文字を超えている場合に発生します。 現在、コンピューターの名前を変更する以外に、回避策はありません。 これを行う 1 つの方法は、ホスト名ファイルを編集し、コンピューターを再起動することです。 詳しくは、次の [Web サイトのガイド](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)を参照してください。

3. システム管理 (SA) パスワードのリセット。

   システム管理者 (SA) のパスワードを忘れた場合、または何らかの理由でそれをリセットする必要がある場合は、次の手順のようにします。

   > [!NOTE]
   > 次の手順では、SQL Server サービスを一時的に停止します。

   ホスト ターミナルにログインして、次のコマンドを実行し、画面の指示に従って SA パスワードをリセットします。

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. パスワードでの特殊文字の使用。

   一部の文字は、SQL Server のログイン パスワードで使った場合、ターミナルの Linux コマンドで使うときに、円記号によるエスケープが必要になる場合があります。 たとえば、ドル記号 ($) は、ターミナル コマンド/シェル スクリプトで使うときは常に、エスケープする必要があります。

   次の場合は動作しません。

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   次の場合は動作します。

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   リソース: [特殊文字](https://tldp.org/LDP/abs/html/special-chars.html)
   [エスケープ](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
