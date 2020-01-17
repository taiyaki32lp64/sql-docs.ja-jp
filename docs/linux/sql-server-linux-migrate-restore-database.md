---
title: SQL Server データベースを Windows から Linux に移行する
description: このチュートリアルでは、Windows で SQL Server データベースのバックアップを作成し、SQL Server が実行されている Linux コンピューターに復元する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 148b887497cf9411aad72936a201805000c717ec
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558564"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>バックアップと復元を使用して SQL Server データベースを Windows から Linux に移行する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server のバックアップと復元の機能は、Windows の SQL Server から SQL Server on Linux にデータベースを移行する場合に推奨される方法です。 このチュートリアルでは、バックアップと復元の手法を使用してデータベースを Linux に移動するために必要な手順について説明します。

> [!div class="checklist"]
> * SSMS を使用して Windows でバックアップ ファイルを作成する
> * Windows に Bash シェルをインストールする
> * Bash シェルから Linux にバックアップ ファイルを移動する
> * Linux で Transact-SQL を使用してバックアップ ファイルを復元する
> * クエリを実行して移行を検証する

また、SQL Server Always On 可用性グループを作成して、SQL Server データベースを Windows から Linux に 移行することもできます。 「[Windows と Linux に SQL Server Always On 可用性グループを構成する (クロス プラットフォーム)](sql-server-linux-availability-group-cross-platform.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次の前提条件を満たす必要があります。

* 次のものを備えた Windows コンピューター:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) がインストールされている。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) がインストールされている。
  * 移行対象のデータベース。

* 次のものがインストールされた Linux コンピューター:
  * コマンドライン ツールを備えた SQL Server ([RHEL](quickstart-install-connect-red-hat.md)、[SLES](quickstart-install-connect-suse.md)、または [Ubuntu](quickstart-install-connect-ubuntu.md))。

## <a name="create-a-backup-on-windows"></a>Windows でバックアップを作成する

Windows でデータベースのバックアップ ファイルを作成するには、いくつかの方法があります。 以下の手順では、SQL Server Management Studio (SSMS) を使います。

1. Windows コンピューターで **SQL Server Management Studio** を開始します。

1. 接続ダイアログ ボックスで、「**localhost**」と入力します。

1. オブジェクト エクスプローラーで、 **[データベース]** を展開します。

