---
title: FCI の構成 - SQL Server on Linux (RHEL)
description: SQL Server 用の Red Hat Enterprise Linux (RHEL) でフェールオーバー クラスター インスタンス (FCI) を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 61fe5d7ffb5dfc6ec98f6d5350eff396deaa0312
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558327"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server の 2 ノード共有ディスクによるフェールオーバー クラスター インスタンスによって、高可用性のためのサーバーレベルの冗長性が提供されます。 このチュートリアルでは、SQL Server on Linux の 2 ノード フェールオーバー クラスター インスタンスを作成する方法について説明します。 実行する具体的な手順は次のとおりです。

> [!div class="checklist"]
> * Linux を設定および構成する
> * SQL Server をインストールして構成する
> * hosts ファイルを構成する
> * 共有ストレージを構成してデータベース ファイルを移動する
> * 各クラスター ノードに Pacemaker をインストールして構成する
> * フェールオーバー クラスター インスタンスを構成する

この記事では、SQL Server の 2 ノード共有ディスクによるフェールオーバー クラスター インスタンス (FCI) を作成する方法について説明します。 この記事には、Red Hat Enterprise Linux (RHEL) 用の手順とスクリプト例が記載されています。 Ubuntu ディストリビューションは RHEL と似ているため、通常、このスクリプト例は Ubuntu 上でも動作します。 

概念については、[Linux での SQL Server フェールオーバー クラスター インスタンス (FCI)](sql-server-linux-shared-disk-cluster-concepts.md) に関する記事をご覧ください。

## <a name="prerequisites"></a>前提条件

以下のエンドツーエンドのシナリオを完了するには、2 ノードのクラスターとストレージ用の別のサーバーを配置するために、2 台のコンピューターが必要です。 以下の手順では、これらのサーバーの構成方法を説明します。

## <a name="set-up-and-configure-linux"></a>Linux を設定および構成する

最初の手順は、クラスター ノード上のオペレーティング システムを構成することです。 クラスター内の各ノード上で、linux ディストリビューションを構成します。 両方のノードで同じディストリビューションとバージョンを使用します。 次のディストリビューションのどちらか一方だけを使用します。
    
* HA アドオン用の有効なサブスクリプションを備えた RHEL

## <a name="install-and-configure-sql-server"></a>SQL Server をインストールして構成する

1. 両方のノードに SQL Server をインストールして設定します。  詳細については、[SQL Server on Linux のインストール](sql-server-linux-setup.md)に関するページを参照してください。
1. 構成目的の場合は、1 つのノードをプライマリ、もう 1 つをセカンダリとして指定します。 このガイドでは、以降でこれらの用語を使用します。  
1. セカンダリ ノードで SQL Server を停止して無効にします。
    次の例では、SQL Server を停止して無効にしています。 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 設定時に、SQL Server インスタンスのサーバー マスター キーが生成され、`var/opt/mssql/secrets/machine-key` に配置されます。 Linux では、SQL Server は常に mssql というローカル アカウントとして実行されます。 ローカル アカウントであるため、その ID はノード間で共有されません。 したがって、プライマリ ノードから各セカンダリ ノードに暗号化キーをコピーして、サーバー マスター キーの暗号化を解除するために各ローカル mssql アカウントがそれにアクセスできるようにする必要があります。 

1.  プライマリ ノードで、Pacemaker の SQL Server ログインを作成し、`sp_server_diagnostics` を実行するためにログイン権限を付与します。 Pacemaker は、このアカウントを使用して、SQL Server が実行されているノードを確認します。 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   sa アカウントを使用して SQL Server `master` データベースに接続し、次のように実行します。

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   または、より細かなレベルでアクセス許可を設定することもできます。 Pacemaker ログインでは、sp_server_diagnostics で正常性状態を照会するための `VIEW SERVER STATE` と、sp_dropserver と sp_addserver を実行することで FCI インスタンス名をリソース名で更新するための `setupadmin` と `ALTER ANY LINKED SERVER` が必要です。 

1. プライマリ ノードで SQL Server を停止して無効にします。 

## <a name="configure-the-hosts-file"></a>hosts ファイルを構成する

各クラスター ノード上で hosts ファイルを構成します。 hosts ファイルには、すべてのクラスター ノードの IP アドレスと名前が含まれている必要があります。

1. 各ノードの IP アドレスを確認します。 次のスクリプトを実行すると、現在のノードの IP アドレスが表示されます。 

    ```bash
    sudo ip addr show
    ```

1. 各ノードのコンピューター名を設定します。 各ノードに 15 文字以下の一意の名前を指定します。 コンピューター名は `/etc/hosts` に追加することで設定します。 次のスクリプトを使うと、`vi` で `/etc/hosts` を編集できます。 

   ```bash
   sudo vi /etc/hosts
   ```
   次の例では、`sqlfcivm1` および `sqlfcivm2` という名前の 2 つのノードが追加された `/etc/hosts` を示します。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>ストレージの構成とデータベース ファイルの移動  

両方のノードがアクセスできるストレージを用意する必要があります。 iSCSI、NFS、または SMB を使用できます。 ストレージを構成し、そのストレージをクラスター ノード用に指定した後、データベース ファイルをその新しいストレージに移動します。 次の記事では、ストレージの種類ごとの手順について説明します。

