---
title: Linux デプロイでの SQL Server の高可用性
description: Always On 可用性グループ、フェールオーバー クラスター インスタンス (FCI)、ログ配布など、SQL Server on Linux で利用できるさまざまな高可用性オプションについて説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 474533a69d74512e3e305f44d96f90009aa64e00
ms.sourcegitcommit: 34d28d49e8d0910cf06efda686e2d73059569bf8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2020
ms.locfileid: "75656611"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux デプロイでの SQL Server 可用性の基本

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 以降では、Linux と Windows の両方で [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] がサポートされています。 Windows ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイと同様に、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] のデータベースとインスタンスは、Linux 下でも高可用性を備えている必要があります。 この記事では、高可用性を備えた Linux ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] データベースとインスタンスを計画し、デプロイするうえでの技術的な側面について説明すると共に、Windows ベースのインストールとの違いについて説明します。 Linux プロフェッショナルは [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] について聞き慣れなかったり、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] プロフェッショナルは Linux について聞き慣れない場合があるかもしれないため、この記事では、一部のプロフェッショナルにとっては馴染みのある概念についても説明しています。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>Linux デプロイでの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 可用性オプション
バックアップと復元に加えて、Linux では、Windows ベースのデプロイと同じ、3 つの可用性機能を使用できます。
-   Always On 可用性グループ (AG)
-   Always On フェールオーバー クラスター インスタンス (FCI)
-   [ログ配布](sql-server-linux-use-log-shipping.md)

Windows の場合、FCI には常に基になる Windows Server フェールオーバー クラスター (WSFC) が必要です。 デプロイ シナリオによっては、AG には通常、基になる WSFC が必要になります (ただし、[!INCLUDE[sssql17-md](../includes/sssql17-md.md)] の新しい None バリアントは例外です)。 WSFC は Linux には存在しません。 Linux でのクラスタリングの実装については、「[Linux で Always On 可用性グループとフェールオーバー クラスター インスタンスを使用するための Pacemaker](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)」セクションで説明されています。

## <a name="a-quick-linux-primer"></a>Linux についてのクイック ガイド
一部の Linux インストールはインターフェイスを使用してインストールされる場合がありますが、ほとんどの場合はそうではありません。つまり、オペレーティング システム レイヤーでは、ほとんどすべてがコマンド ラインを使用して実行されます。 Linux の世界では、このコマンド ラインを指す一般的な用語は "*bash シェル*" です。

Linux では、多くのコマンドを昇格された特権で実行する必要があります。これは、Windows Server で多くの操作を管理者として実行する必要があるのと似ています。 昇格された特権で実行するには、主に次の 2 つの方法があります。
1. 適切なユーザーのコンテキストで実行します。 別のユーザーに変更するには、`su` コマンドを使用します。 `su` をユーザー名なしで単独で実行した場合、パスワードがわかっていれば、"*ルート*" としてシェルに入ることになります。
   
2. より一般的な、セキュリティを意識した方法で実行するには、操作を実行する前に `sudo` を使用することをお勧めします。 この記事の多くの例では、`sudo` を使用しています。

