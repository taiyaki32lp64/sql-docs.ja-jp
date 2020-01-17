---
title: iSCSI FCI ストレージの構成 - SQL Server on Linux
description: SQL Server on Linux 用の iSCSI を使用してフェールオーバー クラスター インスタンス (FCI) を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e10f354a8f0af2467a9519a794995043864a4cd6
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558589"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>フェールオーバー クラスター インスタンスの構成 - iSCSI - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上のフェールオーバー クラスター インスタンス (FCI) 用の iSCSI ストレージを構成する方法について説明します。 

## <a name="configure-iscsi"></a>iSCSI の構成 
iSCSI では、ネットワークを使用して、ターゲットと呼ばれるサーバーから、サーバーに対してディスクを提示します。 iSCSI ターゲットに接続しているサーバーでは、iSCSI イニシエーターが構成されている必要があります。 ターゲット上のディスクには、それらにアクセスすべきイニシエーターだけがアクセスできるように、明示的なアクセス許可が付与されています。 そのターゲット自体が、高可用性と信頼性を備えている必要があります。

### <a name="important-iscsi-target-information"></a>iSCSI ターゲットに関する重要な情報
iSCSI ターゲットを構成する方法は、使用するソースの種類に固有のものであるため、このセクションでは説明しませんが、クラスター ノードで使用されるディスクのセキュリティは必ず構成するようにしてください。  

Linux ベースの iSCSI ターゲットを使用する場合は、FCI ノード上でターゲットを構成しないでください。 パフォーマンスと可用性のために、iSCSI ネットワークは、ソース サーバー、クライアント サーバーの両方で通常のネットワーク トラフィックによって使用されるものとは別にする必要があります。 iSCSI 用に使用するネットワークは高速である必要があります。 ネットワークによってプロセッサの帯域幅の一部が消費されることに注意してください。そのため、通常のサーバーを使用する場合はそれに応じて計画を行います。
ターゲット上で完了していることを確認する必要がある、最も重要なことは、FCI に参加しているサーバーのみがアクセスできるよう、作成されるディスクに適切なアクセス許可が割り当てられていることです。 Microsoft iSCSI ターゲットの例を次に示します。ここで linuxnodes1 は作成される名前であり、この場合は、NewFCIDisk1.vhdx にアクセスできるようにノードの IP アドレスが割り当てられています。

![Initiator][1]

### <a name="instructions"></a>Instructions

このセクションでは、FCI のノードとして機能するサーバー上で iSCSI イニシエーターを構成する方法について説明します。 その手順は、RHEL および Ubuntu 上でそのまま使用できるはずです。

サポートされているディストリビューションに向けた iSCSI イニシエーターの詳細については、次のリンクを参照してください。
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  FCI の構成に参加するいずれかのサーバーを選択します。 どれを選んでも問題ありません。 iSCSI は専用ネットワーク上に配置する必要があるため、そのネットワークを認識および使用するように iSCSI を構成します。 `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` を実行します。ここで、`<iSCSIIfaceName>` はネットワークの一意またはフレンドリ名です。 `iSCSINIC` の使用例を次に示します。
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  `/var/lib/iscsi/ifaces/iSCSIIfaceName` を編集します。 次の値が完全に入力されていることを確認します。

    - iface.net_ifacename は、OS に表示されるネットワーク カードの名前です。
    - iface.hwaddress は、以下でこのインターフェイス用に作成される一意の名前の MAC アドレスです。
    - iface.ipaddress
    - iface.subnet_Mask 

    次の例を参照してください。

    ![iSCSITargetSettings][2]

3.  iSCSI ターゲットを検索します。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName> はネットワークの一意/フレンドリ名、\<TargetIPAddress> は iSCSI ターゲットの IP アドレス、\<TargetPort> は iSCSI ターゲットのポートです。 

    ![iSCSITargetResults][3]

 
4.  ターゲットにログインします

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName> はネットワークの一意/フレンドリ名、\<TargetIPAddress> は iSCSI ターゲットの IP アドレスです。

    ![iSCSITargetLogin][4]

5.  iSCSI ターゲットに接続されていることを確認します。

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  iSCSI 接続されたディスクを確認します

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  iSCSI ディスク上に物理ボリュームを作成します。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename> は、前の手順からのデバイスの名前です。 

 
8.  iSCSI ディスク上にボリューム グループを作成します。 1 つのボリューム グループに割り当てられたディスクは、プールまたはコレクションと見なされます。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName> はボリューム グループの名前、\<devicename> は手順 6 のデバイスの名前です。 
 
9.  ディスクの論理ボリュームを作成して確認します。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<size> は作成するボリュームのサイズです。「G」(ギガバイト)、「T」(テラバイト) などを使って指定できます。\<LogicalVolumeName> は論理ボリュームの名前、\<VolumeGroupName> は前の手順のボリューム グループの名前です。 

    次の例では、25 GB のボリュームを作成します。
 
    ![Create25GBVol][10]

10. `sudo lvs` を実行して、作成された LVM を確認します。
 
11. サポートされているファイル システムで論理ボリュームをフォーマットします。 EXT4 の場合は、次の例を使用します。

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName> は、前の手順のボリューム グループの名前です。 \<LogicalVolumeName> は、前の手順の論理ボリュームの名前です。  

