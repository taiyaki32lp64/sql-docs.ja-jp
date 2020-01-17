---
title: Active Directory 認証 (Kerberos) の使用
titleSuffix: Azure Data Studio
description: Kerberos で Azure Data Studio に対して Active Directory 認証を使用できるようにする方法について学習します
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8aa4502fca51ef8dc15fceb119297915a64bc682
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957066"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Windows 認証 (Kerberos) を使用して [!INCLUDE[name-sos](../includes/name-sos-short.md)] を SQL Server に接続する 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、Kerberos を使用した SQL Server への接続をサポートします。

macOS または Linux で統合認証 (Windows 認証) を使用するには、現在のユーザーを Windows ドメイン アカウントにリンクする **Kerberos チケット**を設定する必要があります。 

## <a name="prerequisites"></a>前提条件

- Kerberos ドメイン コントローラーのクエリを実行するために、Windows ドメインに参加しているコンピューターへのアクセス権。
- SQL Server は、Kerberos 認証を許可するように構成する必要があります。 UNIX で実行されているクライアント ドライバーでは、統合認証は Kerberos を使用した場合にのみサポートされます。 詳細については、「[Kerberos 統合認証による SQL Server への接続](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)」を参照してください。 接続しようとしている SQL Server の各インスタンスに対して、SPN が登録されている必要があります。 詳細については、「[サービス プリンシパル名の登録](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)」を参照してください。


## <a name="checking-if-sql-server-has-kerberos-setup"></a>SQL Server に Kerberos のセットアップがあるかどうかを確認する

SQL Server のホスト コンピューターにログインします。 Windows コマンドプロンプトで、`setspn -L %COMPUTERNAME%` を使用して、ホストのサービス プリンシパル名をすべて一覧表示します。 MSSQLSvc/HostName.Domain.com で始まるエントリが表示されます。これは、SQL Server で SPN を登録し、Kerberos 認証を受け入れる準備ができていることを意味します。 
- SQL Server のホストにアクセスできない場合は、同じ Active Directory に参加している他の Windows OS から、コマンド `setspn -L <SQLSERVER_NETBIOS>` を使用できます。ここで <SQLSERVER_NETBIOS> は、SQL Server のホストのコンピューター名です。


## <a name="get-the-kerberos-key-distribution-center"></a>Kerberos キー配布センターを取得する

Kerberos KDC (キー配布センター) の構成値を見つけます。 Active Directory ドメインに参加している Windows コンピューターで、次のコマンドを実行します。 

`cmd.exe` を開始して、`nltest` を実行します。

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
必要な KDC 構成値である DC 名をコピーします。この場合は dc-33.domain.company.com です。

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>ご利用の OS を Active Directory ドメイン コントローラーに参加させる

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

AD ドメイン コントローラーの IP アドレスが dns-nameserver として一覧表示されるように、`/etc/network/interfaces` ファイルを編集します。 次に例を示します。 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> ネットワーク インターフェイス (eth0) は、コンピューターによって異なる場合があります。 使用しているものを確認するには、ifconfig を実行し、IP アドレスと送受信されたバイトを持つインターフェイスをコピーします。

このファイルを編集した後、ネットワーク サービスを再起動します。

```bash
sudo ifdown eth0 && sudo ifup eth0
```

次のような行が `/etc/resolv.conf` ファイルに含まれていることを確認します。  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

AD ドメイン コントローラーの IP アドレスが DNS サーバーとして一覧表示されるように、`/etc/sysconfig/network-scripts/ifcfg-eth0` ファイル (または、必要に応じてその他のインターフェイス構成ファイル) を編集します。

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

このファイルを編集した後、ネットワーク サービスを再起動します。

```bash
sudo systemctl restart network
```

次のような行が `/etc/resolv.conf` ファイルに含まれていることを確認します。  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 次の手順に従って、macOS を Active Directory ドメイン コントローラーに参加させます。



## <a name="configure-kdc-in-krb5conf"></a>krb5.conf で KDC を構成する

任意のエディターで `/etc/krb5.conf` を編集します。 次のキーを構成します。

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

次に、krb5.conf ファイルを保存して終了します。

> [!NOTE]
> ドメインはすべて大文字にする必要があります。


## <a name="test-the-ticket-granting-ticket-retrieval"></a>チケット保証チケットの取得をテストする

KDC からチケット保証チケット (TGT) を取得します。

```bash
kinit username@DOMAIN.COMPANY.COM
```

klist を使用して使用可能なチケットを表示します。 klist が正常に実行された場合は、チケットが表示されます。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] を使用して接続する

* 新しい接続プロファイルを作成する

* 認証の種類で **[Windows 認証]** を選択する

* 接続プロファイルを完了し、 **[接続]** をクリックする

接続が正常に行われると、ご利用のサーバーが *[サーバー]* サイドバーに表示されます。
