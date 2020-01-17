---
title: SQL Server on Linux の RHEL FCI を構成する
description: Red Hat Enterprise Linux (RHEL) 共有ディスクのフェールオーバー クラスター インスタンス (FCI) を構成し、SQL Server on Linux の可用性を高める方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 3ff0c862e93cd3b552b29c4eec8ab91931c809c7
ms.sourcegitcommit: 34d28d49e8d0910cf06efda686e2d73059569bf8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2020
ms.locfileid: "75656629"
---
# <a name="configure-rhel-failover-cluster-instance-fci-cluster-for-sql-server"></a>SQL Server の RHEL フェールオーバー クラスター インスタンス (FCI) クラスターを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このガイドでは、Red Hat Enterprise Linux 上の SQL Server 用に 2 ノードの共有ディスク フェールオーバー クラスターを作成する手順について説明します。 クラスタリング レイヤーは、[Pacemaker](https://clusterlabs.org/) の上に構築された Red Hat Enterprise Linux (RHEL) [HA アドオン](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)に基づいています。 SQL Server インスタンスは、一方のノードでのみアクティブになります。

> [!NOTE] 
> Red Hat HA アドオンとドキュメントにアクセスするには、サブスクリプションが必要です。 

次の図に示すように、2 台のサーバーに対してストレージが提示されます。 クラスタリング コンポーネント (Corosync と Pacemaker) によって、通信とリソース管理が調整されます。 1 台のサーバーで、ストレージ リソースと SQL Server へのアクティブ接続が行われます。 Pacemaker で障害が検出されると、クラスタリング コンポーネントによって他のノードへのリソースの移動が管理されます。  

![Red Hat Enterprise Linux 7 共有ディスク SQL クラスター](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

クラスター構成、リソース エージェント オプション、および管理の詳細については、[RHEL リファレンス ドキュメント](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)を参照してください。


> [!NOTE] 
> 現時点では、Pacemaker との SQL Server の統合は、Windows の WSFC とは結合されていません。 SQL の内部にはクラスターの存在に関する情報はなく、すべての調整は外部で実行され、サービスはスタンドアロン インスタンスとして Pacemaker によって制御されます。 また、たとえば、クラスター DMV の sys.dm_os_cluster_nodes と _os_cluster_properties にはレコードがありません。
IP ではなく、文字列サーバー名をポイントする接続文字列を使用するには、仮想 IP リソースを作成するために使用する IP (以下のセクションで説明します) を、選択したサーバー名と共に DNS サーバーに登録する必要があります。

次のセクションでは、フェールオーバー クラスター ソリューションを設定する手順について説明します。 

## <a name="prerequisites"></a>前提条件

次のエンドツーエンドのシナリオを完了するには、2 つのノード クラスターともう 1 つのサーバーをデプロイして NFS サーバーを構成するために、2 台のマシンが必要です。 以下の手順では、これらのサーバーの構成方法を説明します。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>各クラスター ノードにオペレーティング システムをセットアップして構成する

最初の手順は、クラスター ノード上のオペレーティング システムを構成することです。 このチュートリアルでは、HA アドオンの有効なサブスクリプションで RHEL を使用します。 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>各クラスター ノードに SQL Server をインストールして構成する

1. 両方のノードに SQL Server をインストールしてセットアップします。  詳細については、[SQL Server on Linux のインストール](sql-server-linux-setup.md)に関するページを参照してください。

1. 構成目的の場合は、1 つのノードをプライマリ、もう 1 つをセカンダリとして指定します。 このガイドでは、以降でこれらの用語を使用します。  

1. セカンダリ ノードで SQL Server を停止して無効にします。

   次の例では、SQL Server を停止して無効にしています。 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> セットアップ時に、SQL Server インスタンスのサーバー マスター キーが生成され、`/var/opt/mssql/secrets/machine-key` に配置されます。 Linux では、SQL Server は常に mssql というローカル アカウントとして実行されます。 ローカル アカウントであるため、その ID はノード間で共有されません。 したがって、プライマリ ノードから各セカンダリ ノードに暗号化キーをコピーして、サーバー マスター キーの暗号化を解除するために各ローカル mssql アカウントがそれにアクセスできるようにする必要があります。 

1. プライマリ ノードで、Pacemaker の SQL Server ログインを作成し、`sp_server_diagnostics` を実行するためにログイン権限を付与します。 Pacemaker は、このアカウントを使用して、SQL Server が実行されているノードを確認します。 

   ```bash
   sudo systemctl start mssql-server
   ```

   sa アカウントを使用して SQL Server `master` データベースに接続し、次のように実行します。

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   または、より細かなレベルでアクセス許可を設定することもできます。 Pacemaker ログインでは、sp_server_diagnostics で正常性状態のクエリを実行するための `VIEW SERVER STATE` と、sp_dropserver と sp_addserver を実行することで FCI インスタンス名をリソース名で更新するための `setupadmin` と `ALTER ANY LINKED SERVER` が必要です。 

1. プライマリ ノードで SQL Server を停止して無効にします。 

1. クラスター ノードごとにホスト ファイルを構成します。 ホスト ファイルには、すべてのクラスター ノードの IP アドレスと名前が含まれている必要があります。 

    各ノードの IP アドレスを確認します。 次のスクリプトを実行すると、現在のノードの IP アドレスが表示されます。 

   ```bash
   sudo ip addr show
   ```

   各ノードのコンピューター名を設定します。 各ノードに 15 文字以下の一意の名前を指定します。 コンピューター名は `/etc/hosts` に追加することで設定します。 次のスクリプトを使うと、`vi` で `/etc/hosts` を編集できます。 

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

次のセクションでは、共有ストレージを構成し、データベース ファイルをそのストレージに移動します。 

## <a name="configure-shared-storage-and-move-database-files"></a>共有ストレージを構成し、データベース ファイルを移動する 

共有ストレージを提供するためのさまざまなソリューションが用意されています。 このチュートリアルでは、NFS を使用した共有ストレージの構成について説明します。 ベスト プラクティスに従い、Kerberos を使用して NFS をセキュリティで保護することをお勧めします (例については、 https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/) を参照してください)。 

