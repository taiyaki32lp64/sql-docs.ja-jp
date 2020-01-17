---
title: Docker 上の SQL Server の構成オプション
description: Docker 内での SQL Server 2017 および 2019 のコンテナー イメージの使用方法と操作方法について説明します。 これには、データの保持、ファイルのコピー、トラブルシューティングが含まれます。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 74168c8cd846f48fdaa87568b85c124ff755489a
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75721562"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Docker 上で SQL Server コンテナー イメージを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Docker を使用して [mssql-server-linux コンテナー イメージ](https://hub.docker.com/_/microsoft-mssql-server)を構成し、使用する方法について説明します。 

その他の展開シナリオは次のとおりです。

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - ビッグ データ クラスター](../big-data-cluster/deploy-get-started.md)

このイメージは Ubuntu 16.04 に基づく Linux で実行されている SQL Server で構成されます。 イメージは Linux の Docker エンジン 1.8+ または Mac/Windows 用 Docker で使用することができます。

> [!NOTE]
> この記事では特に mssql-server-linux イメージを使用することに焦点を当てます。 Windows イメージについては言及しませんが、[msmssql-server-windows Docker Hub ページ](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)で詳細を確認できます。

> [!IMPORTANT]
> 運用環境のユース ケースで SQL Server コンテナーを実行する前に、[SQL Server コンテナーのサポート ポリシー](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)を読み、サポートされる構成で実行していることを確認してください。

この 6 分間のビデオでは、コンテナーでの SQL Server の実行について説明します。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>コンテナー イメージのプルと実行

SQL Server 2017 および SQL Server 2019 用の Docker コンテナー イメージをプルして実行するには、次のクイックスタートの前提条件と手順に従います。

- [Docker を使用して SQL Server 2017 コンテナー イメージを実行する](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Docker を使用して SQL Server 2019 コンテナー イメージを実行する](quickstart-install-connect-docker.md?view=sql-server-ver15)

この構成記事では、以下のセクションで追加の使用シナリオを示します。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> RHEL ベースのコンテナー イメージを実行する

SQL Server Linux コンテナー イメージに関するドキュメントは、Ubuntu ベースのコンテナーを指しています。 SQL Server 2019 以降では、Red Hat Enterprise Linux (RHEL) に基づくコンテナーを使用できます。 すべての Docker コマンド内のコンテナー リポジトリを **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04** から **mcr.microsoft.com/mssql/rhel/server:2019-RC1** に変更します。

たとえば、次のコマンドでは、RHEL を使用する最新の SQL Server 2019 コンテナーをプルします。

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-RC1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-RC1
```

> [!NOTE]
> SQL Server 2019 の GA リリースの時点で、最新の RHEL コンテナー イメージは RC1 バージョンのままです。 このバージョンは、運用環境での使用を目的としたものではありません。 この記事は、新しい RHEL コンテナー イメージが使用可能になったときに更新されます。

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> 実稼働のコンテナー イメージを実行する

前のセクションのクイックスタートでは、Docker Hub から SQL Server の無償の Developer エディションを実行します。 Enterprise Edition、Standard Edition、Web Edition などの実稼働のコンテナー イメージを実行する場合でも、ほとんどの情報が適用されます。 しかし、違う点もいくつかあります。それをここで概説します。

- 有効なライセンスを持っている場合にのみ、運用環境内で SQL Server を使用できます。 無償の SQL Server Express 運用ライセンスは[こちら](https://go.microsoft.com/fwlink/?linkid=857693)で入手できます。 SQL Server Standard Edition と Enterprise Edition のライセンスは、[Microsoft ボリューム ライセンス](https://www.microsoft.com/licensing/default.aspx)を通じて入手できます。


- Developer コンテナー イメージは、実稼働エディションを実行するように構成することもできます。 実稼働エディションを実行するには、次の手順に従います。

要件を確認し、[クイックスタート](quickstart-install-connect-docker.md)の手順を実行します。 **MSSQL_PID** 環境変数を使用して、実稼働エディションを指定する必要があります。 次の例は、Enterprise Edition 用の最新の SQL Server 2017 コンテナー イメージを実行する方法を示しています。

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
 ```