- [フェールオーバー クラスター インスタンスの構成 - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [フェールオーバー クラスター インスタンスの構成 - NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [フェールオーバー クラスター インスタンスの構成 - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>各クラスター ノードに Pacemaker をインストールして構成する

1. 両方のクラスター ノードで、Pacemaker にログインするための SQL Server のユーザー名とパスワードを格納するファイルを作成します。 

    次のコマンドは、このファイルを作成および設定します。

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. 両方のクラスター ノードで、Pacemaker ファイアウォールのポートを開きます。 `firewalld` を使用してこれらのポートを開くには、次のコマンドを実行します。

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 組み込みの高可用性構成が備わっていない別のファイアウォールを使用する場合は、Pacemaker 用に次のポートを開き、クラスター内の他のノードと通信できるようにする必要があります
   >
   > * TCP: ポート 2224、3121、21064
   > * UDP: ポート 5405

1. 各ノードに Pacemaker パッケージをインストールします。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
1. Pacemaker と Corosync のパッケージをインストールしたときに作成された既定のユーザー用のパスワードを設定します。 両方のノードで同じパスワードを使用します。 

   ```bash
   sudo passwd hacluster
   ```
1. `pcsd` サービスと Pacemaker を有効にし、起動します。 これにより、再起動後にノードはクラスターに再度参加できます。 両方のノードで、次のコマンドを実行します。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. SQL Server の FCI リソース エージェントをインストールします。 両方のノードで、次のコマンドを実行します。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>フェールオーバー クラスター インスタンスを構成する

FCI はリソース グループ内に作成されます。 リソース グループによって制約の必要性が軽減されるため、この方が少し簡単になります。 ただし、リソースは、起動させる順番でリソース グループに追加する必要があります。 起動させる順番は次のとおりです。 

1. ストレージ リソース
2. ネットワーク リソース
3. アプリケーション リソース

この例では、グループ NewLinFCIGrp 内に FCI を作成します。 リソース グループの名前は、Pacemaker で作成されるすべてのリソースに対して一意である必要があります。

1.  ディスク リソースを作成します。 問題がなければ、応答は返されません。 ディスク リソースを作成する方法は、ストレージの種類によって異なります。 ストレージの種類ごとの例を以下に示します。 ご自分のクラスター記憶域のストレージの種類に適用される例をお使いください。

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName> は、iSCSI ディスクに関連付けられるリソースの名前です

    \<VolumeGroupName> はボリューム グループの名前です  

    \<LogicalVolumeName> は、作成された論理ボリュームの名前です  

    \<FolderToMountiSCSIDIsk> はディスクをマウントするフォルダーです (システム データベースと既定の場所の場合は、/var/opt/mssql/data になります)

    \<FileSystemType> は EXT4 または XFS になります。これは、書式設定を行う方法と、ディストリビューションが何をサポートするかによって異なります。 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName> は、NFS 共有に関連付けられるリソースの名前です

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです

    \<FolderOnNFSServer> は、NFS 共有の名前です

    \<FolderToMountNFSShare> はディスクをマウントするフォルダーです (システム データベースと既定の場所の場合は、/var/opt/mssql/data になります)

    次に 1 つの例を示します。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName> は、SMB 共有を使用するサーバーの名前です

    \<ShareName> は共有の名前です

    \<FolderName> は、最後の手順で作成したフォルダーの名前です
    
    \<UserName> は、共有にアクセスするユーザーの名前です

    \<Password> はユーザーのパスワードです

    \<ADDomain> は AD DS ドメインです (Windows Server ベースの SMB 共有を使用する場合に適用します)

    \<mssqlUID> は mssql ユーザーの UID です

    \<mssqlGID> は mssql ユーザーの GID です

    \<RGName> はリソース グループの名前です
 
2.  FCI によって使用される IP アドレスを作成します。 問題がなければ、応答は返されません。

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName> は、IP アドレスに関連付けられるリソースの名前です

    \<IPAddress> は FCI の IP アドレスです

    \<NetworkCard> はサブネットに関連付けられているネットワーク カードです (つまり eth0)

    \<NetMask> はサブネットのネットマスクです (つまり 24)

    \<RGName> はリソース グループの名前です
 
3.  FCI リソースを作成します。 問題がなければ、応答は返されません。

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName> は、リソースの名前であるだけでなく、FCI に関連付けられるフレンドリ名でもあります。 ユーザーとアプリケーションはこれを使って接続を行います。 

    \<RGName> はリソース グループの名前です。
 
4.  コマンド `sudo pcs resource` を実行します。 FCI はオンラインである必要があります。
 
5.  FCI の DNS/リソース名を使用して、SSMS または sqlcmd で FCI に接続します。

6.  ステートメント `SELECT @@SERVERNAME` を発行します。 FCI の名前が返されます。

7.  ステートメント `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')` を発行します。 FCI が実行されているノードの名前が返されます。

8.  FCI を、他のノードに手動でフェールオーバーします。 「[フェールオーバー クラスター インスタンスの操作 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)」に記載されている手順をご覧ください。

9.  最後に、FCI を元のノードにフェールバックし、コロケーション制約を削除します。

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>まとめ

このチュートリアルでは、以下のタスクを完了しました。

> [!div class="checklist"]
> * Linux を設定および構成する
> * SQL Server をインストールして構成する
> * hosts ファイルを構成する
> * 共有ストレージを構成してデータベース ファイルを移動する
> * 各クラスター ノードに Pacemaker をインストールして構成する
> * フェールオーバー クラスター インスタンスを構成する

## <a name="next-steps"></a>次のステップ

- [フェールオーバー クラスター インスタンスの操作 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