>[!Warning]
>NFS をセキュリティで保護しない場合、ネットワークにアクセスして SQL ノードの IP アドレスになりすますことができるユーザーが、データ ファイルにアクセスできるようになります。 常に、運用環境で使用する前にシステムの脅威をモデル化するようにしてください。 もう 1 つのストレージ オプションは、SMB ファイル共有を使用することです。

### <a name="configure-shared-storage-with-nfs"></a>NFS を使用して共有ストレージを構成する

> [!IMPORTANT] 
> 4 より小さいバージョンの NFS サーバーでデータベース ファイルをホストすることは、このリリースではサポートされていません。 これには、クラスター化されていないインスタンス上のデータベースだけでなく、共有ディスクのフェールオーバー クラスタリングに NFS を使用することも含まれます。 Microsoft では、今後のリリースでその他の NFS サーバー バージョンを有効化することに取り組んでいます。 

NFS サーバーで、次の操作を行います。

1. `nfs-utils` のインストール

   ```bash
   sudo yum -y install nfs-utils
   ```

1. `rpcbind` を有効にして起動します

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. `nfs-server` を有効にして起動します
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  `/etc/exports` を編集して、共有するディレクトリをエクスポートします。 必要な共有ごとに 1 行が必要です。 次に例を示します。 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 共有をエクスポートします

   ```bash
   sudo exportfs -rav
   ```

1. パスが共有またはエクスポートされていること、NFS サーバーから実行されていることを確認します

   ```bash
   sudo showmount -e
   ```

1. SELinux で例外を追加します

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. サーバーのファイアウォールを開きます。

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 共有ストレージに接続するようにすべてのクラスター ノードを構成する

すべてのクラスター ノードで次の手順を実行します。

1.  `nfs-utils` のインストール

   ```bash
   sudo yum -y install nfs-utils
   ```

1. クライアントと NFS サーバーのファイアウォールを開きます

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. クライアント マシンで NFS 共有が表示されていることを確認します

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. すべてのクラスター ノードでこれらの手順を繰り返します。

NFS の使用の詳細については、次のリソースを参照してください。

