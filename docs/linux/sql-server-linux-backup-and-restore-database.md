---
title: Linux での SQL Server データベースのバックアップと復元
description: Linux で SQL Server データベースをバックアップおよび復元する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 88ef620a24bc2ce623ea6fb072871dadeffbcf6d
ms.sourcegitcommit: 2604e13627fbc9f3bda3926b67045fceb7b04e37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68823116"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Linux での SQL Server データベースのバックアップと復元

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

さまざまなオプションを使用して、Linux 上の SQL Server 2017 からデータベースのバックアップを作成できます。 Linux サーバーでは、**sqlcmd** を使用して SQL Server に接続してバックアップを作成できます。 Windows からは、SQL Server on Linux に接続して、ユーザー インターフェイスを使用してバックアップを作成できます。 バックアップ機能はプラットフォーム間で同じです。 たとえば、データベースのローカル バックアップ、リモート ドライブへのバックアップ、または [Microsoft Azure Blob ストレージ サービス](../relational-databases/backup-restore/sql-server-backup-to-url.md)へのバックアップを行うことができます。

## <a name="backup-a-database"></a>データベースをバックアップする

次の例では、**sqlcmd** がローカル SQL Server インスタンスに接続し、`demodb` というユーザー データベースの完全バックアップを作成します。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

コマンドを実行すると、SQL Server によってパスワードの入力が求められます。 パスワードを入力すると、バックアップの進行状況の結果がシェルから返されます。 例:

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>トランザクション ログをバックアップする

データベースが完全復旧モデルの場合は、さらに詳細な復元オプションのためにトランザクション ログ バックアップを作成することもできます。 次の例では、**sqlcmd** がローカル SQL Server インスタンスに接続し、トランザクション ログ バックアップを作成します。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>データベースを復元する

次の例では、**sqlcmd** が SQL Server のローカル インスタンスに接続し、demodb データベースを復元します。 ログ ファイル バックアップを追加で復元できるように `NORECOVERY` オプションを使用することに注意してください。 追加のログ ファイルを復元する予定がない場合は、`NORECOVERY` オプションを削除します。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 誤って NORECOVERY を使用したが、追加のログ ファイル バックアップがない場合は、パラメーターを付けずにコマンド `RESTORE DATABASE demodb` を実行します。 これによって復元が完了し、データベースは稼働したままになります。

### <a name="restore-the-transaction-log"></a>トランザクション ログを復元する

次のコマンドによって、前のトランザクション ログ バックアップが復元されます。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用してバックアップおよび復元する

Windows コンピューターの SSMS を使用して、Linux データベースに接続し、ユーザー インターフェイスでバックアップを作成します。

>[!NOTE] 
> 最新バージョンの SSMS を使用して SQL Server に接続します。 最新バージョンをダウンロードしてインストールする方法については、[SSMS のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)に関するページを参照してください。 SSMS の使用方法について詳しくは、「[SSMS を使用して SQL Server on Linux を管理する](sql-server-linux-manage-ssms.md)」を参照してください。

次の手順では、SSMS を使用したバックアップの作成方法を説明します。 

1. SSMS を起動し、SQL Server 2017 on Linux 内のサーバーに接続します。

1. オブジェクト エクスプローラーで、データベースを右クリックし、 **[タスク]** 、 **[バックアップ...]** の順にクリックします。

1. **[Backup Up Database]\(データベースのバックアップ\)** ダイアログで、パラメーターとオプションを確認し、 **[OK]** をクリックします。
 
SQL Server によってデータベースのバックアップが完了されます。

### <a name="restore-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用して復元する 

次の手順では、SSMS を使用してデータベースを復元する方法について説明します。

1. SSMS で **[データベース]** を右クリックし、 **[データベースの復元...]** をクリックします。 

1. **[ソース]** の下の **[デバイス:]** をクリックし、省略記号 (...) をクリックします。

1. データベース バックアップ ファイルを見つけたら、 **[OK]** をクリックします。 

1. **[復元プラン]** の下で、バックアップ ファイルと設定を確認します。 **[OK]** をクリックします。 

1. SQL Server によってデータベースが復元されます。 

## <a name="see-also"></a>参照

* [データベースの完全バックアップの作成 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [トランザクション ログのバックアップ (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