1. 対象のデータベースを右クリックし、 **[タスク]** を選択して、 **[バックアップ...]** をクリックします。

   ![SSMS を使用してバックアップ ファイルを作成する](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. **[Backup Up Database]\(データベースのバックアップ\)** ダイアログで、 **[バックアップの種類]** が **[Full]\(完全\)** であり、 **[バックアップ先]** が **[ディスク]** であることを確認します。 ファイルの名前と場所を記録しておきます。 たとえば、SQL Server 2016 では、**YourDB** という名前のデータベースの既定のバックアップ パスは `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak` になります。

1. **[OK]** をクリックしてデータベースをバックアップします。

> [!NOTE]
> もう 1 つの方法は、Transact-SQL のクエリを実行してバックアップ ファイルを作成するこです。 次の Transact-SQL コマンドでは、**YourDB** という名前のデータベースに対して前の手順と同じ操作が実行されます。
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Windows に Bash シェルをインストールする

データベースを復元するには、最初に Windows コンピューターからターゲットの Linux コンピューターにバックアップ ファイルを転送する必要があります。 このチュートリアルでは、Windows 上で実行されている Bash シェル (ターミナル ウィンドウ) から Linux にファイルを移動します。

1. **scp** (セキュア コピー) コマンドと **ssh** (リモート ログイン) コマンドがサポートされている Bash シェルを、Windows コンピューターにインストールします。 次の 2 つの例があります。

   * [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * Git Bash シェル ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Windows で Bash セッションを開きます。

## <a id="scp"></a> バックアップ ファイルを Linux にコピーする

1. Bash セッションで、バックアップ ファイルが格納されているディレクトリに移動します。 次に例を示します。

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. **scp** コマンドを使って、ターゲットの Linux コンピューターにファイルを転送します。 次の例では、IP アドレスが *192.0.2.9* である Linux サーバー上の *user1* のホーム ディレクトリに、**YourDB.bak** を転送します。

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp コマンド](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> scp を使用したファイル転送の代わりになる方法があります。 1 つは、[Samba](https://help.ubuntu.com/community/Samba) を使用して、Windows と Linux の間に SMB ネットワーク共有を構成するというものです。 Ubuntu のチュートリアルについては、「[Samba を使用してネットワーク共有を作成する方法](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)」を参照してください。 確立された後は、Windows からネットワーク ファイル共有としてアクセスできます ( **\\\\machinenameorip\\share** など)。

## <a name="move-the-backup-file-before-restoring"></a>復元する前にバックアップ ファイルを移動する

この時点で、バックアップ ファイルは Linux サーバー上のユーザーのホーム ディレクトリにあります。 SQL Server にデータベースを復元する前に、 **/var/opt/mssql** のサブディレクトリにバックアップを配置する必要があります。

1. 同じ Windows Bash セッションで、**ssh** を使ってターゲット Linux コンピューターにリモート接続します。 次の例では、ユーザー **user1** として Linux コンピューター **192.0.2.9** に接続しています。

   ```bash
   ssh user1@192.0.2.9
   ```

   これで、リモート Linux サーバー上でコマンドが実行されるようになります。

1. スーパー ユーザー モードに移行します。

   ```bash
   sudo su
   ```

1. 新しいバックアップ ディレクトリを作成します。 ディレクトリが既に存在する場合は、-p パラメーターを指定しても何も行われません。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. バックアップ ファイルをそのディレクトリに移動します。 次の例では、バックアップ ファイルは *user1* のホーム ディレクトリにあります。 実際のバックアップ ファイルの場所とファイル名に合わせて、コマンドを変更してください。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. スーパー ユーザー モードを終了します。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Linux でデータベースを復元する

データベースのバックアップを復元するには、**RESTORE DATABASE** Transact-SQL (TQL) コマンドを使います。

> [!NOTE]
> 次の手順では、**sqlcmd** ツールを使います。 SQL Server ツールをインストールしていない場合は、[Linux への SQL Server コマンドライン ツールのインストール](sql-server-linux-setup-tools.md)に関する記事を参照してください。

1. 同じターミナルで、**sqlcmd** を起動します。 次の例では、**SA** ユーザーを使ってローカル SQL Server インスタンスに接続します。 プロンプトが表示されてからパスワードを入力するか、 **-P** パラメーターを追加してパスワードを指定します。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. `>1` プロンプトで、次の **RESTORE DATABASE** コマンドを入力します。1 行入力するごとに Enter キーを押します (複数行のコマンド全体を一度にコピーして貼り付けることはできません)。 すべての `YourDB` を、実際のデータベースの名前に置き換えます。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   データベースが正常に復元されたことを示すメッセージが表示されるはずです。

   `RESTORE DATABASE` では、次の例のようなエラーが返されることがあります。

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   この場合、データベースにはセカンダリ ファイルが含まれています。 これらのファイルを `RESTORE DATABASE` の `MOVE` 句で指定しないと、復元プロシージャでは元のサーバーと同じパスにこれらのファイルの作成が試みられます。 

   バックアップに含まれるすべてのファイルの一覧を表示できます。
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   次のような一覧が表示されます (最初の 2 列のみを示してあります)。
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   この一覧を使って、追加ファイルの `MOVE` 句を作成できます。 この例では、`RESTORE DATABASE` は次のようになります。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. サーバー上のすべてのデータベースの一覧を表示して、復元を確認します。 復元されたデータベースが一覧表示される必要があります。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 移行されたデータベースに対して他のクエリを実行します。 次のコマンドでは、コンテキストが **YourDB** データベースに切り替えられて、そのテーブルの 1 つから行が選択されます。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. **sqlcmd** の使用が終わったら、「`exit`」と入力します。

1. リモート **ssh** セッションでの作業が終わったら、「`exit`」と入力します。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、Windows 上でデータベースをバックアップし、SQL Server が実行されている Linux サーバーにそれを移動する方法について学習しました。 以下の方法を学習しました。
> [!div class="checklist"]
> * SSMS と Transact-SQL を使用して、Windows でバックアップ ファイルを作成する
> * Windows に Bash シェルをインストールする
> * **scp** を使用して、Windows から Linux にバックアップ ファイルを移動する
> * **ssh** を使用して、Linux コンピューターにリモート接続する
> * 復元の準備のためにバックアップ ファイルを再配置する
> * **sqlcmd** を使用して Transact-SQL コマンドを実行する
> * **RESTORE DATABASE** コマンドを使用して、データベースのバックアップを復元する 
> * クエリを実行して移行を検証する

次に、SQL Server on Linux の他の移行シナリオを調べます。 

> [!div class="nextstepaction"]
>[SQL Server on Linux にデータベースを移行する](sql-server-linux-migrate-overview.md)
