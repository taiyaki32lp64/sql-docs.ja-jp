---
title: Docker で SQL Server データベースを復元する
description: このチュートリアルでは、新しい Linux の Docker コンテナーで SQL Server データベースのバックアップを復元する方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 2b34fb6b368f042e39776a25628472c336e21392
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75721827"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Linux の Docker コンテナーで SQL Server データベースを復元する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

このチュートリアルでは、Docker 上で実行している SQL Server 2017 の Linux コンテナー イメージに SQL Server のバックアップ ファイルを移動して、復元する方法について説明します。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

このチュートリアルでは、Docker 上で実行している SQL Server 2019 の Linux コンテナー イメージに SQL Server のバックアップ ファイルを移動して、復元する方法について説明します。

::: moniker-end

> [!div class="checklist"]
> * 最新の SQL Server Linux コンテナー イメージをプルして実行する。
> * Wide World Importers のデータベース ファイルをコンテナーにコピーする。
> * コンテナーにデータベースを復元する。
> * Transact-SQL ステートメントを実行してデータベースの表示と変更を行う。
> * 変更したデータベースをバックアップする。

## <a name="prerequisites"></a>前提条件

* サポートされているいずれかの Linux ディストリビューションの Docker エンジン 1.8+ または Mac/Windows 用 Docker。 詳細については、「[Install Docker](https://docs.docker.com/engine/installation/)」(Docker をインストールする) を参照してください。
* 2 GB 以上のディスク領域
* 2 GB 以上の RAM
* [SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>コンテナー イメージのプルと実行

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Linux/Mac 上で bash ターミナルを開くか、Windows 上で管理者特権の PowerShell セッションを開きます。

1. Docker Hub から SQL Server 2017 Linux コンテナー イメージをプルします。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > このチュートリアル全体で、docker コマンドの例は bash シェル (Linux/Mac) と PowerShell (Windows) の両方に対して提供されます。

1. Docker を使ってコンテナー イメージを実行するには、次のコマンドを使います。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   このコマンドにより、Developer エディションの SQL Server 2017 コンテナー (規定値) が作成されます。 SQL Server のポート **1433** は、ホスト上ではポート **1401** として公開されています。 省略可能な `-v sql1data:/var/opt/mssql` パラメーターを使うと、**sql1ddata** という名前のデータ ボリューム コンテナーが作成されます。 これは、SQL Server によって作成されたデータを永続化するために使われます。

   > [!IMPORTANT]
   > この例では、Docker 内のデータ ボリューム コンテナーが使用されます。 ホスト ディレクトリのマッピングを代わりに選択する場合、Mac と Windows では、Docker でのこの手法に制限があることにご留意ください。 詳細については、「[Docker で SQL Server コンテナーイメージを構成する](sql-server-linux-configure-docker.md#persist)」を参照してください。

1. Docker コンテナーを表示するには、`docker ps` コマンドを使用します。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. **[STATUS]** 列に **[Up]** の状態が表示されている場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列に指定されたポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合は、[構成ガイドのトラブルシューティングのセクション](sql-server-linux-configure-docker.md#troubleshooting)を参照してください。

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Linux/Mac 上で bash ターミナルを開くか、Windows 上で管理者特権の PowerShell セッションを開きます。

1. Docker Hub から SQL Server 2019 Linux コンテナー イメージをプルします。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   > [!TIP]
   > このチュートリアル全体で、docker コマンドの例は bash シェル (Linux/Mac) と PowerShell (Windows) の両方に対して提供されます。

1. Docker を使ってコンテナー イメージを実行するには、次のコマンドを使います。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   このコマンドにより、Developer エディションの SQL Server 2019 コンテナー (規定値) が作成されます。 SQL Server のポート **1433** は、ホスト上ではポート **1401** として公開されています。 省略可能な `-v sql1data:/var/opt/mssql` パラメーターを使うと、**sql1ddata** という名前のデータ ボリューム コンテナーが作成されます。 これは、SQL Server によって作成されたデータを永続化するために使われます。

1. Docker コンテナーを表示するには、`docker ps` コマンドを使用します。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. **[STATUS]** 列に **[Up]** の状態が表示されている場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列に指定されたポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合は、[構成ガイドのトラブルシューティングのセクション](sql-server-linux-configure-docker.md#troubleshooting)を参照してください。

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>SA パスワードの変更

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>バックアップ ファイルをコンテナーにコピーする

このチュートリアルでは、[Wide World Importers のサンプル データベース](../sample/world-wide-importers/wide-world-importers-documentation.md)を使います。 以下の手順に従って、Wide World Importers のデータベース バックアップ ファイルをダウンロードし、お使いの SQL Server コンテナーにコピーします。

1. まず、**docker exec** を使ってバックアップ フォルダーを作成します。 次のコマンドを実行すると、SQL Server コンテナー内に **/var/opt/mssql/backup** ディレクトリが作成されます。

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 次に、ホスト コンピューターに [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) ファイルをダウンロードします。 次のコマンドでは、home/user ディレクトリに移動し、バックアップ ファイルを **wwi.bak** としてダウンロードします。

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. **docker cp** を使って、 **/var/opt/mssql/backup** ディレクトリ内のコンテナーにバックアップ ファイルをコピーします。

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>データベースを復元する

これで、コンテナー内にバックアップ ファイルが配置されました。 バックアップを復元する前に、バックアップ内の論理ファイル名とファイルの種類を把握しておくことが重要です。 以下の Transact-SQL コマンドでは、バックアップを検査し、コンテナーで **sqlcmd** を使って復元を実行します。

> [!TIP]
> コンテナーには **sqlcmd** が事前にインストールされているため、このチュートリアルではコンテナー内でこのツールを使います。 ただし、[Visual Studio Code](sql-server-linux-develop-use-vscode.md) や [SQL Server Management Studio](sql-server-linux-manage-ssms.md) など、コンテナーの外部にある他のクライアント ツールを使って Transact-SQL ステートメントを実行することもできます。 接続するには、コンテナーのポート 1433 にマップされたホストのポートを使います。 この例では、ホスト コンピューター上の **localhost,1401** とリモートの **Host_IP_Address,1401** が該当します。

1. コンテナー内で **sqlcmd** を実行し、バックアップ内の論理ファイル名とパスを一覧表示します。 これを行うには、Transact-SQL ステートメントの **RESTORE FILELISTONLY** を使います。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   次のような出力が表示されます。

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. **RESTORE DATABASE** コマンドを呼び出し、コンテナー内でデータベースを復元します。 前の手順のファイルごとに、新しいパスを指定します。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   次のような出力が表示されます。

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>復元されたデータベースを確認する

次のクエリを実行して、コンテナー内のデータベース名の一覧を表示します。

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

データベースの一覧に **WideWorldImporters** が含まれているはずです。

## <a name="make-a-change"></a>変更を加える

以下の手順では、データベースに変更を加えます。

1. クエリを実行して、**Warehouse.StockItems** テーブルの上位 10 項目を表示します。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   項目の識別子と名前の一覧が表示されます。

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. 次の **UPDATE** ステートメントを使用して、最初の項目の説明を更新します。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   次のテキストのような出力が表示されます。

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>新しいバックアップの作成

コンテナー内にデータベースを復元した後は、実行しているコンテナー内にデータベースのバックアップを定期的に作成することもできます。 その手順は以前の手順のパターンと似ていますが、向きが逆になります。

1. Transact-SQL コマンド **BACKUP DATABASE** を使って、コンテナー内にデータベースのバックアップを作成します。 このチュートリアルでは、以前に作成した **/var/opt/mssql/backup** ディレクトリに、新しいバックアップ ファイル **wwi_2.bak** を作成します。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   次のような出力が表示されます。

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. 次に、そのバックアップ ファイルを、コンテナーからホスト コンピューター上にコピーします。

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>永続化されたデータの使用

データを保護するためにデータベースのバックアップを作成するだけでなく、データ ボリューム コンテナーを使用することもできます。 このチュートリアルの冒頭では、`-v sql1data:/var/opt/mssql` パラメーターを指定して **sql1** コンテナーを作成しました。 **sql1data** データ ボリューム コンテナーによって **/var/opt/mssql** のデータが永続化され、コンテナーが削除された後でも残ります。 以下の手順では、**sql1** コンテナーを完全に削除した後、永続化されたデータを使って新しいコンテナー **sql2** を作成します。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. **sql1** コンテナーを停止します。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. コンテナーを削除します。 これによって、以前に作成した **sql1data** データ ボリューム コンテナーと、その中に永続化されているデータが削除されることはありません。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 新しいコンテナー **sql2** を作成し、**sql1data** データ ボリューム コンテナーを再利用します。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. これで Wide World Importers のデータベースが新しいコンテナーに追加されました。 クエリを実行して、以前に加えた変更を確認します。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA パスワードは、**sql2** コンテナーに対して指定したパスワード (`MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`) ではありません。 SQL Server のデータは、チュートリアルの前半で変更したパスワードを含め、すべて **sql1** から復元されました。 実際には、このような一部のオプションは、/var/opt/mssql にデータを復元することが原因で無視されます。 このため、パスワードはここに示されているように `<YourNewStrong!Passw0rd>` となります。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. **sql1** コンテナーを停止します。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. コンテナーを削除します。 これによって、以前に作成した **sql1data** データ ボリューム コンテナーと、その中に永続化されているデータが削除されることはありません。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 新しいコンテナー **sql2** を作成し、**sql1data** データ ボリューム コンテナーを再利用します。

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
    ```

1. これで Wide World Importers のデータベースが新しいコンテナーに追加されました。 クエリを実行して、以前に加えた変更を確認します。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA パスワードは、**sql2** コンテナーに対して指定したパスワード (`MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`) ではありません。 SQL Server のデータは、チュートリアルの前半で変更したパスワードを含め、すべて **sql1** から復元されました。 実際には、このような一部のオプションは、/var/opt/mssql にデータを復元することが原因で無視されます。 このため、パスワードはここに示されているように `<YourNewStrong!Passw0rd>` となります。

::: moniker-end

## <a name="next-steps"></a>次のステップ

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

このチュートリアルでは、Windows 上でデータベースをバックアップし、SQL Server 2017 を稼働している Linux サーバーにそれを移動する方法について学習しました。 以下の方法を学習しました。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

このチュートリアルでは、Windows 上でデータベースをバックアップし、SQL Server 2019 が実行されている Linux サーバーにそれを移動する方法について学習しました。 以下の方法を学習しました。

::: moniker-end

> [!div class="checklist"]
> * SQL Server の Linux コンテナー イメージを作成する。
> * SQL Server データベースのバックアップをコンテナーにコピーする。
> * **sqlcmd** を使ってコンテナー内で Transact-SQL ステートメントを実行する。
> * コンテナーからバックアップ ファイルを作成して抽出する。
> * Docker のデータ ボリューム コンテナーを使って SQL Server データを永続化する。

次に、その他の Docker の構成とトラブルシューティングのシナリオを確認します。

> [!div class="nextstepaction"]
>[Docker 上の SQL Server 2017 の構成ガイド](sql-server-linux-configure-docker.md)
