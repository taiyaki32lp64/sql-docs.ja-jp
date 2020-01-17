---
title: フェールオーバー クラスター インスタンス - SQL Server on Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 81d283ba02ec62a2de8d3c8f0e56be8c55d58190
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032392"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>フェールオーバー クラスター インスタンス - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上の SQL Server フェールオーバー クラスター インスタンス (FCI) に関連する概念について説明します。 

Linux 上に SQL Server FCI を作成するには、[Linux 上の SQL Server FCI の構成](sql-server-linux-shared-disk-cluster-configure.md)に関する記事を参照してください。

## <a name="the-clustering-layer"></a>クラスタリング レイヤー

* RHEL では、クラスタリング レイヤーは Red Hat Enterprise Linux (RHEL) [HA アドオン](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)に基づいています。 

    > [!NOTE] 
    > Red Hat HA アドオンとドキュメントにアクセスするには、サブスクリプションが必要です。 

* SLES では、クラスタリング レイヤーは、SUSE Linux Enterprise [High Availability Extension (HAE)](https://www.suse.com/products/highavailability) に基づいています。

    クラスター構成、リソース エージェントのオプション、管理、ベスト プラクティス、および推奨事項の詳細については、「[SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)」を参照してください。

RHEL HA アドオンと SUSE HAE は、どちらも [Pacemaker](https://clusterlabs.org/) 上に構築されます。

次の図に示すように、2 台のサーバーに対してストレージが提示されます。 クラスタリング コンポーネント (Corosync と Pacemaker) によって、通信とリソース管理が調整されます。 1 台のサーバーで、ストレージ リソースと SQL Server へのアクティブ接続が行われます。 Pacemaker で障害が検出されると、クラスタリング コンポーネントによって、他のノードへのリソースの移動が管理されます。  

![Red Hat Enterprise Linux 7 共有ディスク SQL クラスター](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 現時点では、Linux 上の SQL Server と Pacemaker の統合では、Windows 上の WSFC のような連携は行われていません。 SQL の内部にはクラスターの存在に関する情報はなく、すべての調整は外部で実行され、サービスはスタンドアロン インスタンスとして Pacemaker によって制御されます。 さらに、仮想ネットワーク名は WSFC に固有のものであり、Pacemaker にはそれに該当するものはありません。 @@servername と sys.servers によってノード名が返され、クラスター dmvs の sys.dm_os_cluster_nodes と sys.dm_os_cluster_properties にはレコードがないと想定されています。 IP ではなく、文字列サーバー名をポイントする接続文字列を使用するには、仮想 IP リソースを作成するために使用する IP (以下のセクションで説明します) を、選択したサーバー名と共に DNS サーバーに登録する必要があります。

## <a name="number-of-instances-and-nodes"></a>インスタンスとノードの数

SQL Server on Linux での重要な違いの 1 つは、Linux サーバーごとにインストールできる SQL Server は 1 台だけであるということです。 そのインストールをインスタンスと呼びます。 つまり、Windows Server フェールオーバー クラスター (WSFC) ごとに最大 25 の FCI がサポートされる Windows Server とは異なり、Linux ベースの FCI には、インスタンスが 1 つだけ存在します。 この 1 つのインスタンスは、既定のインスタンスでもあります。Linux には、名前付きインスタンスという概念はありません。 

Corosync が関与している場合、Pacemaker クラスターには最大 16 個のノードを含めることができるので、1 つの FCI は最大 16 台のサーバーにまたがることができます。 Standard Edition の SQL Server で実装された FCI では、Pacemaker クラスターに最大 16 個のノードがある場合でも、1 つのクラスターで最大 2 個のノードがサポートされます。

SQL Server FCI では、SQL Server インスタンスは、片方のノードでのみアクティブになります。

## <a name="ip-address-and-name"></a>IP アドレスと名前
Linux Pacemaker クラスターでは、各 SQL Server FCI に固有の IP アドレスと名前が必要です。 FCI 構成が複数のサブネットにまたがっている場合は、サブネットごとに 1 つの IP アドレスが必要です。 FCI へのアクセスでは、Pacemaker クラスターの基になるサーバーをアプリケーションとエンドユーザーが認識する必要がないように、一意の名前と IP アドレスが使用されます。

DNS 内の FCI の名前は、Pacemaker クラスター内に作成される FCI リソースの名前と同じである必要があります。
名前と IP アドレスの両方を DNS に登録する必要があります。

## <a name="shared-storage"></a>ストレージの共有
すべての FCI は、Linux サーバー上にあるか Windows Server 上にあるかにかかわらず、何らかの形式の共有ストレージを必要とします。 このストレージが FCI をホストできる可能性があるすべてのサーバーに提示されますが、FCI のためにこのストレージを使用できるのは常に 1 台のサーバーだけです。 Linux 上で使用できる共有ストレージのオプションを次に示します。

- iSCSI
- Network File System (NFS)
- Windows Server のサーバー メッセージ ブロック (SMB)。わずかに異なるオプションがあります。 Linux ベースの FCI で現在サポートされていないオプションの 1 つとして、SQL Server の一時ワークスペースである TempDB 用のノードに対してローカルなディスクを使用する機能があります。

複数の場所にまたがる構成では、片方のデータ センターに格納されるものを他方のデータ センターと同期する必要があります。 フェールオーバーが発生した場合、FCI をオンラインにすることができ、ストレージは同じものであることが認識されます。 これを実現するには、ストレージ レプリケーションのための外部的な方法が必要であり、基になるストレージ ハードウェアによって実行されるか、何らかのソフトウェアベースのユーティリティによって実行されます。 

>[!NOTE]
>SQL Server では、ディスクを使用してサーバーに直接提示される Linux ベースのデプロイは、XFS または EXT4 でフォーマットする必要があります。 それ以外のファイル システムは現在サポートされていません。 すべての変更はここに反映されます。

共有ストレージを提示するためのプロセスは、サポートされている他の方法と同じです。

- 共有ストレージを構成する
- FCI 用の Pacemaker クラスターのノードとして機能するサーバーに、ストレージをフォルダーとしてマウントする
- 必要に応じて、SQL Server システム データベースを共有ストレージに移動する
- 共有ストレージに接続されている各サーバーから SQL Server が動作することをテストする

SQL Server on Linux での主要な違いの 1 つは、既定のユーザー データとログ ファイルの場所は構成することはできますが、システム データベースは常に `/var/opt/mssql/data` に存在する必要があるということです。 Windows Server では、TempDB を含めて、システム データベースを移動することができます。 この事実は、FCI 用に共有ストレージをどのように構成するかに関係します。

システム以外のデータベースの既定のパスを、`mssql-conf` ユーティリティを使用して変更できます。 既定値を変更する方法の詳細については、[既定のデータまたはログ ディレクトリの場所の変更](sql-server-linux-configure-mssql-conf.md#datadir)に関する記事を参照してください。 適切なセキュリティが設定されている限り、既定の場所以外の場所に SQL Server のデータとトランザクションを格納することもできますが、その場所を明示する必要があります。

次のトピックで、Linux ベースの SQL Server FCI でサポートされている種類のストレージを構成する方法について説明しています。

- [フェールオーバー クラスター インスタンスの構成 - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [フェールオーバー クラスター インスタンスの構成 - NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [フェールオーバー クラスター インスタンスの構成 - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
