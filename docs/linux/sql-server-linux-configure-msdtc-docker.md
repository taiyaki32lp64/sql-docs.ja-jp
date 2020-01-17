---
title: Docker 上の SQL Server による分散トランザクション (MSDTC)
description: Docker 上の SQL Server コンテナーの分散トランザクションで Microsoft 分散トランザクション コーディネーター (MSDTC) を使用する方法について説明します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 99c17e04e4352df91ad3c6028b3ec88fc5022c50
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558406"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Docker 上で SQL Server による分散トランザクションを使用する方法

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、分散トランザクションのために Docker 上に SQL Server Linux コンテナーをセットアップする方法について説明します。

SQL Server のコンテナー イメージでは、分散トランザクションに必要な Microsoft 分散トランザクション コーディネーター (MSDTC) を使用できます。 MSDTC での通信要件を理解するために、「[Linux 上の Microsoft 分散トランザクション コーディネーター (MSDTC) を構成する方法](sql-server-linux-configure-msdtc.md)」を参照してください。 この記事では、SQL Server の Docker コンテナーに関連する特別な要件とシナリオについて説明します。

## <a name="configuration"></a>構成

Docker に対するコンテナーにおいて MSDTC トランザクションを有効にするには、次の 2 つの新しい環境変数を設定する必要があります。

- **MSSQL_RPC_PORT**: RPC エンドポイント マッパー サービスがバインドされてリッスンする TCP ポート。  
- **MSSQL_DTC_TCP_PORT**: MSDTC サービスがリッスンするように構成されているポート。

### <a name="pull-and-run"></a>プルおよび実行

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

次の例では、これらの環境変数を使用して、MSDTC 用に構成された 1 つの SQL Server 2017 コンテナーをプルして実行する方法を示しています。 これにより、任意のホスト上の任意のアプリケーションと通信できるようになります。

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

次の例では、これらの環境変数を使用して、MSDTC 用に構成された 1 つの SQL Server 2019 コンテナーをプルして実行する方法を示しています。 これにより、任意のホスト上の任意のアプリケーションと通信できるようになります。

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

> [!IMPORTANT]
> 上記のコマンドは、Linux 上で実行される Docker に対してのみ機能します。 Windows 上にある Docker の場合は、Windows ホストによって既にポート 135 上でリッスンされています。 Windows 上の Docker に対する `-p 135:135` パラメーターを削除することは可能ですが、いくつかの制限があります。 作成されたコンテナーは、ホストに関連する分散トランザクションには使用できません。ホスト上にある Docker コンテナー間での分散トランザクションのみに使用できます。

このコマンドでは、**RPC エンドポイント マッパー サービス**がポート 135 にバインドされ、**MSDTC** サービスが Docker 仮想ネットワーク内のポート 51000 にバインドされています。 SQL Server の TDS 通信は、Docker 仮想ネットワーク内のポート 1433 上で行われます。 これらのポートは、TDS ポート 51433、RPC エンドポイント マッパーポート 135、および MSDTC ポート 51000 としてホストするために、外部に公開されています。

> [!NOTE]
> RPC エンドポイント マッパーと MSDTC ポートは、ホストとコンテナー上で同一になっている必要はありません。 そのため、RPC エンドポイント マッパーのポートはコンテナー上で 135 になるように構成されると共に、潜在的にはポート 13501 またはホスト サーバー上で利用できるその他の任意のポートにマップされる可能性があります。

## <a name="configure-the-firewall"></a>ファイアウォールの構成

ホストと通信するためには、コンテナー用のホスト サーバー上にファイアウォールを構成する必要もあります。 Docker コンテナーが外部通信用に公開しているすべてのポートに対して、ファイアウォールを開きます。 前の例では、これはポート 135、51433、および 51000 になります。 これらは、ホスト自体にあるポートであり、コンテナー内でマップされているポートではありません。 そのため、コンテナーの RPC エンドポイント マッパーのポート 51000 がホストのポート 51001 にマップされた場合は、ホストとの通信のためにファイアウォールに (51000 ではなく) ポート 51001 を開く必要があります。  

次の例は、Ubuntu 上でこれらの規則を作成する方法を示しています。

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

次の例は、Red Hat Enterprise Linux (RHEL) 上でこれを行う方法を示しています。

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>ホスト上にポートのルーティングを構成する

前の例では、1 つの Docker コンテナーが RPC ポート 135 をホスト上のポート 135 にマップするため、それ以上構成しなくても、ホストによる分散トランザクションが機能するようになっています。 それらのコンテナーでは昇格された特権によって SQL Server が実行されるため、ルートとして実行されているコンテナー内でポート 135 を直接使用できることに注意してください。 コンテナー外にある SQL Server の場合、または非ルート コンテナーの場合、別の一時的なポート (13500 など) が使用される必要があり、ポート 135 へのトラフィックはそのポートにルーティングされる必要があります。 コンテナー内のポート ルーティング規則を、コンテナー ポート 135 から一時的なポートに構成する必要もあります。

また、コンテナーのポート 135 をホスト上の別のポート (13500 など) にマップすることに決めた場合は、ホスト上にポートのルーティングを構成する必要があります。 これにより、ホストやその他の外部サーバーでの分散トランザクションに、Docker コンテナーを利用できるようになります。

ポートのルーティングの詳細については、「[ポートのルーティングを構成する](sql-server-linux-configure-msdtc.md#configure-port-routing)」を参照してください。

> [!NOTE]
> SQL Server 2017 は既定でルート コンテナーで実行されるのに対し、SQL Server 2019 コンテナーは非ルート ユーザーとして実行されます。

## <a name="next-steps"></a>次のステップ

Linux 上での MSDTC に関する詳細については、「[Linux 上の Microsoft 分散トランザクション コーディネーター (MSDTC) を構成する方法](sql-server-linux-configure-msdtc.md)」を参照してください。