> [!IMPORTANT]
> 値 **Y** を環境変数 **ACCEPT_EULA** に渡し、エディション値を **MSSQL_PID** に渡すことによって、使用する予定の SQL Server のエディションとバージョンに対して有効な既存のライセンスがあることを示しています。 また、Docker コンテナー イメージ内で実行されている SQL Server ソフトウェアの使用は SQL Server ライセンスの条項によって管理されることに同意します。

> [!NOTE]
> **MSSQL_PID** に使用できる値の完全な一覧については、「[Linux 上の SQL Server の設定を環境変数で構成する](sql-server-linux-configure-environment-variables.md)」を参照してください。

::: moniker-end

## <a name="connect-and-query"></a>接続とクエリ

コンテナーの外部またはコンテナーの内部から、コンテナー内の SQL Server に接続してクエリを実行できます。 次のセクションでは、両方のシナリオについて説明します。 

### <a name="tools-outside-the-container"></a>コンテナーの外部のツール

SQL 接続をサポートする外部の Linux、Windows、macOS ツールから、Docker マシン上の SQL Server インスタンスに接続することができます。 いくつかの一般的なツールを次に示します。

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows の SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

次の例では、**sqlcmd** を使用して、Docker コンテナー内で実行されている SQL Server に接続します。 接続文字列内の IP アドレスは、コンテナーを実行しているホスト マシンの IP アドレスです。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

既定の **1433** ではないホスト ポートをマップした場合は、そのポートを接続文字列に追加します。 たとえば、`docker run` コマンド内で `-p 1400:1433` を指定した場合は、ポート 1400 を明示的に指定して接続します。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>コンテナーの内部のツール

SQL Server 2017 以降では、[SQL Server のコマンドライン ツール](sql-server-linux-setup-tools.md)がコンテナー イメージに含まれています。 対話型のコマンド プロンプトを使用してイメージにアタッチすると、ツールをローカルで実行できます。

1. 実行中のコンテナー内で対話型の Bash シェルを開始するには、`docker exec -it` コマンドを使用します。 次の例では、`e69e056c702d` はコンテナー ID です。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 常にコンテナー ID 全体を指定する必要はありません。一意に識別するのに十分な文字を指定するだけでかまいません。 したがって、この例では、完全な ID ではなく `e6` または `e69` を使用すれば十分な可能性があります。

2. コンテナー内では sqlcmd とローカル接続してください。 既定では sqlcmd はパスにないため、完全なパスを指定する必要があることにご注意ください。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. sqlcmd が終了したら、「`exit`」と入力します。

4. 対話型コマンド プロンプトでの操作が完了したら、「`exit`」と入力します。 コンテナーは、対話型の Bash シェルを終了した後も引き続き実行されます。

## <a name="run-multiple-sql-server-containers"></a>複数の SQL Server コンテナーを実行する

Docker には、同じホスト マシン上で複数の SQL Server コンテナーを実行する方法が用意されています。 このアプローチは、同じホスト上に複数の SQL Server インスタンスを必要とするシナリオで使用します。 各コンテナーは、異なるポート上で公開される必要があります。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

次の例では、2 つの SQL Server 2017 コンテナーを作成して、ホスト マシン上のポート **1401** と **1402** にマップします。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

次の例では、2 つの SQL Server 2019 コンテナーを作成して、ホスト マシン上のポート **1401** と **1402** にマップします。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

これで、SQL Server の 2 つのインスタンスが別々のコンテナー内で実行されるようになりました。 クライアントは、Docker ホストの IP アドレスとコンテナーのポート番号を使用して、各 SQL Server インスタンスに接続できます。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> カスタマイズしたコンテナーを作成する

