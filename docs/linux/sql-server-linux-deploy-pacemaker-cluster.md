---
title: SQL Server on Linux 用の Pacemaker クラスターをデプロイする
description: このチュートリアルでは、SQL Server on Linux 用に Pacemaker クラスターをデプロイする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ee3b4aac2e1bcdcc37de17a569f080d3b9bc87cc
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077476"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>SQL Server on Linux 用の Pacemaker クラスターをデプロイする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このチュートリアルでは、。[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On 可用性グループ (AG) またはフェールオーバー クラスター インスタンス (FCI) 用の Linux Pacemaker クラスターをデプロイするために必要なタスクについて説明します。 緊密に結合された Windows Server/ [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] スタックとは異なり、Linux 上の Pacemaker クラスター作成と可用性グループ (AG) 構成は、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] のインストールの前でも後でも行うことができます。 AG または FCI デプロイの Pacemaker 部分のリソースの統合と構成は、クラスターの構成後に行われます。
> [!IMPORTANT]
> クラスター タイプが [なし] の AG では、Pacemaker クラスターは必要 "*なく*"、Pacemaker によって管理することもできません。 

> [!div class="checklist"]
> * 高可用性アドオンをインストールし、Pacemaker をインストールします。
> * Pacemaker のノードを準備します (RHEL および Ubuntu のみ)。
> * Pacemaker クラスターを作成します。
> * SQL Server HA および SQL Server エージェント パッケージをインストールします。
 