12. システム データベース、または既定のデータの場所に格納されているものについては、以下の手順に従います。 それ以外の場合は、手順 13 に進みます。

   *    作業中のサーバーで SQL Server が停止していることを確認します。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    完全にスーパーユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    sudo -i
    ```

   *    mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    su mssql
    ```

   *    SQL Server のデータ ファイルとログ ファイルを格納するための一時ディレクトリを作成します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir> はフォルダーの名前です。 以下の例では、/var/opt/mssql/TempDir という名前のフォルダーを作成します。

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    SQL Server のデータ ファイルとログ ファイルを一時ディレクトリにコピーします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir> は、前の手順で指定したフォルダーの名前です。
    
   *    ファイルがディレクトリ内にあることを確認します。

    ```bash
    ls \<TempDir>
    ```
    \<TempDir> は、手順 d で作成したフォルダーの名前です。

   *    既存の SQL Server データ ディレクトリからファイルを削除します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    ファイルが削除されていることを確認します。 次の図は、c から h までのシーケンス全体の例を示しています。

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    「`exit`」と入力して、ルート ユーザーに切り替えます。

   *    iSCSI 論理ボリュームを SQL Server データ フォルダーにマウントします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName> はボリューム グループの名前、\<LogicalVolumeName> は作成された論理ボリュームの名前です。 次の構文の例は、前のコマンドのボリューム グループと論理ボリュームに一致しています。

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    マウントの所有者を mssql に変更します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    マウントのグループの所有権を mssql に変更します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    su mssql
    ``` 

   *    一時ディレクトリ /var/opt/mssql/data からファイルをコピーします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    ファイルがあることを確認します。

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    「`exit`」と入力して mssql を終了します。
    
   *    「`exit`」と入力してルートを終了します。

   *    SQL Server を起動します。 すべてが正しくコピーされ、セキュリティが正しく適用されている場合、SQL Server は起動済みと表示されます。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    SQL Server を停止し、シャットダウンされていることを確認します。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. ユーザー データベースやバックアップなどのシステム データベース以外のものについては、次の手順に従います。 既定の場所のみを使用する場合は、手順 14 に進みます。

   *    スーパーユーザーになるように切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    sudo -i
    ```

   *    SQL Server によって使用されるフォルダーを作成します。 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName> はフォルダーの名前です。 正しい場所にない場合は、フォルダーの完全なパスを指定する必要があります。 以下の例では、/var/opt/mssql/userdata という名前のフォルダーを作成します。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    前の手順で作成したフォルダーに iSCSI 論理ボリュームをマウントします。 成功した場合は、確認応答を何も受け取りません。
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName> はボリューム グループの名前、\<LogicalVolumeName> は作成された論理ボリュームの名前、\<FolderName> はフォルダーの名前です。 構文の例を次に示します。

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    作成されたフォルダーの所有権を mssql に変更します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName> は、作成されたフォルダーの名前です。 次に例を示します。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    作成されたフォルダーのグループを mssql に変更します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName> は、作成されたフォルダーの名前です。 次に例を示します。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    スーパーユーザーではなくなるよう、「`exit`」と入力します。

   *    テストするには、そのフォルダーにデータベースを作成します。 以下に示す例では、sqlcmd を使用してデータベースを作成し、コンテキストをそれに切り替え、ファイルが OS レベルで存在することを確認した後、一時的な場所を削除します。 SSMS を使用できます。
  
    ![50-ExampleCreateSSMS][9]

   *    共有のマウントを解除します 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName> はボリューム グループの名前、\<LogicalVolumeName> は作成された論理ボリュームの名前、\<FolderName> はフォルダーの名前です。 構文の例を次に示します。

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Pacemaker のみがボリューム グループをアクティブ化できるようにサーバーを構成します。

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. サーバー上のボリューム グループの一覧を生成します。 一覧表示されたもののうち iSCSI ディスクでないものは、システムによって使用されます (OS ディスク用など)。

    ```bash
    sudo vgs
    ```

16. ファイル /etc/lvm/lvm.conf のアクティブ化の構成セクションを変更します。 次の行を構成します。

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker> は、FCI によって使用されない、手順 20 の出力からのボリューム グループの一覧です。 それぞれを引用符で囲み、コンマで区切ります。 次に例を示します。

    ![55-ListOfVGs][11]
 
 
17. Linux が起動すると、ファイル システムがマウントされます。 Pacemaker だけが iSCSI ディスクをマウントできるようにするために、ルート ファイルシステムのイメージをリビルドします。 

    次のコマンドを実行します。完了するまでにしばらく時間がかかる場合があります。 成功した場合、メッセージは返されません。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. サーバーを再起動します。

19. FCI に参加する別のサーバー上で、手順 1-6 を実行します。 これにより、SQL Server に対して iSCSI ターゲットが提示されます。 
 
20. サーバー上のボリューム グループの一覧を生成します。 前に作成したボリューム グループが表示されます。 

    ```bash
    sudo vgs
    ``` 
23. SQL Server を起動し、それがこのサーバー上で起動できることを確認します。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. SQL Server を停止し、それがシャットダウンされていることを確認します。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. FCI に参加するその他のすべてのサーバー上で、手順 1-6 を繰り返します。

これで、FCI を構成する準備が整いました。

|Distribution |トピック 
|----- |-----
|**HA アドオン を含む Red Hat Enterprise Linux** |[構成](sql-server-linux-shared-disk-cluster-configure.md)<br/>[運用](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**HA アドオンを含む SUSE Linux Enterprise Server** |[構成](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>次のステップ

[フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
