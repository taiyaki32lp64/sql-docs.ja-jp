---
title: SQL Server on Linux で RHEL FCI を運用する
description: FCI を手動でフェールオーバーさせたり、クラスターにノードを追加したり、クラスターからノードを削除したりするなど、SQL Server で Red Hat Enterprise Linux (RHEL) 共有ディスクのフェールオーバー クラスター インスタンス (FCI) を運用し、可用性を高める方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 76c59c6c7b821bfcc9eb76ca3a694a1c69095ce1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558527"
---
# <a name="operate-rhel-failover-cluster-instance-fci-for-sql-server"></a>SQL Server の RHEL フェールオーバー クラスター インスタンス (FCI) を運用する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このドキュメントでは、Red Hat Enterprise Linux を使用した共有ディスク フェールオーバー クラスターで SQL Server に対する次のタスクを実行する方法について説明します。

- クラスターを手動でフェールオーバーする
- フェールオーバー クラスターの SQL Server サービスを監視する
- クラスター ノードを追加する
- クラスター ノードを削除する
- SQL Server のリソース監視頻度を変更する

## <a name="architecture-description"></a>アーキテクチャの説明

クラスタリング レイヤーは、[Pacemaker](https://clusterlabs.org/) の上に構築された Red Hat Enterprise Linux (RHEL) [HA アドオン](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)に基づいています。 Corosync と Pacemaker によって、クラスターの通信とリソース管理が調整されます。 SQL Server インスタンスは、一方のノードでのみアクティブになります。

次の図では、SQL Server が含まれる Linux クラスターのコンポーネントが示されています。 

![Red Hat Enterprise Linux 7 共有ディスク SQL クラスター](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

クラスター構成、リソース エージェント オプション、および管理の詳細については、[RHEL リファレンス ドキュメント](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)を参照してください。

## <a name = "failManual"></a>クラスターを手動でフェールオーバーする

`resource move` コマンドでは、ターゲット ノードでリソースを強制的に開始する制約が作成されます。  `move` コマンドを実行した後、リソースの `clear` を実行すると制約が削除されるため、リソースを再び移動したり、リソースを自動的にフェールオーバーしたりできるようになります。 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

次の例では、**mssqlha** リソースを **sqlfcivm2** という名前のノードに移動した後、リソースが別のノードに移動できるように、制約を削除します。  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>フェールオーバー クラスターの SQL Server サービスを監視する

クラスターの現在の状態を表示します。

```bash
sudo pcs status  
```

クラスターとリソースのライブ状態を表示します。

```bash
sudo crm_mon 
```

`/var/log/cluster/corosync.log` にあるリソース エージェント ログを表示します

## <a name="add-a-node-to-a-cluster"></a>クラスターにノードを追加する

1. 各ノードの IP アドレスを確認します。 次のスクリプトを実行すると、現在のノードの IP アドレスが表示されます。 

   ```bash
   ip addr show
   ```

3. 新しいノードには、15 文字以下の一意の名前を指定する必要があります。 Red Hat Linux での既定のコンピューター名は `localhost.localdomain` です。 この既定の名前は一意ではない可能性があり、長すぎます。 新しいノードにコンピューター名を設定します。 コンピューター名は `/etc/hosts` に追加することで設定します。 次のスクリプトを使うと、`vi` で `/etc/hosts` を編集できます。 

   ```bash
   sudo vi /etc/hosts
   ```

   次の例では、`sqlfcivm1`、`sqlfcivm2`、`sqlfcivm3` という名前の 3 つのノードに対する追加が含まれる `/etc/hosts` を示します。

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   ファイルは、すべてのノードで同じである必要があります。 

1. 新しいノードで SQL Server サービスを停止します。

1. 指示に従って、データベース ファイルのディレクトリを共有の場所にマウントします。

   NFS サーバーから、`nfs-utils` をインストールします

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   クライアントと NFS サーバーのファイアウォールを開きます 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   /etc/fstab ファイルを編集して、mount コマンドを追加します。 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   `mount -a` を実行して、変更を有効にします。
   
1. 新しいノードで、Pacemaker のログインのために SQL Server のユーザー名とパスワードを格納するファイルを作成します。 次のコマンドは、このファイルを作成および設定します。

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. 新しいノードで、Pacemaker のファイアウォール ポートを開きます。 `firewalld` を使用してこれらのポートを開くには、次のコマンドを実行します。

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > 組み込みの高可用性構成が備わっていない別のファイアウォールを使用する場合は、Pacemaker 用に次のポートを開き、クラスター内の他のノードと通信できるようにする必要があります
   >
   > * TCP: ポート 2224、3121、21064
   > * UDP: ポート 5405

1. 新しいノードに Pacemaker パッケージをインストールします。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Pacemaker と Corosync のパッケージをインストールしたときに作成された既定のユーザー用のパスワードを設定します。 既存のノードと同じパスワードを使います。 

   ```bash
   sudo passwd hacluster
   ```
 
3. `pcsd` サービスと Pacemaker を有効にし、起動します。 これにより、再起動後に新しいノードはクラスターに再度参加できます。 新しいノードで次のコマンドを実行します。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. SQL Server の FCI リソース エージェントをインストールします。 新しいノードで次のコマンドを実行します。 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. クラスターの既存のノードで、新しいノードを認証し、クラスターに追加します。

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    次の例では、**vm3** という名前のノードがクラスターに追加されます。

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>クラスターからノードを削除する

クラスターからノードを削除するには、次のコマンドを実行します。

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>sqlservr リソースの監視間隔の頻度を変更する

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

次の例では、mssql リソースの監視間隔を 2 秒に設定しています。

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>SQL Server 用の Red Hat Enterprise Linux 共有ディスク クラスターのトラブルシューティングを行う

クラスターのトラブルシューティングでは、3 つのデーモンの連携によってクラスター リソースが管理される方法を理解しておくと役に立つ場合があります。 

| デーモン | [説明] 
| ----- | -----
| Corosync | クラスター ノード間のクォーラム メンバーシップとメッセージングを提供します。
| Pacemaker | Corosync の上に存在し、リソースのステート マシンを提供します。 
| PCSD | `pcs` ツールによって Pacemaker と corosync の両方を管理します

`pcs` ツールを使うには、PCSD が実行されている必要があります。 

### <a name="current-cluster-status"></a>クラスターの現在の状態 

`sudo pcs status` では、各ノードのクラスター、クォーラム、ノード、リソース、デーモンの状態に関する基本情報が返されます。 

Pacemaker での正常なクォーラムの出力の例を次に示します。

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

この例で、`partition with quorum` はノードの過半数のクォーラムがオンラインであることを意味します。 クラスターでノードの過半数のクォーラムが失われると、`pcs status` から `partition WITHOUT quorum` が返され、すべてのリソースが停止されます。 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` では、クラスターに現在参加しているすべてのノードの名前が返されます。 参加していないノードがある場合は、`pcs status` から `OFFLINE: [<nodename>]` が返されます。

`PCSD Status` では、各ノードのクラスターの状態が示されます。

### <a name="reasons-why-a-node-may-be-offline"></a>ノードがオフラインになる理由

ノードがオフラインのときは、次の項目を確認してください。

- **ファイアウォール**

    Pacemaker が通信できるためには、すべてのノードで次のポートが開かれている必要があります。
    
    - **TCP: 2224、3121、21064

- **Pacemaker または Corosync サービスが実行されていること**

- **ノードの通信**

- **ノード名のマッピング**

## <a name="additional-resources"></a>その他のリソース

* Pacemaker の「[一からのクラスター](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)」ガイド

## <a name="next-steps"></a>次のステップ

[SQL Server 用に Red Hat Enterprise Linux 共有ディスクを構成する](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