## <a name="prerequisite"></a>前提条件
[SQL Server 2017 をインストールします](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>高可用性アドオンをインストールする
次の構文を使用して、Linux の各ディストリビューションの高可用性 (HA) アドオンを構成するパッケージをインストールします。 

**Red Hat Enterprise Linux (RHEL)**
1.  次の構文を使用してサーバーを登録します。 有効なユーザー名とパスワードの入力を求められます。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  登録に使用できるプールを一覧表示します。
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  次のコマンドを実行して、RHEL 高可用性をサブスクリプションに関連付けます。
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    ここで、*PoolId* は前の手順の高可用性サブスクリプションのプール ID です。
    
4.  リポジトリが高可用性アドオンを使用できるようにします。
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Pacemaker をインストールします。
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

YaST に高可用性パターンをインストールするか、サーバーのメイン インストールの一部として実行します。 インストールは、ISO/DVD をソースとして使用することも、オンラインで入手して行うこともできます。
> [!NOTE]
> SLES では、クラスターの作成時に HA アドオンが初期化されます。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Pacemaker のノードを準備する (RHEL および Ubuntu のみ)
Pacemaker そのものは、*hacluster* という名前のディストリビューションに作成されたユーザーを使用します。 このユーザーは、RHEL および Ubuntu に HA アドオンをインストールしたときに作成されます。
1. Pacemaker クラスターのノードとして機能する各サーバーで、クラスターによって使用されるユーザーのパスワードを作成します。 例で使用されている名前は *hacluster* ですが、任意の名前を使用できます。 名前とパスワードは、Pacemaker クラスターに参加するすべてのノードで同じである必要があります。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Pacemaker クラスターの一部となる各ノードで、次のコマンドを使用して `pcsd` サービスを有効にして開始します (RHEL および Ubuntu)。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   次に以下を実行します。
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   これによって `pcsd` が開始されます。
3. Pacemaker クラスターの各ノードで Pacemaker クラスターを有効にします。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   Ubuntu では、次のエラーが表示されます。
   
   *pacemaker Default-Start contains no runlevels, aborting.*
   
   このエラーは既知の問題です。 エラーが発生しても、Pacemaker サービスは正常に有効になっています。このバグは将来のある時点で修正される予定です。
   
4. 次に、Pacemaker クラスターを作成して開始します。 この手順では、RHEL と Ubuntu に違いが 1 つあります。 どちらのディストリビューションでも、`pcs` をインストールすると Pacemaker クラスター用の既定の構成ファイルが構成されますが、RHEL では、このコマンドの実行によって既存の構成が破棄され新しいクラスターが作成されます。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Pacemaker クラスターを作成する 
このセクションでは、Linux の各ディストリビューション用にクラスターを作成して構成する方法について説明します。

**RHEL**

1. ノードを承認する
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   ここで、*NodeX* はノードの名前です。
2. クラスターを作成する
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   ここで、*PMClusterName* は Pacemaker クラスターに割り当てられる名前、*Nodelist* はスペースで区切られたノード名のリストです。

**Ubuntu**

Ubuntu の構成は RHEL に似ています。 ただし、大きな違いが1つあります。Pacemaker パッケージをインストールすると、クラスターの基本構成が作成され、`pcsd` が有効になり、開始されます。 RHEL の手順どおりに Pacemaker クラスターを構成しようとすると、エラーが発生します。 この問題を解決するには、次の手順を実行します。 
1. 各ノードから既定の Pacemaker 構成を削除します。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 「RHEL」セクションの手順に従って、Pacemaker クラスターを作成します。

**SLES**

SLES で Pacemaker クラスターを作成するプロセスは、RHEL と Ubuntu とはまったく異なります。 次の手順では、SLES でクラスターを作成する方法について説明します。
1. ノードの 1 つで以下を実行します。 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   クラスター構成プロセスが開始します。 NTP が構成されておらず、ウォッチドッグ デバイスが見つからないというすメッセージが表示される場合があります。 作業を進めても問題ありません。 ストレージベースの SLES 組み込みフェンスを使用している場合、ウォッチドッグは STONITH に関連しています。 NTP とウォッチドッグは、後で構成できます。
   
2. Corosync を構成するように求められます。 バインド先のネットワーク アドレスの他にマルチキャスト アドレスとポートも要求されます。 ネットワーク アドレスは、使用しているサブネットです (たとえば、192.191.190.0)。 すべてのプロンプトで既定値をそのまま使用することも、必要に応じて変更することもできます。
   
3. 次に、SBD (ディスクベースのフェンス) を構成するかどうかを確認するメッセージが表示されます。 この構成は、必要に応じて後で行うことができます。 SBD が構成されない場合、RHEL と Ubuntu とは異なり、`stonith-enabled` が既定で false に設定されます。
   
4. 最後に、管理用の IP アドレスを構成するかどうかを確認するメッセージが表示されます。 この IP アドレスは省略可能ですが、Windows Server フェールオーバー クラスター (WSFC) の IP アドレスのように機能します。つまり、HA Web Konsole (HAWK) 経由での接続に使用される IP アドレスをクラスター内に作成するという意味です。 この構成も省略可能です。
   
5. 以下を発行して、クラスターが稼働していることを確認します。 
   ```bash
   sudo crm status
   ```
   
6. 次のようにして *hacluster* のパスワードを変更します。 
   ```bash
   sudo passwd hacluster
   ```
   
7. 管理用の IP アドレスを構成した場合は、ブラウザーでテストできます。このとき、*hacluster* のパスワード変更もテストされます。
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. クラスターのノードとなる別の SLES サーバーで、以下を実行します。 
   ```bash
   sudo ha-cluster-join
   ```
   
9. プロンプトが表示されたら、前の手順でクラスターの最初のノードとして構成したサーバーの名前または IP アドレスを入力します。 サーバーが、既存のクラスターにノードとして追加されます。
   
10. 以下を発行してノードが追加されたことを確認します。 
   ```bash
   sudo crm status
   ```
   
11. 次のようにして *hacluster* のパスワードを変更します。 
   ```bash
   sudo passwd hacluster
   ```
   
12. クラスターに追加する他のすべてのサーバーについて、手順 8 - 11 を繰り返します。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>SQL Server HA および SQL Server エージェント パッケージをインストールする
次のコマンドを使用して、SQL Server HA パッケージおよび [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] エージェントをインストールします (まだインストールしていない場合)。 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] をインストールした後で HA パッケージをインストールすると、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] を使用するために再起動が必要になります。 この時点で [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] がインストールされているはずであるため、これらの手順では、Microsoft パッケージのリポジトリが既にセットアップされていることを前提としています。
> [!NOTE]
> - ログ配布またはその他の用途で [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] エージェントを使用する予定がない場合は、インストールする必要がありません。したがって、パッケージ *mssql-server-agent* はスキップできます。
> - [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux 用のその他のパッケージ ([!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] フルテキスト検索 (*mssql-server-fts*) と [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*)) は、FCI と AG のいずれについても、高可用性を確保するうえで必須ではありません。

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>次の手順

このチュートリアルでは、SQL Server on Linux 用に Pacemaker クラスターをデプロイする方法について説明しました。 以下の方法を学習しました。
> [!div class="checklist"]
> * 高可用性アドオンをインストールし、Pacemaker をインストールします。
> * Pacemaker のノードを準備します (RHEL および Ubuntu のみ)。
> * Pacemaker クラスターを作成します。
> * SQL Server HA および SQL Server エージェント パッケージをインストールします。

SQL Server on Linux の可用性グループを作成および構成するには、以下を参照してください。

> [!div class="nextstepaction"]
> [SQL Server on Linux の可用性グループを作成および構成する](sql-server-linux-create-availability-group.md)