* [NFS サーバーと firewalld | Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [NFS ボリュームのマウント | Linux ネットワーク管理者ガイド](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [NFS サーバーの構成 | Red Hat カスタマー ポータル](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>共有ストレージを指すようにデータベース ファイルのディレクトリをマウントする

1.  **プライマリ ノードの場合のみ**、データベース ファイルを一時的な場所に保存します。次のスクリプトでは、新しい一時ディレクトリを作成し、データベース ファイルを新しいディレクトリにコピーして、古いデータベース ファイルを削除します。 SQL Server はローカル ユーザー mssql として実行されるので、マウントされた共有へのデータ転送後に、ローカル ユーザーが共有に読み取り/書き込みアクセスできることを、確認する必要があります。 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  すべてのクラスター ノードで、`/etc/fstab` ファイルを編集して mount コマンドを含めます。  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   次のスクリプトは、この編集の例を示しています。  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>ここで推奨されているようにファイル システム (FS) のリソースを使用する場合は、マウント コマンドを /etc/fstab に保存する必要はありません。 Pacemaker は、FS クラスター化されたリソースを開始するときに、フォルダーのマウントを処理します。 フェンスを使用すると、FS が 2 回マウントされることがなくなります。 

1.  システムの `mount -a` コマンドを実行して、マウントされたパスを更新します。  

1.  `/var/opt/mssql/tmp` に保存したデータベースとログ ファイルを新しくマウントされた共有 `/var/opt/mssql/data` にコピーします。 これは、**プライマリ ノード上**でのみ実行する必要があります。 'mssql ' ローカル ユーザーに必ず読み取り/書き込みアクセス許可を付与してください。

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  SQL Server が新しいファイル パスで正常に起動されることを確認します。 これを各ノードで行います。 この時点では、一度に 1 つのノードだけで SQL Server を実行する必要があります。 両方が同時にデータ ファイルにアクセスしようとするため、両方とも同時に実行することはできません (両方のノードで誤って SQL Server が開始されるのを防ぐために、ファイル システム クラスターのリソースを使用して、共有が異なるノードによって 2 回マウントされていないようにしてください)。 次のコマンドでは、SQL Server が起動され、状態が確認されてから、SQL Server が停止されます。
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
この時点で、SQL Server の両方のインスタンスが、共有ストレージ上のデータベース ファイルを使用して実行されるように構成されています。 次のステップでは、Pacemaker 用に SQL Server を構成します。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>各クラスター ノードに Pacemaker をインストールして構成する


2. 両方のクラスター ノードで、Pacemaker にログインするための SQL Server のユーザー名とパスワードを格納するファイルを作成します。 次のコマンドは、このファイルを作成および設定します。

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 両方のクラスター ノードで、Pacemaker ファイアウォールのポートを開きます。 `firewalld` を使用してこれらのポートを開くには、次のコマンドを実行します。

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

    

2. Pacemaker と Corosync のパッケージをインストールしたときに作成された既定のユーザー用のパスワードを設定します。 両方のノードで同じパスワードを使用します。 

   ```bash
   sudo passwd hacluster
   ```

    

3. `pcsd` サービスと Pacemaker を有効にし、起動します。 これにより、再起動後にノードはクラスターに再度参加できます。 両方のノードで、次のコマンドを実行します。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server の FCI リソース エージェントをインストールします。 両方のノードで、次のコマンドを実行します。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-fencing-agent"></a>フェンス エージェントを構成する

STONITH デバイスでは、フェンス エージェントが提供されます。 「[Azure の Red Hat Enterprise Linux に Pacemaker をセットアップする](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices)」では、Azure でこのクラスター用の STONITH デバイスを作成する方法の例が示されています。 環境の手順を変更します。

## <a name="create-the-cluster"></a>クラスターを作成する 

1. ノードのいずれかで、クラスターを作成します。

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

2. SQL Server、ファイル システム、および仮想 IP リソースのクラスター リソースを構成し、クラスターに構成をプッシュします。 次の情報が必要です。

   - **SQL Server のリソース名**: クラスター化された SQL Server のリソースの名前。 
   - **フローティング IP のリソース名**:仮想 IP アドレスのリソースの名前。
   - **IP アドレス**:SQL Server のクラスター化されたインスタンスに接続するためにクライアントが使用する IP アドレス。 
   - **ファイル システムのリソース名**:ファイル システムのリソースの名前。
   - **デバイス**: NFS 共有パス
   - **デバイス**: 共有へのマウント先を示すローカル パス
   - **fstype**:ファイル共有の種類 (つまり、nfs)

   実際の環境に合わせて、次のスクリプトの値を更新します。 1 つのノードで実行し、クラスター化されたサービスを構成して開始します。  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   たとえば、次のスクリプトは、`mssqlha` という名前の SQL Server クラスター化されたリソースと、IP アドレスが `10.0.0.99` のフローティング IP のリソースを作成します。 また、ファイル システムのリソースを作成し、制約を追加して、すべてのリソースが SQL リソースと同じノードに併置されるようにします。 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   構成がプッシュされると、1 つのノードで SQL Server が起動します。 

3. SQL Server が起動されていることを確認します。 

   ```bash
   sudo pcs status 
   ```

   次の例は、Pacemaker がクラスター化された SQL Server のインスタンスを正常に開始した場合の結果を示しています。 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>その他のリソース

* Pacemaker の「[一からのクラスター](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)」ガイド

## <a name="next-steps"></a>次のステップ

[Red Hat Enterprise Linux 共有ディスク クラスターで SQL Server を操作する](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
