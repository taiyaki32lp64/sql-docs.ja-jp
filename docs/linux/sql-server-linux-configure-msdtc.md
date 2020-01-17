---
title: Linux で MSDTC を構成する方法
description: この記事では、Linux で MSDTC を構成する手順について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 08/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: a39e0a743053db694efc2d0e8176e659d7e376d1
ms.sourcegitcommit: 58f1d5498c87bfe0f6ec4fd9d7bbe723be47896b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995875"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Linux で Microsoft 分散トランザクション コーディネーター (MSDTC) を構成する方法

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux で Microsoft 分散トランザクション コーディネーター (MSDTC) を構成する方法を説明します。

> [!NOTE]
> Linux 上の MSDTC は、累積的な更新プログラム 16 以降が適用された SQL Server 2017 でサポートされています。

## <a name="overview"></a>概要

分散トランザクションをSQL Server on Linux で有効にするには、MSDTC および RPC エンドポイント マッパー機能を SQL Server に導入します。 既定では、RPC エンドポイント マッピング プロセスは、着信 RPC 要求をポート 135 でリッスンし、登録されたコンポーネント情報をリモート要求に提供します。 リモート要求は、登録済み RPC コンポーネント (MSDTC サービスなど) と通信するために、エンドポイント マッパーによって返される情報を使用できます。 プロセスが Linux 上のよく知られているポート (ポート番号 1024 未満) にバインドするには、スーパーユーザー特権が必要です。 RPC エンドポイント マッパー プロセスのルート権限を使用した SQL Server の起動を回避するには、システム管理者が iptables を使用してネットワーク アドレス変換を作成し、ポート 135 のトラフィックを SQL Server の RPC エンドポイント マッピング プロセスにルーティングするする必要があります。

MSDTC では、mssql-conf ユーティリティ用に次の 2 つの構成パラメーターを使用します。

| mssql-conf setting | [説明] |
|---|---|
| **network.rpcport** | RPC エンドポイント マッパー プロセスのバインド先の TCP ポート。 |
| **distributedtransaction.servertcpport** | MSDTC サーバーがリッスンするポート。 設定しない場合、MSDTC サービスはサービス再起動時にランダムな一時ポートを使用するため、MSDTC サービスが通信を継続できるようにファイアウォールの例外を再構成する必要があります。 |

これらの設定やその他の関連する MSDTC 設定について詳しくは、「[mssql-conf ツールを使用して SQL Server on Linux を構成する](sql-server-linux-configure-mssql-conf.md)」をご覧ください。

## <a name="supported-msdtc-configurations"></a>サポートされている MSDTC 構成

サポートされている MSDTC 構成は次のとおりです。

- ODBC プロバイダーのための SQL Server on Linux に対する OLE-TX 分散トランザクション。