次に示すのは、いくつかの一般的なコマンドです。これらについては、さまざまなスイッチやオプションをオンラインで調べることができます。
-   `cd` - ディレクトリを変更します
-   `chmod` - ファイルまたはディレクトリのアクセス許可を変更します
-   `chown` - ファイルまたはディレクトリの所有者を変更します
-   `ls` - ディレクトリの内容を表示します
-   `mkdir` - ドライブにフォルダー (ディレクトリ) を作成します
-   `mv` - ある場所から別の場所にファイルを移動します
-   `ps` - 処理中のプロセスをすべて表示します
-   `rm` - ファイルをサーバー上でローカルに削除します
-   `rmdir` - フォルダー (ディレクトリ) を削除します
-   `systemctl` - サービスを開始、停止、または有効化します
-   テキスト エディター コマンド。 Linux には、vi や emacs など、さまざまなテキスト エディター オプションがあります。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Linux 上の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の可用性構成に関する一般的なタスク
このセクションでは、Linux ベースのすべての [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイに共通するタスクについて説明します。

### <a name="ensure-that-files-can-be-copied"></a>ファイルをコピーできることを確認する
あるサーバーから別のサーバーへのファイルのコピーは、Linux で [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] を使用するすべてのユーザーが実行できる必要があるタスクです。 このタスクは、AG の構成にとって非常に重要です。

アクセス許可の問題などは、Windows ベースのインストールだけでなく、Linux にも存在する可能性があります。 ただし、Windows 上のサーバー間でのコピー方法に慣れているユーザーは、Linux での実行方法についてはよく知らない場合もあるでしょう。 一般的な方法は、コマンドライン ユーティリティ `scp` (セキュリティで保護されたコピーを意味します) を使用することです。 `scp` では、バックグラウンドで OpenSSH が使用されます。 SSH は、セキュリティで保護されたシェルを意味します。 Linux ディストリビューションによっては、OpenSSH 自体はインストールされない場合もあります。 その場合は、最初に OpenSSH をインストールする必要があります。 OpenSSH の構成の詳細については、各ディストリビューションに関する次のリンクを参照してください。
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

`scp` を使用する際には、サーバーが転送元または転送先ではない場合に、サーバーの資格情報を指定する必要があります。 たとえば、

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

を使用すると、MyAGCert.cer ファイルが、もう一方のサーバー上の指定されたフォルダーにコピーされます。 コピーするには、ファイルのアクセス許可 (および場合によっては所有権) を持っている必要があることに注意してください。そのため、コピーする前に `chown` も使用しなければならない場合があります。 同様に、受信側では、アクセス権を持った適切なユーザーがファイルを操作する必要があります。 たとえば、証明書ファイルを復元するには、`mssql` のユーザーがそのファイルにアクセスできる必要があります。

サーバー メッセージ ブロック (SMB) の Linux バリアントである Samba を使用して、UNC パス (`\\SERVERNAME\SHARE` など) によってアクセスされる共有を作成することもできます。 Samba の構成の詳細については、各ディストリビューションに関する次のリンクを参照してください。
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Windows ベースの SMB 共有を使用することもできます。[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] をホストしている Linux サーバー 上で Samba のクライアント部分が適切に構成されていて、共有に適切なアクセス権があれば、SMB 共有が Linux ベースである必要はありません。 混合環境では、これは Linux ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイの既存のインフラストラクチャを利用するための 1 つの方法です。

重要なのは、デプロイされた Samba のバージョンが SMB 3.0 に準拠している必要があるということです。 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)] で SMB サポートが追加されたときには、すべての共有で SMB 3.0 をサポートする必要がありました。 Windows Server ではなく、共有に Samba を使用する場合は、Samba ベースの共有で、SMB 3.1.1 をサポートしている Samba 4.0 以降 (できれば 4.3 以降) を使用する必要があります。 「[SMB3 in Samba](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)」は、SMB と Linux に関する情報源として有用です。

最後に、ネットワーク ファイル システム (NFS) 共有を使用することもできます。 NFS は、Windows ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイでは使用できず、Linux ベースのデプロイでのみ使用できます。

### <a name="configure-the-firewall"></a>ファイアウォールの構成
Windows と同様に、Linux ディストリビューションにはファイアウォールが組み込まれています。 組織のサーバーに外部ファイアウォールが使用されている場合は、Linux でファイアウォールを無効にすることが許容される可能性もあります。 ただし、ファイアウォールがどこで有効になっているかに関係なく、ポートは開いている必要があります。 次の表は、Linux 上の高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイに必要な、一般的なポートを示したものです。

