---
title: SQL Server 用に SLES 共有ディスク クラスターを構成する
description: SQL Server 用に SUSE Linux Enterprise Server (SLES) 共有クラスターを構成することにより、高可用性を実現します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 70701d5c0103da089444177db1143066d0c862cd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032224"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>SQL Server 用に SLES 共有ディスク クラスターを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このガイドでは、SUSE Linux Enterprise Server (SLES) 上の SQL Server 用に 2 ノードの共有ディスク クラスターを作成する手順について説明します。 クラスタリング レイヤーは、[Pacemaker](https://clusterlabs.org/) の上に構築された SUSE [High Availability Extension (HAE)](https://www.suse.com/products/highavailability) に基づいています。 

クラスター構成、リソース エージェントのオプション、管理、ベスト プラクティス、推奨事項の詳細については、「[SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

次のエンドツーエンドのシナリオを完了するには、2 ノードのクラスターと別のサーバーを配置して NFS 共有を構成するために、2 台のコンピューターが必要です。 以下の手順では、これらのサーバーの構成方法を説明します。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>各クラスター ノードにオペレーティング システムをセットアップして構成する

最初の手順では、クラスター ノードのオペレーティング システムを構成します。 このチュートリアルでは、HA アドオンの有効なサブスクリプションで SLES を使用します。

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>各クラスター ノードに SQL Server をインストールして構成する

1. 両方のノードに SQL Server をインストールしてセットアップします。 詳細については、[SQL Server on Linux のインストール](sql-server-linux-setup.md)に関するページを参照してください。
2. 構成の目的の場合は、1 つのノードをプライマリ、もう 1 つをセカンダリとして指定します。 このガイドでは、以降でこれらの用語を使用します。 
3. セカンダリ ノードで SQL Server を停止して無効にします。 次の例では、SQL Server を停止して無効にします。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > セットアップ時に、SQL Server インスタンスのサーバー マスター キーが生成され、`/var/opt/mssql/secrets/machine-key` に配置されます。 Linux では、SQL Server は常に mssql というローカル アカウントとして実行されます。 ローカル アカウントであるため、ID はノード間で共有されません。 したがって、プライマリ ノードから各セカンダリ ノードに暗号化キーをコピーして、サーバー マスター キーの暗号化を解除するために各ローカル mssql アカウントがそれにアクセスできるようにする必要があります。
4. プライマリ ノードで、Pacemaker の SQL Server ログインを作成し、`sp_server_diagnostics` を実行するためにログイン権限を付与します。 Pacemaker では、このアカウントを使用して、SQL Server が実行されているノードが確認されます。

    ```bash
    sudo systemctl start mssql-server
    ```
    "sa" アカウントを使用して SQL Server の master データベースに接続し、次のように実行します。

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. プライマリ ノードで SQL Server を停止して無効にします。
6. [SUSE のドキュメント](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html)の手順に従って、各クラスター ノードのホスト ファイルを構成および更新します。 "hosts" ファイルには、すべてのクラスター ノードの IP アドレスと名前が含まれている必要があります。

    現在のノードの IP アドレスを確認するには、次のように実行します。

    ```bash
    sudo ip addr show
    ```

    各ノードにコンピューター名を設定します。 各ノードに 15 文字以下の一意の名前を指定します。 [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) を使って、または[手動](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html)で、`/etc/hostname` にコンピューター名を追加して設定します。

    次の例では、`SLES1` および `SLES2` という名前の 2 つのノードに対する追加が含まれる `/etc/hosts` を示します。

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > すべてのクラスター ノードは、SSH を使用して相互にアクセスできる必要があります。 hb_report or crm_report (トラブルシューティング用) などのツールや Hawk の History Explorer では、ノード間でパスワードなしの SSH アクセスが必要です。それ以外の場合は、現在のノード以外のデータは収集できません。 非標準の SSH ポートを使用する場合は、-X オプションを使用します ([man ページを参照](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html))。 たとえば、SSH ポートが 3479 の場合は、次のコマンドを実行して crm_report を呼び出します。
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >詳細については、「[管理ガイド](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc) 」を参照してください。

次のセクションでは、共有ストレージを構成し、データベース ファイルをそのストレージに移動します。  

## <a name="configure-shared-storage-and-move-database-files"></a>共有ストレージを構成し、データベース ファイルを移動する

共有ストレージを提供するためのさまざまなソリューションが用意されています。 このチュートリアルでは、NFS を使用した共有ストレージの構成について説明します。 ベスト プラクティスに従い、Kerberos を使用して NFS をセキュリティで保護することをお勧めします。 

- [NFS でファイル システムを共有する](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

このガイダンスに従わない場合、ネットワークにアクセスして SQL ノードの IP アドレスになりすますことができるユーザーは、データ ファイルにアクセスできるようになります。 常に、運用環境で使用する前にシステムの脅威をモデル化するようにしてください。 

もう 1 つのストレージ オプションは、SMB ファイル共有を使用することです。

- [SUSE ドキュメントの Samba セクション](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>NFS サーバーを構成する

NFS サーバーを構成するには、SUSE のドキュメントで次の手順を参照してください: [NFS サーバーの構成](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server)。

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 共有ストレージに接続するようにすべてのクラスター ノードを構成する

クライアント NFS を構成して、共有ストレージの場所を指すように SQL Server データベース ファイルのパスをマウントする前に、後で共有にコピーできるように、データベース ファイルを一時的な場所に保存します。

1. **プライマリ ノードでのみ**、データベース ファイルを一時的な場所に保存します。 次のスクリプトでは、新しい一時ディレクトリが作成され、データベース ファイルが新しいディレクトリにコピーされて、古いデータベース ファイルが削除されます。 SQL Server はローカル ユーザー mssql として実行されるので、マウントされた共有へのデータ転送後に、ローカル ユーザーが共有に読み取り/書き込みアクセスできることを、確認する必要があります。 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    すべてのクラスター ノードで NFS クライアントを構成します。

    - [クライアントの構成](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > SUSE のベスト プラクティスと、高可用性 NFS ストレージに関する推奨事項に従うことをお勧めします。[DRBD と Pacemaker による高可用性 NFS ストレージ](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html)。

2. SQL Server が新しいファイル パスで正常に起動されることを確認します。 これを各ノードで行います。 この時点では、一度に 1 つのノードだけで SQL Server を実行する必要があります。 両方が同時にデータ ファイルにアクセスしようとするため、両方とも同時に実行することはできません (両方のノードで誤って SQL Server が起動されるのを防ぐために、ファイル システム クラスター リソースを使用して、共有が異なるノードによって 2 回マウントされないようにします)。 次のコマンドでは、SQL Server が起動され、状態が確認されてから、SQL Server が停止されます。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

この時点で、SQL Server の両方のインスタンスが、共有ストレージ上のデータベース ファイルを使用して実行されるように構成されています。 次のステップでは、Pacemaker 用に SQL Server を構成します。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>各クラスター ノードに Pacemaker をインストールして構成する

1. **両方のクラスター ノードで、Pacemaker にログインするための SQL Server のユーザー名とパスワードを格納するファイルを作成します**。 次のコマンドは、このファイルを作成および設定します。

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **すべてのクラスター ノードは、SSH を使用して相互にアクセスできる必要があります**。 hb_report or crm_report (トラブルシューティング用) などのツールや Hawk の History Explorer では、ノード間でパスワードなしの SSH アクセスが必要です。それ以外の場合は、現在のノード以外のデータは収集できません。 非標準の SSH ポートを使用する場合は、-X オプションを使用します (man ページを参照)。 たとえば、SSH ポートが 3479 の場合は、次のコマンドを実行して hb_report を呼び出します。

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    詳細については、[SUSE ドキュメントのシステム要件と推奨事項](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)をご覧ください。

3. **High Availability Extension をインストールします**。 High Availability Extension をインストールするには、次の SUSE のトピックの手順を実行します。
    
    [インストールとセットアップのクイック スタート](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **SQL Server の FCI リソース エージェントをインストールします**。 両方のノードで、次のコマンドを実行します。

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **最初のノードが自動的にセットアップされます**。 次の手順では、最初のノードである SLES1 を構成することにより、動作中の 1 ノード クラスターをセットアップします。 SUSE のトピック「[Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) (最初のノードのセットアップ)」の指示に従ってください。

    完了したら、`crm status` を使用してクラスターの状態を確認します。
    ```bash
    crm status
    ```

    ノード SLES1 が構成済みであることが表示されます。

6. **既存のクラスターにノードを追加します**。 次に、ノード SLES2 をクラスターに参加させます。 SUSE のトピック「[Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) (2 番目のノードの追加)」の指示に従います。
    
    完了したら、**crm status** を使用してクラスターの状態を確認します。 2 番目のノードが正常に追加されると、次のような出力が表示されます。
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** は、最初の 1 ノード クラスターのセットアップ時に構成された仮想 IP クラスターのリソースです。

7.  **削除手順**。 クラスターからノードを削除する必要がある場合は、ブートストラップ スクリプト **ha-cluster-remove** を使用します。 詳細については、「[Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap) (ブートストラップ スクリプトの概要)」をご覧ください。  

## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server 用にクラスター リソースを構成する

次の手順では、SQL Server 用にクラスター リソースを構成する方法について説明します。 カスタマイズする必要のある設定が 2 つあります。

- **SQL Server のリソース名**: クラスター化された SQL Server のリソースの名前。 
- **タイムアウト値**: タイムアウト値は、リソースがオンラインになるまでクラスターが待機する時間です。 SQL Server の場合、これは SQL Server によって `master` データベースがオンラインにされるまでにかかることが予想される時間です。 

実際の環境に合わせて、次のスクリプトの値を更新します。 1 つのノードで実行し、クラスター化されたサービスを構成して開始します。

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

たとえば、次のスクリプトでは、mssqlha という名前のクラスター化された SQL Server リソースが作成されます。 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

構成がコミットされた後、仮想 IP リソースと同じノードで SQL Server が起動されます。 

詳細については、「[クラスター リソースの構成と管理 (コマンド ライン)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)」を参照してください。 

### <a name="verify-that-sql-server-is-started"></a>SQL Server が起動されていることを確認します。 

SQL Server が起動されたことを確認するには、**crm status** コマンドを実行します。

```bash
crm status
```

次の例では、クラスター化されたリソースが Pacemaker によって正常に開始されたときの結果が示されています。 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>クラスター リソースの管理

クラスター リソースの管理については、次の SUSE トピックを参照してください: [クラスター リソースの管理](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>手動フェールオーバー (manual failover)

リソースはハードウェアまたはソフトウェアの障害が発生した場合にクラスターの他のノードに自動的にフェールオーバー (または移行) するように構成されていますが、Pacemaker の GUI またはコマンド ラインを使って、手動でクラスター内の別のノードにリソースを移動することもできます。 

このタスクには migrate コマンドを使います。 たとえば、SQL リソースをクラスター ノード名 SLES2 に移行するには、以下を実行します。 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>その他のリソース

[SUSE Linux Enterprise High Availability Extension - 管理ガイド](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
