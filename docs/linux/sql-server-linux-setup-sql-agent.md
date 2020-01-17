---
title: Linux 上での SQL Server エージェントのインストールを構成する
description: この記事では、Linux 上での SQL Server エージェントの有効化またはインストールの方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 12/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: b281c60248d86daba36a2cf5628e1ae729d227fe
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258389"
---
# <a name="install-sql-server-agent-on-linux"></a>Linux 上に SQL Server エージェントをインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上での SQL Server エージェントの有効化またはインストールの方法について説明します。

[SQL Server エージェント](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)は、スケジュールされた SQL Server ジョブを実行します。 SQL Server 2017 CU4 以降、SQL Server エージェントは **mssql-Server** パッケージに含まれており、既定で無効になっています。 このリリースの SQL Server エージェントでサポートされている機能とバージョン情報については、[リリース ノート](sql-server-linux-release-notes.md)を参照してください。

## <a name="instructions"></a>Instructions

Linux 上で SQL Server エージェントを使用する前に、次の手順に従って、有効化またはインストールを行います。

1. `/etc/hosts` ファイルにホスト名を追加します (ドメインあり、およびドメインなし)。 次の各行は、このエントリの形式の例です。

   ```bash
   "IP Address" "hostname"
   "IP Address" "hostname.domain.com"
   ```

1. SQL Server のバージョンに応じて、次のいずれかのセクションの手順に従います。

   | バージョン | Instructions |
   |---|---|
   | SQL Server 2017 CU4 以降</br>SQL Server 2019 | [SQL Server エージェントを有効にする](#EnableAgentAfterCU4) |
   | SQL Server 2017 CU3 以前 | [SQL Server エージェントをインストールする](#InstallAgentBelowCU4) |

## <a id="EnableAgentAfterCU4"></a>SQL Server エージェントを有効にする

SQL Server 2019 および SQL Server 2017 CU4 以降では、SQL Server エージェントの有効化のみが必要です。 別途パッケージをインストールする必要はありません。

SQL Server エージェントを有効にするには、次の手順に従います。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> エージェントがインストールされている 2017 CU3 以前からアップグレードすると、SQL Server エージェントが自動的に有効になり、前のエージェント パッケージはアンインストールされます。  

## <a name="InstallAgentBelowCU4"></a>SQL Server エージェントをインストールする

SQL Server 2017 CU3 以前では、SQL Server エージェント パッケージをインストールする必要があります。

> [!NOTE]
> 以下のインストール手順は SQL Server バージョン 2017 CU3 以前に適用されます。 SQL Server エージェントをインストールする前に、まず [SQL Server をインストール](sql-server-linux-setup.md#platforms)してください。 これにより **mssql-server-agent** パッケージをインストールするときに使用されるキーとリポジトリが構成されます。

お使いのプラットフォーム用の SQL Server エージェントをインストールします。
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">RHEL へのインストール</a>

次の手順を使用して、Red Hat Enterprise Linux に **mssql-server-agent** をインストールします。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

既に **mssql-server-agent** がインストールされている場合は、次のコマンドを使用して最新バージョンに更新できます。

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)の SQL Server エージェント パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

### <a name="ubuntu">Ubuntu へのインストール</a>

次の手順を使用して、Ubuntu に **mssql-server-agent** をインストールします。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

既に **mssql-server-agent** がインストールされている場合は、次のコマンドを使用して最新バージョンに更新できます。

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)の SQL Server エージェント パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

### <a name="SLES">SLES へのインストール</a>

次の手順を使用して、SUSE Linux Enterprise Server に **mssql-server-agent** をインストールします。 

**mssql-server-agent** をインストールします。 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

既に **mssql-server-agent** がインストールされている場合は、次のコマンドを使用して最新バージョンに更新できます。

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)の SQL Server エージェント パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="next-steps"></a>次のステップ
SQL Server エージェントを使用してジョブを作成、スケジュール設定、および実行する方法について詳しくは、[Linux 上での SQL Server エージェント ジョブの実行](sql-server-linux-run-sql-server-agent-job.md)に関するページをご覧ください。