- JDBC および ODBC プロバイダーを使用する SQL Server on Linux に対する XA 分散トランザクション。 XA トランザクションを ODBC プロバイダーを使用して実行するには、Microsoft ODBC Driver for SQL Server バージョン 17.3 以降を使用する必要があります。 詳細については、「[XA トランザクションについて](../connect/jdbc/understanding-xa-transactions.md#configuration-instructions)」を参照してください。

- リンクサーバー上の分散トランザクション。

## <a name="msdtc-configuration-steps"></a>MSDTCの 構成手順

MSDTC の通信と機能を構成するには、3 つの手順を実行します。 必要な構成手順を実行しないと、SQL Server によって MSDTC 機能が有効になりません。

- mssql-conf を使用して **network.rpcport** と **distributedtransaction.servertcpport** を構成します。
- **distributedtransaction.servertcpport** とポート 135 での通信を許可するようにファイアウォールを構成します。
- ポート 135 上の RPC 通信が SQL Server の **network.rpcport** にリダイレクトされるように Linux サーバーのルーティングを構成します。

以下のセクションで各手順について詳しく説明します。

## <a name="configure-rpc-and-msdtc-ports"></a>RPC および MSDTC ポートを構成する

最初に mssql-conf を使用して **network.rpcport** と **distributedtransaction.servertcpport** を構成します。 この手順は、SQL Server に固有であり、サポートされるすべてのディストリビューションで共通しています。

1. mssql-conf を使用して **network.rpcport** 値を設定します。 次の例では 13500 に設定されます。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. **distributedtransaction.servertcpport** 値を設定します。 次の例では 51999 に設定されます。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. SQL Server を再起動してください。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>ファイアウォールの構成

2 番目の手順では、**servertcpport** とポート 135 での通信を許可するようにファイアウォールを構成します。  これにより、RPC エンドポイント マッピング プロセスと MSDTC プロセスが、他のトランザクション マネージャーやコーディネーターと外部で通信できるようになります。 このための実際の手順は、Linux ディストリビューションとファイアウォールによって異なります。 

次の例は、**Ubuntu** でこれらの規則を作成する方法を示しています。

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

次の例は、**Red Hat Enterprise Linux (RHEL)** でこれを行う方法を示しています。

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

次のセクションでポートルーティングを構成する前に、ファイアウォールを構成することが重要です。 場合によっては、ファイアウォールを更新するとポートのルーティング規則がクリアされます。

## <a name="configure-port-routing"></a>ポートのルーティングを構成する

ポート 135 上の RPC 通信が SQL Server の **network.rpcport** にリダイレクトされるように Linux サーバーのルーティング テーブルを構成します。 異なるディストリビューションではポート転送の構成メカニズムが異なる場合があります。 以下のセクションでは、Ubuntu、SUS Enterprise Linux (SLES)、および Red Hat Enterprise Linux (RHEL) に関するガイダンスを提供します。

### <a name="port-routing-in-ubuntu-and-sles"></a>Ubuntu および SLES でのポート ルーティング

Ubuntu と SLES では **firewalld** サービスが使用されないため、ポート ルーティングを実現するには **iptable** 規則が有効なメカニズムです。 **iptable** 規則は再起動時に保持されない可能性があるため、再起動後に規則を復元するように次のコマンドに指示を指定します。

1. ポート 135 のルーティング規則を作成します。 次の例では、ポート 135 は、前のセクションで定義した RPC ポート 13500 に転送されます。 `<ipaddress>` をご使用のサーバーの IP アドレスで置き換えます。

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   前のコマンドの `--comment RpcEndPointMapper` パラメーターは、後のコマンドでこれらの規則を管理する際に役立ちます。

2. 次のコマンドを使用して、作成したルーティング規則を表示します。

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. コンピューター上のファイルにルーティング規則を保存します。

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. 再起動後に規則を再読み込みするには、次のコマンドを `/etc/rc.local` (Ubuntu の場合) または `/etc/init.d/after.local` (SLES の場合) に追加します。

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > **rc.local** ファイルまたは **after.local** ファイルを編集するには、スーパー ユーザー (sudo) 特権が必要です。

**iptables-save** および **iptables-restore** コマンドと `rc.local`/`after.local` スタートアップ構成によって、iptables エントリを保存して復元するための基本的なメカニズムが提供されます。 Linux ディストリビューションによっては、高度な方法つまり自動化された方法を使用できる場合もあります。 たとえば、Ubuntu での代替手段は、エントリを永続化するための **iptables-persistent** パッケージです。

> [!IMPORTANT]
> 前の手順では、固定 IP アドレスが想定されています。 SQL Server インスタンスの IP アドレスが (手動操作または DHCP によって) 変更されると、iptables を使用してルーティング規則を作成していた場合は、削除して再作成する必要があります。 既存のルーティング規則を再作成または削除する必要がある場合、次のコマンドを使用して古い `RpcEndPointMapper` 規則を削除できます。
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>RHEL でのポート ルーティング

Red Hat Enterprise Linux など、**firewalld** サービスを使用する古いディストリビューションでは、サーバー上のポートのオープンと内部ポート転送の両方に同じサービスを使用できます。 たとえば、Red Hat Enterprise Linux では、iptables を使用する代わりに、**firewalld** サービス (**firewall-cmd** 構成ユーティリティに `-add-forward-port` や同様のオプションを指定) を使用して、永続的なポート転送規則を作成および管理する必要があります。

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>Verify (英語の可能性あり)

この時点で、SQL Server は分散トランザクションに参加できるようになっています。 SQL Server がリッスンしていることを確認するには、**netstat** コマンドを実行します (RHEL を使用しているときは、場合によっては最初に **net-tools** パッケージをインストールする必要があります)。

```bash
sudo netstat -tulpn | grep sqlservr
```

次のような出力が表示されます。

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

ただし、再起動後に、SQL Server は最初の分散トランザクションまで **servertcpport** でのリッスンを開始しません。 この場合、最初の分散トランザクションまで、この例のポート 51999 でリッスンしている SQL Server は表示されません。

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>MSDTC のために RPC 通信の認証を構成する

SQL Server on Linux の MSDTC では、既定で RPC 通信で認証が使用されません。 ただし、ホスト マシインが Active Directory (AD) ドメインに参加しているときは、次の **mssql-conf** 設定を使用して認証された RPC 通信を使用するように MSDTC を構成できます。

| 設定 | [説明] |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | 分散トランザクションに対して、セキュリティで保護された RPC のみを構成します。 既定値は 0 です。 |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | 分散トランザクションに対して、セキュリティで保護された RPC のみを構成します。 既定値は 0 です。 |
| **distributedtransaction.turnoffrpcsecurity**               | 分散トランザクションの RPC セキュリティを有効または無効にします。 既定値は 0 です。 |

## <a name="additional-guidance"></a>その他のガイダンス

### <a name="active-directory"></a>Active Directory

SQL Server が Active Directory (AD) 構成に登録されている場合は、RPC が有効になっている MSDTC を使用することをお勧めします。 AD 認証を使用するように SQL Server が構成されている場合、MSDTC は、既定で相互認証 RPC セキュリティを使用します。

### <a name="windows-and-linux"></a>Windows と Linux

Windows オペレーティング システム上のクライアントが SQL Server on Linux での分散トランザクションに参加する必要がある場合は、次のバージョン以上の Windows オペレーティング システムが必要です。

| オペレーティング システム | 最小バージョン | OS ビルド |
|---|---|---|
| [Windows Server](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info) | 1903 | 18362.30.190401-1528 |
| [Windows 10](https://docs.microsoft.com/windows/release-information/) | 1903 | 18362.267 |

## <a name="next-steps"></a>次の手順

SQL Server on Linux について詳しくは、「[SQL Server on Linux](sql-server-linux-overview.md)」をご覧ください。