独自の [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) を作成して、カスタマイズされた SQL Server コンテナーを作成することができます。 詳しくは、[SQL Server とノード アプリケーションを組み合わせたデモ](https://github.com/twright-msft/mssql-node-docker-demo-app)をご覧ください。 独自の Dockerfile を作成する場合は、フォアグラウンド プロセスに注意してください。このプロセスによってコンテナーの有効期間が制御されるためです。 終了すると、コンテナーがシャットダウンされます。 たとえば、スクリプトを実行して SQL Server を開始する場合は、SQL Server プロセスが一番右のコマンドであることを確認します。 その他のコマンドはすべてバックグラウンドで実行されます。 次のコマンドは、Dockerfile 内でのこのことを示しています。

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

前の例のコマンドを元に戻した場合、do-my-sql-commands.sh スクリプトの完了時にコンテナーがシャットダウンされます。

## <a id="persist"></a> データを保持する

`docker stop` と `docker start` を使用してコンテナーを再起動しても、SQL Server の構成変更とデータベース ファイルはコンテナーに保持されています。 一方、`docker rm` を使用してコンテナーを削除すると、SQL Server とデータベースを含め、コンテナーの内容がすべて削除されます。 次のセクションでは、関連付けられているコンテナーが削除された場合でも、**データ ボリューム**を使用してデータベース ファイルを保持する方法について説明します。

> [!IMPORTANT]
> SQL Server の場合、Docker 内でのデータの保持について理解しておくことが重要です。 このセクションの説明に加えて、[Docker コンテナー内でデータを管理する方法](https://docs.docker.com/engine/tutorials/dockervolumes/)については、Docker のドキュメントをご覧ください。

### <a name="mount-a-host-directory-as-data-volume"></a>ホスト ディレクトリをデータ ボリュームとしてマウントする

1 つ目のオプションは、ホスト上のディレクトリをコンテナー内のデータ ボリュームとしてマウントすることです。 これを行うには、`docker run` コマンドを `-v <host directory>:/var/opt/mssql` フラグと共に使用します。 これにより、コンテナーの実行間でデータを復元できます。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

この手法では、Docker の外部にあるホスト上のファイルを共有して表示することもできます。

> [!IMPORTANT]
> **Windows 上の Docker** のホスト ボリューム マッピングでは現在のところ、完全な `/var/opt/mssql` ディレクトリをマッピングできません。 ただし、`/var/opt/mssql/data` など、サブディレクトリをホスト コンピューターにマッピングできます。

> [!IMPORTANT]
> 現時点では、SQL Server on Linux イメージを使用した **Mac 上の Docker** のホスト ボリューム マッピングはサポートされていません。 代わりにデータ ボリューム コンテナーを使用してください。 この制限は、`/var/opt/mssql` ディレクトリに固有のものです。 マウントされたディレクトリからの読み取りは正常に機能します。 たとえば、Mac 上で -v を使用してホスト ディレクトリをマウントし、ホスト上に存在する .bak ファイルからバックアップを復元することができます。

### <a name="use-data-volume-containers"></a>データ ボリューム コンテナーを使用する

2 つ目のオプションは、データ ボリューム コンテナーを使用することです。 `-v` パラメーターを使用してホスト ディレクトリではなくボリューム名を指定して、データ ボリューム コンテナーを作成できます。 次の例では、**sqlvolume** という名前の共有データ ボリュームを作成します。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> 実行コマンド内でデータ ボリュームを暗黙的に作成するためのこの手法は、以前のバージョンの Docker では動作しません。 その場合は、Docker のドキュメント、「[データ ボリューム コンテナーの作成とマウント](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)」に概説されている明示的な手順を使用します。

このコンテナーを停止して削除しても、データ ボリュームは保持されます。 `docker volume ls` コマンドを使用して表示できます。

```bash
docker volume ls
```

その後、同じボリューム名を持つ別のコンテナーを作成すると、新しいコンテナーでは、ボリュームに含まれているのと同じ SQL Server データが使用されます。

データ ボリューム コンテナーを削除するには、`docker volume rm` コマンドを使用します。

> [!WARNING]
> データ ボリューム コンテナーを削除すると、コンテナー内のすべての SQL Server データがすべて*完全に*削除されます。

### <a name="backup-and-restore"></a>バックアップと復元

これらのコンテナー手法に加えて、標準の SQL Server バックアップと復元の手法を使用することもできます。 バックアップ ファイルを使用して、データを保護したり、別の SQL Server インスタンスにデータを移動したりすることができます。 詳細については、「[Linux 上での SQL Server データベースのバックアップと復元](sql-server-linux-backup-and-restore-database.md)」を参照してください。

> [!WARNING]
> バックアップを作成する場合は、必ずコンテナーの外部でバックアップ ファイルを作成またはコピーしてください。 そうしないと、コンテナーが削除された場合に、バックアップ ファイルも削除されます。

## <a name="execute-commands-in-a-container"></a>コンテナー内でコマンドを実行する

実行中のコンテナーがある場合は、ホスト ターミナルからコンテナー内でコマンドを実行できます。

コンテナー ID を取得するには、次のように実行します。

```bash
docker ps
```

コンテナー内で bash ターミナルを開始するには、次のように実行します。

```bash
docker exec -it <Container ID> /bin/bash
```

これで、コンテナーの内部のターミナルで実行する場合と同じようにコマンドを実行できるようになりました。 終わったら、`exit` と入力します。 これにより対話型コマンド セッションが終了しますが、コンテナーは引き続き実行されます。

## <a name="copy-files-from-a-container"></a>コンテナーからファイルをコピーする

コンテナーからファイルをコピーするには、次のコマンドを使用します。

```bash
docker cp <Container ID>:<Container path> <host path>
```

**例:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>コンテナーにファイルをコピーする

コンテナーにファイルをコピーするには、次のコマンドを使用します。

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**例:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a> タイムゾーンを構成する

特定のタイムゾーンを持つ Linux コンテナー内で SQL Server を実行するには、`TZ` 環境変数を構成します。 適切なタイムゾーン値を検索するには、Linux bash プロンプトから `tzselect` コマンドを実行します。

```bash
tzselect
```

タイムゾーンを選択すると、`tzselect` に次のような出力が表示されます。

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

この情報を使用して、Linux コンテナー内で同じ環境変数を設定できます。 次の例は、`Americas/Los_Angeles` タイムゾーンのコンテナー内で SQL Server を実行する方法を示しています。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a id="tags"></a> 特定の SQL Server コンテナー イメージを実行する

最新の SQL Server コンテナー イメージを使用したくないシナリオもあります。 特定の SQL Server コンテナー イメージを実行するには、次の手順を使用します。

1. 使用するリリースの Docker **タグ**を特定します。 利用可能なタグを表示するには、[mssql-server-linux Docker Hub ページ](https://hub.docker.com/_/microsoft-mssql-server)を参照してください。

2. タグを使用して SQL Server コンテナー イメージをプルします。 たとえば、RC1 イメージをプルするには、次のコマンド内の `<image_tag>` を `rc1` に置き換えます。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. そのイメージを使用して新しいコンテナーを実行するには、`docker run` コマンド内でタグ名を指定します。 次のコマンド内の `<image_tag>` を、実行するバージョンに置き換えます。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

これらの手順は、既存のコンテナーをダウングレードするためにも使用できます。 たとえば、実行中のコンテナーをロールバックまたはダウングレードして、トラブルシューティングやテストを行うことができます。 実行中のコンテナーをダウングレードするには、データ フォルダーの永続化手法を使用する必要があります。 [アップグレードのセクション](#upgrade)で説明したのと同じ手順に従いますが、新しいコンテナーを実行するときに、古いバージョンのタグ名を指定します。

## <a id="version"></a> コンテナーのバージョンを確認する

実行中の docker コンテナー内の SQL Server のバージョンを知りたい場合は、次のコマンドを実行して表示します。 `<Container ID or name>` はターゲット コンテナーの ID または名前で置き換えます。 `<YourStrong!Passw0rd>` は SA ログインの SQL Server パスワードで置き換えます。

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

ターゲットの docker コンテナー イメージの SQL Server バージョンとビルド番号を特定することもできます。 次のコマンドでは、**mcr.microsoft.com/mssql/server:2017-latest** イメージの SQL Server バージョンとビルド情報が表示されます。 これは、環境変数 **PAL_PROGRAM_INFO=1** を使用して新しいコンテナーを実行することで行われます。 結果のコンテナーはすぐに終了し、`docker rm` コマンドによって削除されます。

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

上記のコマンドでは、次の出力のようなバージョン情報が表示されます。

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a id="upgrade"></a> コンテナー内の SQL Server をアップグレードする

Docker を使用してコンテナー イメージをアップグレードするには、まず、アップグレードするリリースのタグを特定します。 `docker pull` コマンドを使用して、このバージョンをレジストリからプルします。

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

これにより、作成した新しいコンテナーの SQL Server イメージが更新されますが、実行中のコンテナー内で SQL Server は更新されません。 これを行うには、最新の SQL Server コンテナー イメージを使用して新しいコンテナーを作成し、その新しいコンテナーにデータを移行する必要があります。

1. 既存の SQL Server コンテナーに対して[データの保持手法](#persist)の 1 つを使用していることを確認します。 これにより、同じデータを使用して新しいコンテナーを開始できます。

1. `docker stop` コマンドを使用して SQL Server コンテナーを停止します。

1. `docker run` を使用して新しい SQL Server コンテナーを作成し、マップされたホスト ディレクトリまたはデータ ボリューム コンテナーを指定します。 SQL Server のアップグレードには、必ず特定のタグを使用してください。 新しいコンテナーでは、新しいバージョンの SQL Server が既存の SQL Server データと共に使用されるようになります。

   > [!IMPORTANT]
   > 現時点では、アップグレードは RC1、RC2、GA の間でのみサポートされます。

1. 新しいコンテナー内のデータベースとデータを確認します。

1. 必要に応じて、`docker rm` を使用して古いコンテナーを削除します。

## <a id="buildnonrootcontainer"></a>非ルート SQL Server 2017 コンテナーを作成して実行する

次の手順に従って、`mssql` (非ルート) ユーザーとして起動する SQL Server 2017 コンテナーを作成します。

> [!NOTE]
> SQL Server 2019 コンテナーは自動的に非ルートとして起動するため、次の手順は、既定でルートとして起動する SQL Server 2017 コンテナーにのみ適用されます。

1. [非ルート SQL Server コンテナー用のサンプル dockerfile](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile) をダウンロードし、`dockerfile` として保存します。
 
2. dockerfile ディレクトリのコンテキストで次のコマンドを実行して、非ルート SQL Server コンテナーを作成します。

```bash
cd <path to dockerfile>
docker build -t 2017-latest-non-root .
```
 
3. コンテナーを開始します。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
```

> [!NOTE]
> 非ルート SQL Server コンテナーによってトラブルシューティング用のダンプが生成されるようにするには、`--cap-add SYS_PTRACE` フラグが必要です。
 
4. コンテナーが非ルート ユーザーとして実行されていることを確認します。

docker exec をコンテナーに挿入します。
```bash
docker exec -it sql1 bash
```
 
`whoami` を実行します。これにより、コンテナー内で実行されているユーザーが返されます。
 
```bash
whoami
```

## <a id="nonrootuser"></a> ホスト上で別の非ルート ユーザーとしてコンテナーを実行する

SQL Server コンテナーを別の非ルート ユーザーとして実行するには、-u フラグを docker run コマンドに追加します。 非ルート コンテナーに適用される制限として、非ルート ユーザーがアクセスできる '/var/opt/mssql' にボリュームがマウントされていない場合、ルート グループの一部として実行される必要があります。 ルート グループから非ルート ユーザーに対して追加のルート アクセス許可は付与されません。
 
**UID 4000 を持つユーザーとして実行する**
 
カスタム UID を使用して SQL Server を開始できます。 たとえば、次のコマンドでは UID 4000 を使用して SQL Server が開始されます。
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
 
> [!Warning]
> SQL Server コンテナーに 'mssql' や 'root' などの名前付きユーザーが含まれていることを確認してください。そうしないと、コンテナー内で SQLCMD を実行できません。 SQL Server コンテナーが名前付きユーザーとして実行されているかどうかは、コンテナー内で `whoami` を実行することで確認できます。

**非ルート コンテナーをルート ユーザーとして実行する**

必要に応じて、非ルート コンテナーをルート ユーザーとして実行できます。 この場合はまた、より高い特権となるため、コンテナーにすべてのファイル アクセス許可が自動的に付与されます。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
 
**ご利用のホスト コンピューター上のユーザーとして実行する**
 
次のコマンドを使用すれば、ホスト コンピューター上の既存のユーザーで SQL Server を開始できます。
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
 
**別のユーザーおよびグループとして実行する**
 
カスタムのユーザーおよびグループで SQL Server を開始できます。 この例では、マウントされたボリュームには、ホスト コンピューター上のユーザーまたはグループ用に構成されたアクセス許可があります。
 
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
 
## <a id="storagepermissions"></a> 非ルート コンテナーに対して永続的なストレージ アクセス許可を構成する

マウントされたボリューム上にある DB ファイルへのアクセスを非ルート ユーザーに許可するには、ご自分がコンテナーを実行する場合のユーザーまたはグループが永続的なファイル ストレージにアクセスできることを確認します。  

次のコマンドを使用すれば、データベース ファイルの現在の所有権を取得できます。
 
```bash
ls -ll <database file dir>
```

永続化されたデータベース ファイルへのアクセス権が SQL Server にない場合は、次のいずれかのコマンドを実行します。
 
**DB ファイルへの R/W アクセス権をルート グループに付与する**

非ルート SQL Server コンテナーがデータベース ファイルにアクセスできるように、次のディレクトリへのアクセス許可をルート グループに付与します。

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**非ルート ユーザーをファイルの所有者として設定します。**

これは、既定の非ルート ユーザーとすることも、その他の任意の非ルート ユーザーを指定することもできます。 この例では、UID 10001 を非ルート ユーザーとして設定します。

```bash
chown -R 10001:0 <database file dir>
```

## <a id="changefilelocation"></a> 既定のファイルの場所を変更する

ご利用の `docker run` コマンド内にデータ ディレクトリを変更するための `MSSQL_DATA_DIR` 変数を追加してしてから、ご利用のコンテナーのユーザーがアクセスできるその場所にボリュームをマウントします。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="troubleshooting"></a> トラブルシューティング

以下のセクションでは、コンテナー内で実行中の SQL Server に対するトラブルシューティングの推奨事項について説明します。

### <a name="docker-command-errors"></a>Docker コマンドのエラー

いずれかの `docker` コマンドでエラーが発生した場合は、docker サービスが実行されていることを確認し、高度な権限を使用して実行してみてください。

たとえば、Linux 上では、`docker` コマンドの実行時に次のエラーが表示される場合があります。

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux 上でこのエラーが発生した場合は、前に `sudo` を付けて同じコマンドを実行してみてください。 これが失敗した場合は、docker サービスが実行されていることを確認し、必要に応じて開始します。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows では、PowerShell またはコマンド プロンプトを管理者として起動していることを確認します。

### <a name="sql-server-container-startup-errors"></a>SQL Server コンテナーのスタートアップ エラー

SQL Server コンテナーの実行に失敗する場合は、次のテストを試してください。

- **"failed to create endpoint CONTAINER_NAME on network bridge.Error starting proxy: listen tcp 0.0.0.0:1433 bind: address already in use."** などのエラーが表示される場合は、コンテナー ポート 1433 を既に使用中のポートにマップしようとしています。 これは、ホスト マシン上で SQL Server をローカルに実行している場合に発生する可能性があります。 また、2 つの SQL Server コンテナーを開始し、両方を同じホスト ポートにマップしようとした場合にも発生する可能性があります。 この状況が発生した場合は、`-p` パラメーターを使用して、コンテナー ポート 1433 を別のホスト ポートにマップします。 次に例を示します。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- **"Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock:Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied"** などのエラーが表示される場合は、コンテナーを起動しようとするときに、Ubuntu 内の docker グループにユーザーを追加します。 その後、この変更が新しいセッションに影響するため、ログアウトしてもう一度ログインします。 

   ```bash
    usermod -aG docker $USER
    ```
- コンテナーからのエラー メッセージがあるかどうかを確認します。

    ```bash
    docker logs e69e056c702d
    ```

- クイックスタートの記事の「[前提条件](quickstart-install-connect-docker.md#requirements)」セクションで指定されている最小メモリおよびディスク要件を満たしていることを確認します。

- コンテナー管理ソフトウェアを使用している場合は、ルートとして実行されているコンテナー プロセスがサポートされていることを確認します。 コンテナー内の sqlservr プロセスは、ルートとして実行されます。

- 「[SQL Server のセットアップ ログとエラー ログ](#errorlogs)」を確認してください。

### <a name="enable-dump-captures"></a>ダンプ キャプチャを有効にする

SQL Server プロセスがコンテナーの内部で失敗している場合は、**SYS_PTRACE** が有効になった新しいコンテナーを作成する必要があります。 これにより、プロセスをトレースするための Linux 機能が追加されます。これは、例外発生時にダンプ ファイルを作成するために必要です。 ダンプ ファイルは、問題のトラブルシューティングを支援するためにサポートによって使用できます。 次の docker run コマンドを使用すると、この機能が有効になります。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 接続の失敗

コンテナー内で実行されている SQL Server インスタンスに接続できない場合は、次のテストを試してください。

- `docker ps -a` 出力の **STATUS** 列を参照して、SQL Server コンテナーが実行されていることを確認します。 そうでない場合は、`docker start <Container ID>` を使用して開始します。

- (1433 ではなく) 既定以外のホスト ポートにマップした場合は、接続文字列内でポートを指定していることを確認してください。 ポート マッピングは、`docker ps -a` 出力の **PORTS** 列に表示されます。 たとえば、次のコマンドでは、sqlcmd をポート 1401 上でリッスンしているコンテナーに接続します。

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 既存のマップ済みデータ ボリュームまたはデータ ボリューム コンテナーと共に `docker run` を使用した場合、SQL Server では `MSSQL_SA_PASSWORD` の値が無視されます。 代わりに、事前に構成された SA ユーザーのパスワードが、データ ボリュームまたはデータ ボリューム コンテナー内の SQL Server データから使用されます。 アタッチ先のデータに関連付けられている SA パスワードを使用していることを確認します。

- 「[SQL Server のセットアップ ログとエラー ログ](#errorlogs)」を確認してください。

### <a name="sql-server-availability-groups"></a>SQL Server の可用性グループ

SQL Server の可用性グループと共に Docker を使用している場合は、2 つの追加要件があります。

- レプリカ通信に使用されるポートをマップします (既定値は 5022)。 たとえば、`docker run` コマンドの一部として `-p 5022:5022` を指定します。

- `docker run` コマンドの `-h YOURHOSTNAME` パラメーターを使用して、コンテナーのホスト名を明示的に設定します。 このホスト名は、可用性グループを構成するときに使用されます。 `-h` を使用して指定しない場合は、既定でコンテナー ID が使用されます。

### <a id="errorlogs"></a> SQL Server のセットアップ ログとエラー ログ

SQL Server のセットアップ ログとエラー ログは、 **/var/opt/mssql/log** 内で確認できます。 コンテナーが実行されていない場合は、まずコンテナーを開始します。 次に、対話型のコマンド プロンプトを使用して、ログを検査します。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

コンテナーの内部の bash セッションから、次のコマンドを実行します。

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> コンテナーの作成時にホスト ディレクトリを **/var/opt/mssql** にマウントした場合は、代わりに、ホスト上のマップされたパスにある **log** サブディレクトリを調べることができます。

## <a name="next-steps"></a>次のステップ

[クイックスタート](quickstart-install-connect-docker.md)に従って、Docker 上で SQL Server 2017 のコンテナー イメージを開始します。

リソース、フィードバック、既知の問題について、[mssql-docker GitHub リポジトリ](https://github.com/Microsoft/mssql-docker)も参照してください。

[SQL Server のコンテナー用の可用性グループを調べる](sql-server-linux-container-ha-overview.md)