| ポート番号 | 種類     | [説明]                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS - `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (使用されている場合) - End Point Mapper                                                                                          |
| 137         | UDP      | Samba (使用されている場合) - NetBIOS Name Service                                                                                      |
| 138         | UDP      | Samba (使用されている場合) - NetBIOS Datagram                                                                                          |
| 139         | TCP      | Samba (使用されている場合) - NetBIOS Session                                                                                           |
| 445         | TCP      | Samba (使用されている場合) - SMB over TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - 既定のポート。必要に応じて、`mssql-conf set network.tcpport <portnumber>` を使用して変更できます                       |
| 2049        | TCP、UDP | NFS (使用されている場合)                                                                                                               |
| 2224        | TCP      | Pacemaker - `pcsd` によって使用されます                                                                                                |
| 3121        | TCP      | Pacemaker - Pacemaker Remote ノードがある場合に必要です                                                                    |
| 3260        | TCP      | iSCSI Initiator (使用されている場合) - `/etc/iscsi/iscsid.config` (RHEL) で変更できますが、iSCSI Target のポートと一致している必要があります |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - AG エンドポイント用に使用される既定のポート。エンドポイントの作成時に変更できます                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker - マルチキャスト UDP を使用している場合は Corosync で必要になります                                                                     |
| 5405        | UDP      | Pacemaker - Corosync で必要です                                                                                            |
| 21064       | TCP      | Pacemaker - DLM を使用しているリソースで必要になります                                                                                 |
| 変数    | TCP      | AG エンドポイント ポート。既定値は 5022 です                                                                                           |
| 変数    | TCP      | NFS - `LOCKD_TCPPORT` 用のポート (RHEL では `/etc/sysconfig/nfs` にあります)                                              |
| 変数    | UDP      | NFS - `LOCKD_UDPPORT` 用のポート (RHEL では `/etc/sysconfig/nfs` にあります)                                              |
| 変数    | TCP/UDP  | NFS - `MOUNTD_PORT` 用のポート (RHEL では `/etc/sysconfig/nfs` にあります)                                                |
| 変数    | TCP/UDP  | NFS - `STATD_PORT` 用のポート (RHEL では `/etc/sysconfig/nfs` にあります)                                                 |

Samba で使用できるその他のポートについては、「[Samba ポートの使用方法](https://wiki.samba.org/index.php/Samba_Port_Usage)」を参照してください。

逆に、Linux でのサービスの名前を、ポートの代わりに例外として追加することもできます (たとえば、Pacemaker の `high-availability` など)。 このアプローチを採用する場合は、使用するディストリビューションで当該の名前を参照してください。 たとえば、RHEL では、Pacemaker を追加するコマンドは次のようになります

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**ファイアウォールのドキュメント:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>可用性のための [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] パッケージをインストールする
Windows ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] インストールでは、一部のコンポーネントは基本的なエンジンのインストールでもインストールされますが、それ以外はインストールされません。 Linux では、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] エンジンのみがインストール プロセスの一部としてインストールされます。 その他はすべてオプションです。 Linux 下の高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] インスタンスの場合、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] と共に 2 つのパッケージをインストールする必要があります。[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*mssql-server-agent*) と高可用性 (HA) パッケージ (*mssql-server-ha*) です。 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent は厳密にはオプションですが、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] のジョブのスケジューラであり、ログ配布で必要とされるため、インストールすることをお勧めします。 Windows ベースのインストールでは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent はオプションではありません。

>[!NOTE]
>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] に聞き慣れない方のために説明すると、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent は [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の組み込みのジョブ スケジューラです。 これは、DBA がバックアップやその他の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] メンテナンスなどをスケジュール設定するための一般的な方法です。 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent が完全に別のサービスである Windows ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] インストールとは異なり、Linux では、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent は [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 自体のコンテキストで実行されます。

AG または FCI が Windows ベースの構成で構成されている場合、それらはクラスター対応となります。 クラスター対応とは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] で、WSFC によって認識される特定のリソース DLL (FCI の場合は sqagtres.dll と sqsrvres.dll、AG の場合は hadrres.dll) があり、WSFC によってそれが使用されることで、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] のクラスター化機能が稼働し、正常に機能していることが確認されることを意味します。 クラスタリングは [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] にとってだけでなく、Linux 自体にとっても外部的な機能であるため、Microsoft では、Linux ベースの AG デプロイや FCI デプロイのために、リソース DLL に相当するコードを記述する必要がありました。 それが、*mssql-server-ha* パッケージです (Pacemaker 用の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] リソース エージェントとも呼ばれます)。 *mssql-server-ha* パッケージをインストールするには、「[SQL Server HA および SQL Server エージェント パッケージをインストールする](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)」を参照してください。

Linux 上の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 用のその他のパッケージ ([!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] フルテキスト検索 (*mssql-server-fts*) と [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*)) は、FCI と AG のいずれについても、高可用性を確保するうえで必須ではありません。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Linux 上の Always On 可用性グループおよびフェールオーバー クラスター インスタンスのための Pacemaker
前述のように、現在 Microsoft for AG と FCI でサポートされている唯一のクラスタリング メカニズムは、Pacemaker と Corosync です。 このセクションでは、ソリューションについて理解するための基本的な情報と、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 構成を計画およびデプロイする方法について説明します。

### <a name="ha-add-onextension-basics"></a>HA アドオン/拡張機能の基本
現在サポートされているすべてのディストリビューションには、Pacemaker クラスタリング スタックに基づく高可用性アドオン/拡張機能が付属しています。 このスタックには、次の 2 つの主要コンポーネントが組み込まれています。Pacemaker と Corosync。 スタックのすべてのコンポーネントは次のとおりです。
-   Pacemaker - クラスター化されたマシン間の調整などを行うコア クラスタリング コンポーネントです。
-   Corosync - クォーラムなどの機能や、失敗したプロセスを再起動する機能などを提供するフレームワークと API セットです。
-   libQB - ログ記録などを提供します。
-   リソース エージェント - アプリケーションが Pacemaker を統合できるようにするための機能です。
-   フェンス エージェント - ノードを分離し、問題が発生した場合にはそれらに対処できるようにするためのスクリプト/機能です。
    
> [!NOTE]
> クラスター スタックは、Linux の世界では一般に Pacemaker と呼ばれています。

このソリューションは、ある意味では Windows を使用したクラスター化構成のデプロイと似ていますが、異なる点も多くあります。 Windows では、クラスタリングの可用性形式 (Windows Server フェールオーバー クラスター (WSFC)) がオペレーティング システムに組み込まれており、WSFC の作成を可能にする機能 (フェールオーバー クラスタリング) は既定で無効になっています。 Windows では、AG と FCI は WSFC の上に構築されており、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] によって提供される特定のリソース DLL により、緊密な統合が共有されます。 この密結合のソリューションは、1 つのベンダーから提供されているからこそ実現できているとも言えます。

![](./media/sql-server-linux-ha-basics/image1.png)

Linux では、サポートされている各ディストリビューションで Pacemaker を利用できますが、それぞれのディストリビューションでカスタマイズすることができ、実装とバージョンが少し異なる場合があります。 相違点の一部は、この記事の手順に反映されています。 クラスタリング レイヤーはオープンソースであるため、ディストリビューションに付属している場合でも、Windows 下の WSFC と同じ方法で緊密に統合されてはいません。 そのため、Microsoft では *mssql-server-ha* を提供してします。これにより、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] と Pacemaker スタックでも、Windows 下の AG や FCI に近いエクスペリエンスを提供できるようになっています (ただし、完全に同じではありません)。

Pacemaker に関する完全なドキュメント (完全な参照情報を含んだ詳細な説明など) については、RHEL と SLES についてそれぞれ次を参照してください。
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu には、可用性に関するガイドはありません。

スタック全体の詳細については、Clusterlabs サイトにある公式の [Pacemaker ドキュメント ページ](https://clusterlabs.org/doc/)も参照してください。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker の概念と用語
このセクションでは、Pacemaker の実装に関する一般的な概念と用語について説明します。

#### <a name="node"></a>Node
ノードとは、クラスターに参加しているサーバーのことです。 Pacemaker クラスターでは、最大 16 のノードがネイティブにサポートされています。 この数は、Corosync が追加のノードで実行されていなけば超えることもできますが、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] には Corosync が必須です。 したがって、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ベースの構成に対してクラスターで設定できるノードの最大数は 16 になります。これは Pacemaker の制限であり、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] によって課せられる AG または FCI の最大制限とは関係ありません。 

#### <a name="resource"></a>リソース
リソースの概念は、WSFC と Pacemaker のどちらのクラスターにも存在します。 リソースとは、クラスターのコンテキストで実行される特定の機能のことです(ディスクや IP アドレスなど)。 たとえば、Pacemaker では、FCI と AG の両方のリソースを作成できます。 これは、AG の構成時に FCI または AG リソースに対する [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] リソースが表示される WSFC での操作と似ていますが、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] と Pacemaker の統合方法に根本的な違いがあるため、まったく同じではありません。

Pacemaker には、標準リソースとクローン リソースがあります。 クローン リソースとは、すべてのノードで同時に実行されるリソースのことです。 たとえば、負荷分散のために複数のノードで実行される IP アドレスなどがこれに該当します。 FCI 用に作成されたリソースでは、標準リソースが使用されます。これは、FCI は 1 つのノードでしか同時にホストできないためです。

AG を作成する際には、マルチステート リソースと呼ばれる特殊な形式の複製リソースが必要になります。 AG のプライマリ レプリカは 1 つだけですが、AG 自体は、動作元として構成されたすべてのノードで実行され、場合によっては、読み取り専用アクセスなども使用することができます。 これはノードを "ライブで" で使用する手法なので、リソースの状態は、マスターとスレーブという 2 つの概念で表されます。 詳細については、「[多状態のリソース:複数モードのリソース](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)」を参照してください。

#### <a name="resource-groupssets"></a>リソース グループ/セット
WSFC のロールのように、Pacemaker クラスターにはリソース グループという概念があります。 リソース グループ (SLES ではセットと呼ばれます) とは、連携的に機能し、1 つのノードから別のノードにフェールオーバーすることができる、リソースのコレクションのことを指します。 リソース グループには、マスター/スレーブとして構成されたリソースを含めることはできません。したがって、リソース グループは AG には使用できません。 リソース グループは FCI には使用できますが、通常は推奨される構成ではありません。

#### <a name="constraints"></a>制約
WSFC には、リソースに関する各種パラメーターに加え、依存関係などの概念もあります。これにより、2 つの異なるリソース間の親子関係が WSFC に伝えられます。 依存関係とは、どのリソースを最初にオンラインにする必要があるかを WSFC に指示するルールのことです。

Pacemaker クラスターには、依存関係の概念はありませんが、制約という概念があります。 制約には、コロケーション、場所、順序という 3 つの種類があります。
-   コロケーション制約は、2 つのリソースを同じノードで実行する必要があるかどうかを指示するものです。
-   場所制約は、リソースを実行できる (または実行できない) 場所を Pacemaker クラスターに指示するものです。
-   順序制約は、リソースの開始順序を Pacemaker クラスターに指示するものです。

> [!NOTE]
> コロケーション制約は、リソース グループ内のリソースには必要ありません　(すべてのリソースが 1 つの単位として見なされるため)。

#### <a name="quorum-fence-agents-and-stonith"></a>クォーラム、フェンス エージェント、STONITH
Pacemaker のクォーラムは、概念的には WSFC と似ています。 クラスターのクォーラム メカニズムの全体的な目的は、クラスターの稼働状態を維持することです。 Linux ディストリビューション用の WSFC アドオンと HA アドオンには、各ノードがクォーラムに対してカウントされる、投票という概念があります。 投票では、稼働状態のノードが多数を占めるのが理想です。そうでないと、最悪の場合はクラスターがシャット ダウンされます。

WSFC とは異なり、クォーラムでは、連携する監視リソースはありません。 WSFC と同様に、投票ノードの数を奇数に維持することが目標とされます。 クォーラム構成では、AG について、FCI とは異なる考慮事項があります。

WSFC では、参加しているノードの状態が監視され、問題が発生したときにはそれらが処理されます。 新しいバージョンの WSFC では、誤動作しているノードや使用できないノード (ノードがオンになっていない、ネットワーク通信が停止しているなど) を検査する機能などが提供されます。 Linux 側では、この種の機能はフェンス エージェントによって提供されます。 この概念は、"フェンス" と呼ばれることもあります。 ただし、これらのフェンス エージェントは通常、デプロイに固有のものであり、多くの場合、ハードウェア ベンダーや一部のソフトウェア ベンダー (ハイパーバイザーを提供するベンダーなど) によって提供されます。 たとえば、VMware では、vSphere を使用して仮想化された Linux VM 用に使用できるフェンス エージェントが提供されます。

クォーラムとフェンスは、STONITH (Shoot the Other Node in the Head) と呼ばれる別の概念と関連します。 STONITH では、すべての Linux ディストリビューションで Pacemaker クラスターがサポートされていることが要件となります。 詳細については、「[Red Hat High Availability Cluster でのフェンス](https://access.redhat.com/solutions/15575)」を参照してください。

#### <a name="corosyncconf"></a>corosync.conf
この `corosync.conf` ファイルには、クラスターの構成が格納されます。 このファイルは `/etc/corosync` にあります。 通常の日常業務では、クラスターが適切に設定されていれば、このファイルを編集する必要はありません。

#### <a name="cluster-log-location"></a>クラスター ログの場所
Pacemaker クラスターのログの場所は、ディストリビューションによって異なります。
-   RHEL および SLES - `/var/log/cluster/corosync.log`
-   Ubuntu - `/var/log/corosync/corosync.log`

ログの既定の場所を変更するには、`corosync.conf` に変更を加えます。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Pacemaker クラスターを [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 用に計画 する
このセクションでは、Pacemaker クラスターの重要な計画ポイントについて説明します。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Linux ベースの Pacemaker クラスターを [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 用に仮想化する
仮想マシンを使用して Linux ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイを AG と FCI 用にデプロイする際には、Windows ベースの場合と同じ規則が適用されます。 仮想化された [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] デプロイのサポートに関する一連の基本規則は、[Microsoft サポート KB 956893](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment) で公開されています。 Microsoft の Hyper-V や VMware の ESXi など、異なるハイパーバイザー間では、プラットフォーム自体の違いによって異なる規則が生じる場合もあります。

仮想化環境で AG と FCI を使用する場合は、指定された Pacemaker クラスターのノードに対して、アンチアフィニティが設定されていることを確認してください。 AG または FCI の構成で高可用性向けに構成された場合、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] をホストしている各 VM は、同じハイパーバイザー ホストで実行されないようにする必要があります。 たとえば、2 ノードの FCI がデプロイされている場合、特にライブ マイグレーションや vMotion のような機能を使用している場合には、ホストで障害が発生したときに、ノードをホストしている VM のいずれかに対して移行先を確保できるよう、"*少なくとも*" 3 つのハイパーバイザー ホストを確保する必要があります。

詳細については、以下を参照してください。
-   Hyper-V のドキュメント - [高可用性のためのゲスト クラスタリングの使用](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   ホワイトペーパー (Windows ベースのデプロイ向けに記述されていますが、ほとんどの概念が適用されます) - [VMware vSphere を使用したミッション クリティカルな高可用性 SQL Server デプロイの計画](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

### <a name="networking"></a>ネットワーク
WSFC とは異なり、Pacemaker では、Pacemaker クラスター自体に対して専用の名前を付けたり、少なくとも 1 つの専用 IP アドレスを持たせる必要はありません。 AG と FCI には IP アドレスが必要 (詳細については、それぞれのドキュメントを参照してください) ですが、ネットワーク名リソースがないので、名前は必要ありません。 SLES では、管理目的で IP アドレスを構成することができますが、「[Pacemaker クラスターを作成する](sql-server-linux-deploy-pacemaker-cluster.md#create)」で示されているように、必須ではありません。

WSFC と同様に、Pacemaker では冗長ネットワークの使用が推奨されます。つまり、ネットワーク カード (NIC または物理用の pNIC) ごとに個別の IP アドレスを持たせることが推奨されます。 クラスター構成の観点からいうと、各 IP アドレスには、専用のリングと呼ばれるものが使用されます。 ただし、現在の WSFC と同様に、多くの実装は仮想化されたり、パブリック クラウド上に置かれるため、実際にはサーバーに対して 1 つの仮想 NIC (vNIC) しか存在しません。 すべての pNIC と vNIC が同じ物理または仮想スイッチに接続されている場合、ネットワーク層には真の冗長性が確保されないため、複数の NIC を構成することは、仮想マシンにとっては一種の気休めということになります。 ネットワークの冗長性は、通常、仮想化されたデプロイ用にハイパーバイザーに組み込まれており、最終的にパブリック クラウドに組み込まれます。

複数の NIC を Pacemaker で使用する場合と WSFC で使用する場合の違いを 1 つ挙げると、Pacemaker では、同じサブネット上で複数の IP アドレスが許可されますが、WSFC では許可されません。 複数のサブネットと Linux クラスターの詳細については、[複数のサブネットの構成](sql-server-linux-configure-multiple-subnet.md)に関する記事を参照してください。

### <a name="quorum-and-stonith"></a>クォーラムと STONITH
クォーラムの構成と要件は、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の AG または FCI 固有のデプロイに関連します。

サポートされている Pacemaker クラスターには STONITH が必須です。 STONITH を構成するには、ディストリビューションのドキュメントを使用します。 たとえば、SLES の場合なら「[ストレージベースのフェンス](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)」を使用します。 ESXI ベースのソリューションの場合は、VMware vCenter 用の STONITH エージェントもあります。 詳細については、「[VMWare VM VCenter SOAP フェンス向け STONITH プラグイン エージェント (非公式)](https://github.com/olafrv/fence_vmware_soap)」を参照してください。

### <a name="interoperability"></a>相互運用性
このセクションでは、Linux ベースのクラスターで、WSFC や他の Linux ディストリビューションとどのように連携できるかについて説明します。

#### <a name="wsfc"></a>WSFC
現時点では、WSFC と Pacemaker クラスターを連携させる直接的な方法はありません。 つまり、WSFC と Pacemaker をまたいで動作する AG や FCI を作成することはできません。 ただし、2 つの相互運用性ソリューションがあります。これらは、どちらも AG 向けに設計されています。 FCI をクロスプラットフォーム構成に参加させる唯一の方法は、次の 2 つのシナリオのいずれかで、FCI をインスタンスとして参加させる方法です。
-   クラスターの種類が None の AG。 詳細については、Windows の[可用性グループに関するドキュメント](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)を参照してください。
-   分散型 AG。これは、2 つの異なる AG を独自の可用性グループとして構成することができる、特別な種類の可用性グループです。 分散 AG の詳細については、ドキュメント「[分散型可用性グループ](../database-engine/availability-groups/windows/distributed-availability-groups.md)」を参照してください。

#### <a name="other-linux-distributions"></a>他の Linux ディストリビューション
Linux では、Pacemaker クラスターのすべてのノードが同じディストリビューション上に存在している必要があります。 たとえば、RHEL ノードは、SLES ノードを持つ Pacemaker クラスターの一部にすることはできません。 この問題の主な理由は、前に説明したとおりです。つまり、ディストリビューションのバージョンと機能が異なることで、正常に機能しない可能性があるためです。 ディストリビューションの混合については、WSFC と Linux の混合と同じ条件が適用されます。つまり、None または 分散型 AG を使用してください。

## <a name="next-steps"></a>次のステップ
[SQL Server on Linux 用の Pacemaker クラスターをデプロイする](sql-server-linux-deploy-pacemaker-cluster.md)
