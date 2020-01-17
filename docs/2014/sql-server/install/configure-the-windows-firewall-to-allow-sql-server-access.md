---
title: SQL Server のアクセスを許可するための Windows ファイアウォールの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall ports
- WMI firewall ports
- Windows Firewall [Database Engine]
- firewall systems, configuring
- advfirewall
- firewall systems
- rules firewall
- firewall systems, overview and port list
- 1433 TCP port
- portopening using netsh
- ports [SQL Server], TCP
- netsh to open firewall ports
ms.assetid: f55c6a0e-b6bd-4803-b51a-f3a419803024
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5dcbf0aae9c96e788fdbf9544114d226fa8f0bfd
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637854"
---
# <a name="configure-the-windows-firewall-to-allow-sql-server-access"></a>SQL Server のアクセスを許可するための Windows ファイアウォールの構成
  ファイアウォール システムは、コンピューター リソースへの不正アクセスを防ぐのに役立ちます。 ファイアウォールがオンになっているが、正しく構成されていない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続の試行がブロックされる可能性があります。  
  
 ファイアウォールを経由して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアクセスするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターで、アクセスを許可するようにファイアウォールを構成する必要があります。 ファイアウォールは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のコンポーネントです。 他社製のファイアウォール プログラムをインストールすることもできます。 このトピックでは、Windows ファイアウォールを構成する方法について説明しますが、基本的な原則は他のファイアウォール プログラムにも適用されます。  
  
> [!NOTE]  
>  このトピックでは、ファイアウォール構成の概要について説明し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者を対象とした情報がまとめられています。 ファイアウォールの詳細および管理ファイアウォール情報については、「 [セキュリティが強化された Windows ファイアウォールの設計ガイド](https://go.microsoft.com/fwlink/?LinkID=116904)」などのファイアウォールのマニュアルを参照してください。  
  
 コントロール パネルの **[Windows ファイアウォール]** と、セキュリティが強化された Windows ファイアウォールの Microsoft 管理コンソール (MMC) スナップインの操作に慣れているユーザーや、どのファイアウォール設定を構成するかがわかっているユーザーは、次の一覧にあるトピックに直接進んでください。  
  
-   [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../../../2014/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  

  
##  <a name="BKMK_basic"></a> ファイアウォールに関する基本情報  
 ファイアウォールは、受信パケットを調べて一連のルールと比較することによって機能します。 ルールでパケットの使用が許可されている場合、パケットはファイアウォールを通過して TCP/IP プロトコルに渡され、さらに処理が行われます。 ルールでパケットの使用が許可されていない場合は、ファイアウォールでパケットが破棄され、ログ記録が有効になっている場合は、ファイアウォール ログ ファイルにエントリが作成されます。  
  
 次のいずれかの方法で、許可されたトラフィックの一覧が追加されます。  
  
-   ファイアウォールが有効になっているコンピューターで通信が開始されると、それに対する応答が許可されるようにファイアウォールによって一覧内にエントリが作成されます。 受信した応答は、要請されたトラフィックと見なされるので、この応答を構成する必要はありません。  
  
-   管理者がファイアウォールの例外を構成します。 これにより、コンピューターで実行されている指定したプログラムへのアクセス、またはコンピューター上の指定した接続ポートへのアクセスが許可されます。 この場合、サーバー、リスナー、またはピアとして機能しているコンピューターは、要請されていない受信トラフィックを受け入れます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するには、この種類の構成を完了している必要があります。  
  
 ファイアウォール戦略の選択は、特定のポートを開くか閉じるかを単に決定するよりも複雑です。 企業に合ったファイアウォール戦略を策定するときは、必ず使用できるすべてのルールと構成オプションについて検討してください。 このトピックでは、可能なファイアウォール オプションすべてを検討するわけではありません。 次のドキュメントを確認することをお勧めします。  
  
 [セキュリティが強化された Windows ファイアウォール ファースト ステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=116080)  
  
 [セキュリティが強化された Windows ファイアウォールの設計ガイド](https://go.microsoft.com/fwlink/?LinkId=116904)  
  
 [サーバーとドメインの分離の概要](https://go.microsoft.com/fwlink/?LinkId=116081)  
  
##  <a name="BKMK_default"></a> 既定のファイアウォール設定  
 ファイアウォール構成を計画するには、まずオペレーティング システムのファイアウォールについて現在の状態を確認します。 オペレーティング システムが前のバージョンからアップグレードされた場合、以前のファイアウォール設定が維持されている可能性があります。 また、他の管理者やドメイン内のグループ ポリシーによってファイアウォール設定が変更された可能性もあります。  
  
> [!NOTE]  
>  ファイアウォールをオンにすると、ファイルとプリンターの共有やリモート デスクトップ接続など、このコンピューターにアクセスする他のプログラムに影響を与えます。 管理者はファイアウォール設定を調整する前に、コンピューターで実行されているすべてのアプリケーションについて検討する必要があります。  
  
##  <a name="BKMK_programs"></a> ファイアウォールを構成するためのプログラム  
 Windows ファイアウォールの設定を構成するには、次の 3 つの方法があります。  
  
-   **コントロール パネルの [Windows ファイアウォール]**  
  
     **[Windows ファイアウォール]** は、コントロール パネルから開くことができます。  
  
    > [!IMPORTANT]  
    >  コントロール パネルの **[Windows ファイアウォール]** で行った変更は、現在のプロファイルにのみ影響を与えます。 ラップトップなどのモバイル デバイスでは、別の設定で接続されるときにプロファイルが変更される可能性があるので、コントロール パネルの **[Windows ファイアウォール]** は使用しないでください。 以前に構成されたプロファイルには影響を及ぼしません。 プロファイルの詳細については、「 [セキュリティが強化された Windows ファイアウォール ファースト ステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=116080)」を参照してください。  
  
     コントロール パネルの **[Windows ファイアウォール]** で基本的なオプションを構成できます。 その一部を次に示します。  
  
    -   コントロール パネルの **[Windows ファイアウォール]** のオンとオフを切り替える  
  
    -   ルールを有効または無効にする  
  
    -   ポートおよびプログラムの例外を許可する  
  
    -   一部のスコープの制限を設定する  
  
     コントロール パネルの **[Windows ファイアウォール]** は、ファイアウォールの構成に慣れていないユーザーや、モバイル デバイスでないコンピューターに基本的なファイアウォール オプションを構成するユーザーに最適です。 次の手順に従って、`run` コマンドからコントロールパネルの **[Windows ファイアウォール]** を開くこともできます。  
  
    #### <a name="to-open-the-windows-firewall-item"></a>[Windows ファイアウォール] を開くには  
  
    1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして、「 `firewall.cpl`」と入力します。  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
-   **Microsoft 管理コンソール (MMC)**  
  
     セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、詳細なファイアウォール設定を構成できます。 このスナップインは、ほとんどのファイアウォール オプションが使いやすい形式で表示され、すべてのファイアウォール プロファイルが提供されます。 詳細については、後の「 [セキュリティが強化された Windows ファイアウォールのスナップインの使用](#BKMK_WF_msc) 」を参照してください。  
  
-   **netsh**  
  
     **netsh.exe** ツールを使用して、管理者はコマンド プロンプトまたはバッチ ファイルで Windows ベースのコンピューターの構成および監視を行うことができます **。** **netsh** ツールを使用すれば、入力したコンテキスト コマンドを適切なヘルパーに渡し、ヘルパーによってコマンドを実行できます。 ヘルパーは、1 つ以上のサービス、ユーティリティ、またはプロトコルの構成、監視、サポートを行って **netsh** ツールの機能を拡張するダイナミック リンク ライブラリ (.dll) ファイルです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートしているすべてのオペレーティング システムには、ファイアウォール ヘルパーが組み込まれています。 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] には、 **advfirewall**という高度なファイアウォール ヘルパーも組み込まれています。 **netsh** の使用方法の詳細については、このトピックでは説明しません。 ただし、このトピックで説明する構成オプションの多くは、 **netsh**を使用して構成できます。 たとえば、コマンド プロンプトで次のスクリプトを実行すると、TCP ポート 1433 を開くことができます。  
  
    ```  
    netsh firewall set portopening protocol = TCP port = 1433 name = SQLPort mode = ENABLE scope = SUBNET profile = CURRENT  
    ```  
  
     セキュリティを強化するための Windows ファイアウォール ヘルパーを使用した同様の例  
  
    ```  
    netsh advfirewall firewall add rule name = SQLPort dir = in protocol = tcp action = allow localport = 1433 remoteip = localsubnet profile = DOMAIN  
    ```  
  
     **netsh**の詳細については、次のリンクを参照してください。  
  
    -   [Netsh.exe ツールとコマンド ライン スイッチの使用方法](https://support.microsoft.com/kb/242468)  
  
    -   ["netsh firewall" コンテキストの代わりに "netsh advfirewall firewall" コンテキストを使用して、Windows Server 2008 および Windows Vista で Windows ファイアウォールの動作を制御する方法](https://support.microsoft.com/kb/947709)  
  
    -   ["profile=all" パラメーターと共に "netsh firewall" コマンドを使用しても、Windows Vista ベースのコンピューターでパブリック プロファイルが構成されない](https://support.microsoft.com/kb/947213)  
  
## <a name="ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>で使用されるポート [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 次の表で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用されるポートを確認できます。  
  
###  <a name="BKMK_ssde"></a> Ports Used By the Database Engine  
 次の表に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]で頻繁に使用されるポートの一覧を示します。  
  
|Scenario|[ポート]|コメント|  
|--------------|----------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンス|TCP ポート 1433|これは、ファイアウォールを通過することを許可されている最も一般的なポートです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインストール、またはコンピューターで実行中の唯一のインスタンスである名前付きインスタンスへの、通常の接続に適用されます (名前付きインスタンスには注意事項があります。 後の「 [動的ポート](#BKMK_dynamic_ports) 」を参照してください。)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名前付きインスタンス|TCP ポートは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の起動時に決定される動的ポートです。|後の「 [動的ポート](#BKMK_dynamic_ports)」の説明を参照してください。 名前付きインスタンスを使用している場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスで UDP ポート 1434 が必要になる可能性があります。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名前付きインスタンス|管理者が構成するポート番号|後の「 [動的ポート](#BKMK_dynamic_ports)」の説明を参照してください。|  
|専用管理者接続|TCP ポート 1434 (既定のインスタンスに使用)。 その他のポートは名前付きインスタンスに使用されます。 ポート番号については、エラー ログを確認してください。|既定では、専用管理者接続 (DAC) へのリモート接続は有効になっていません。 リモート DAC を有効にするには、セキュリティ構成ファセットを使用します。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス|UDP ポート 1434|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスは、名前付きインスタンスへの着信接続をリッスンし、その名前付きインスタンスに対応する TCP ポート番号をクライアントに提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスが使用されている場合は、通常 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Browser サービスを開始します。 名前付きインスタンスの特定のポートに接続するようにクライアントが構成されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを開始する必要はありません。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス|HTTP エンドポイントの作成時に指定できます。 既定の TCP ポートは、CLEAR_PORT トラフィックでは 80、SSL_PORT トラフィックでは 443 です。|URL を使用した HTTP 接続に使用されます。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンス|TCP ポート 443|URL を使用した HTTPS 接続に使用されます。 HTTPS は、Secure Sockets Layer (SSL) を使用した HTTP 接続です。|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|TCP ポート 4022。 使用されるポートを確認するには、次のクエリを実行します。<br /><br /> `SELECT name, protocol_desc, port, state_desc`<br /><br /> `FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'SERVICE_BROKER'`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSB](../../includes/sssb-md.md)]の既定のポートはありませんが、これがオンライン ブックの例で使用される通常の構成です。|  
|データベース ミラーリング|管理者が選択したポート。 ポートを特定するには、次のクエリを実行します。<br /><br /> `SELECT name, protocol_desc, port, state_desc FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'DATABASE_MIRRORING'`|データベース ミラーリング用の既定のポートはありませんが、オンライン ブックの例では TCP ポート 7022 が使用されています。 特に自動フェールオーバーを伴う高い安全性モードでは、使用中のミラーリング エンドポイントが中断しないようにすることはきわめて重要です。 ファイアウォール構成によりクォーラムが分割されないようにする必要があります。 詳細については、「 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)を使用します。|  
|レプリケーション|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのレプリケーション接続では、一般的な正規の [!INCLUDE[ssDE](../../includes/ssde-md.md)] ポートを使用します (既定のインスタンスに使用される TCP ポート 1433 など)。<br /><br /> レプリケーション スナップショットのための Web 同期と FTP/UNC アクセスには、ファイアウォール上で追加のポートを開く必要があります。 ある場所から別の場所に初期データおよびスキーマを転送するために、レプリケーションでは FTP (TCP ポート 21)、HTTP (TCP ポート 80) を使用した同期、またはファイル共有を使用できます。 ファイル共有では、NetBIOS を使用する場合、UDP ポート 137 と 138、および TCP ポート 139 を使用します。 ファイル共有は TCP ポート 445 を使用します。|HTTP を使用した同期のために、レプリケーションでは IIS エンドポイント (既定ではポート 80 だが構成可能) を使用しますが、IIS プロセスは標準のポート (既定のインスタンスの場合は 1433) を使用してバックエンドの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します。<br /><br /> FTP を使用した Web 同期時は、サブスクライバーと IIS の間ではなく、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 発行者と IIS の間で FTP 転送が行われます。|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガー|TCP ポート 135<br /><br /> 「 [ポート 135 に関する注意事項](#BKMK_port_135)」を参照してください。<br /><br /> [IPsec](#BKMK_additional_ports) の例外が必要な場合もあります。|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ホスト コンピューターで [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を使用している場合は、 **Devenv.exe** を例外リストに追加し、TCP ポート 135 を開く必要もあります。<br /><br /> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ホスト コンピューターで [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用している場合は、 **ssms.exe** を例外リストに追加し、TCP ポート 135 を開く必要もあります。 詳細については、「 [Transact-sql デバッガーの構成](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)」を参照してください。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]で Windows ファイアウォールを構成する詳細な手順については、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」を参照してください。  
  
####  <a name="BKMK_dynamic_ports"></a> 動的ポート  
 既定では、名前付きインスタンス ( [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を含む) では動的ポートを使用します。 したがって、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が起動するたびに使用可能なポートが特定され、そのポート番号が使用されます。 インストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが名前付きインスタンスのみの場合、通常は TCP ポート 1433 が使用されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の他のインスタンスがインストールされている場合は、別の TCP ポートが使用される可能性が高くなります。 選択されたポートは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が起動するたびに変わる可能性があるので、正しいポート番号にアクセスできるようにファイアウォールを構成することは容易ではありません。 したがって、ファイアウォールを使用する場合は、毎回同じポート番号を使用するように [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再構成することをお勧めします。 このポートを固定ポートまたは静的なポートと呼びます。 詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
 固定ポートでリッスンするように名前付きインスタンスを構成する代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlservr.exe **(** ) などの [!INCLUDE[ssDE](../../includes/ssde-md.md)]プログラムを対象としてファイアウォールで例外を作成することもできます。 この方法が有効な場合もありますが、セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用しているときは、 **[受信の規則]** ページの **[ローカル ポート]** 列にポート番号が表示されません。 そのため、どのポートが開いているかを調べるのが難しくなる可能性があります。 もう 1 つの注意事項は、Service Pack または累積された更新によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 実行可能ファイルへのパスが変更され、ファイアウォールのルールが無効になる可能性があるということです。  
  
> [!NOTE]  
>  次の手順では、コントロール パネルの **[Windows ファイアウォール]** を使用します。 セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、より複雑なルールを構成できます。 その場合は、サービスの例外の設定も行います。これは、多層防御を実装する場合に有効です。 後の「 [セキュリティが強化された Windows ファイアウォールのスナップインの使用](#BKMK_WF_msc) 」を参照してください。  
  
###### <a name="to-add-a-program-exception-to-the-firewall-using-the-windows-firewall-item-in-control-panel"></a>コントロール パネルの [Windows ファイアウォール] を使用して、ファイアウォールにプログラムの例外を追加するには  
  
1.  コントロール パネルの **[Windows ファイアウォール]** の **[例外]** タブをクリックし、 **[プログラムの追加]** をクリックします。  
  
2.  ファイアウォール経由で許可する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの場所を参照します。たとえば、 **C:\Program Server\MSSQL12. < instance_name > \MSSQL\Binn**、sqlservr.exe を選択し、[開く] をクリックし**ます。** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 エンドポイントの詳細については、「[複数の TCP ポートでリッスンするデータベース エンジンの構成](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)」と「[エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql)」を参照してください。  
  
###  <a name="BKMK_ssas"></a> Analysis Services で使用されるポート  
 次の表に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で頻繁に使用されるポートの一覧を示します。  
  
|機能|[ポート]|コメント|  
|-------------|----------|--------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|TCP ポート 2383 (既定のインスタンスに使用)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の既定のインスタンスに使用される標準ポートです。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス|TCP ポート 2382 ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の名前付きインスタンスにのみ必要)|ポート番号を指定せずに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の名前付きインスタンスに対してクライアントが接続要求を行うと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser がリッスンするポート 2382 が指定されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、名前付きインスタンスが使用するポートに要求をリダイレクトします。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] IIS/HTTP 経由で使用するように構成された<br /><br /> (PivotTable? サービスは HTTP または HTTPS を使用します)|TCP ポート 80|URL を使用した HTTP 接続に使用されます。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] IIS/HTTPS 経由で使用するように構成された<br /><br /> (PivotTable? サービスは HTTP または HTTPS を使用します)|TCP ポート 443|URL を使用した HTTPS 接続に使用されます。 HTTPS は、Secure Sockets Layer (SSL) を使用した HTTP 接続です。|  
  
 ユーザーが IIS やインターネットを経由して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] にアクセスする場合は、IIS がリッスンするポートを開き、クライアントの接続文字列にそのポートを指定する必要があります。 この場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に直接アクセスするためのポートを開く必要はありません。 必要のない他のすべてのポートと共に、既定のポート 2389 およびポート 2382 を制限する必要があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で Windows ファイアウォールを構成する詳細な手順については、「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../../../2014/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)」を参照してください。  
  
###  <a name="BKMK_ssrs"></a> Reporting Services で使用されるポート  
 次の表に、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で頻繁に使用されるポートの一覧を示します。  
  
|機能|[ポート]|コメント|  
|-------------|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web サービス|TCP ポート 80|URL を使用した [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] への HTTP 接続に使用されます。 **[World Wide Web サービス (HTTP)]** のあらかじめ構成されたルールは使用しないことをお勧めします。 詳細については、後の「 [その他のファイアウォール ルールの操作](#BKMK_other_rules) 」を参照してください。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] HTTPS 経由で使用するように構成された|TCP ポート 443|URL を使用した HTTPS 接続に使用されます。 HTTPS は、Secure Sockets Layer (SSL) を使用した HTTP 接続です。 **[セキュア World Wide Web サービス (HTTPS)]** のあらかじめ構成されたルールは使用しないことをお勧めします。 詳細については、後の「 [その他のファイアウォール ルールの操作](#BKMK_other_rules) 」を参照してください。|  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] から [!INCLUDE[ssDE](../../includes/ssde-md.md)] または [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続する場合、そのサービス用の適切なポートを開く必要もあります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で Windows ファイアウォールを構成する詳細な手順については、「 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)」を参照してください。  
  
###  <a name="BKMK_ssis"></a> Integration Services で使用されるポート  
 次の表に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスで使用されるポートの一覧を示します。  
  
|機能|[ポート]|コメント|  
|-------------|----------|--------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] リモート プロシージャ呼び出し (MS RPC)<br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムで使用されます。|TCP ポート 135<br /><br /> 「 [ポート 135 に関する注意事項](#BKMK_port_135)」を参照してください。|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスでは、ポート 135 で DCOM を使用します。 サービス コントロール マネージャーではポート 135 を使用して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの開始と停止、実行中のサービスに対する制御要求の転送などのタスクを実行します。 ポート番号を変更することはできません。<br /><br /> このポートは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] またはカスタム アプリケーションから [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] サービスのリモート インスタンスに接続する場合にのみ、開く必要があります。|  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]で Windows ファイアウォールを構成する詳細な手順については、「 [SSIS サービスにアクセスするように Windows ファイアウォールを構成する](../../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)」を参照してください。  
  
###  <a name="BKMK_additional_ports"></a> 追加のポートとサービス  
 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が依存している可能性があるポートとサービスの一覧を示します。  
  
|Scenario|[ポート]|コメント|  
|--------------|----------|--------------|  
|Windows Management Instrumentation (Windows Management Instrumentation)<br /><br /> WMI の詳細については、「 [WMI Provider for Configuration Management Concepts](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)」を参照してください。|WMI は、DCOM によってポートが割り当てられている共有サービス ホストの一部として実行されます。 WMI では TCP ポート 135 を使用している可能性があります。<br /><br /> 「 [ポート 135 に関する注意事項](#BKMK_port_135)」を参照してください。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、WMI を使用してサービスの一覧を表示し、管理します。 **[Windows Management Instrumentation (WMI)]** のあらかじめ構成されたルール グループを使用することをお勧めします。 詳細については、後の「 [その他のファイアウォール ルールの操作](#BKMK_other_rules) 」を参照してください。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC)|TCP ポート 135<br /><br /> 「 [ポート 135 に関する注意事項](#BKMK_port_135)」を参照してください。|アプリケーションで分散トランザクションを使用する場合は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トラフィックが、各 MS DTC インスタンス間、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などのリソース マネージャーと MS DTC との間を流れるように、ファイアウォールを構成することが必要になる可能性があります。 **[分散トランザクション コーディネーター]** のあらかじめ構成されたルール グループを使用することをお勧めします。<br /><br /> 個別のリソース グループのクラスター全体に対して 1 つの共有 MS DTC が構成されている場合は、ファイアウォールに sqlservr.exe を例外として追加する必要があります。|  
|[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の参照ボタンを押すと、UDP を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスに接続できます。 詳細については、「[SQL Server Browser サービス &#40;データベース エンジンと SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)」を参照してください。参照してください。|UDP ポート 1434|UDP はコネクションレスのプロトコルです。<br /><br /> ファイアウォールには、 [INetFwProfile インターフェイスの UnicastResponsesToMulticastBroadcastDisabled プロパティ](https://go.microsoft.com/fwlink/?LinkId=118371) という設定があります。この設定は、ブロードキャスト (またはマルチキャスト) UDP 要求へのユニキャスト応答に関するファイアウォールの動作を制御します。  この設定には次の 2 つの動作があります。<br /><br /> 設定が TRUE の場合、ブロードキャスト要求へのユニキャスト応答はまったく許可されません。 サービスの列挙は失敗します。<br /><br /> 設定が FALSE (既定) の場合、ユニキャスト応答が 3 秒間許可されます。 この時間の長さは構成できません。 混雑しているネットワークや待機時間の長いネットワークまたは負荷の大きいサーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを列挙しようとすると、一覧の一部しか返されない可能性があり、ユーザーの混乱を招くことがあります。|  
|IPsec トラフィック|UDP ポート 500 および UDP ポート 4500|ドメインのポリシーにより IPsec 経由でネットワーク通信を行う必要がある場合は、UDP ポート 4500 と UDP ポート 500 も例外の一覧に追加する必要があります。 IPsec は、Windows ファイアウォール スナップインの **新規の受信の規則ウィザード** を使用するオプションです。 詳細については、後の「 [セキュリティが強化された Windows ファイアウォールのスナップインの使用](#BKMK_WF_msc) 」を参照してください。|  
|信頼されたドメインでの Windows 認証の使用|認証要求を許可するようにファイアウォールを構成する必要があります。|詳細については、「 [ドメインの信頼関係を使用するためのファイアウォールの構成方法](https://support.microsoft.com/kb/179442/)」を参照してください。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と Windows のクラスタリング|クラスタリングでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に直接関連付けられていない追加のポートが必要です。|詳細については、「 [クラスターで使用するネットワークを有効にする](https://go.microsoft.com/fwlink/?LinkId=118372)」を参照してください。|  
|HTTP サーバー API (HTTP.SYS) で予約された URL 名前空間|通常は TCP ポート 80 を使用しますが、他のポートに構成することもできます。 一般的な情報については、「 [HTTP および HTTPS の構成](https://go.microsoft.com/fwlink/?LinkId=118373)」を参照してください。|HttpCfg.exe を使用した HTTP.SYS エンドポイントの予約に関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の情報については、「[URL の予約と登録について &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)」を参照してください。|  
  
##  <a name="BKMK_port_135"></a> ポート 135 に関する注意事項  
 RPC と共にトランスポートとして TCP/IP または UDP/IP を使用する場合、必要に応じて受信ポートがシステム サービスに動的に割り当てられることがよくあります。ポート 1024 より大きい TCP/IP ポートや UDP/IP ポートが使用されます。 これらはしばしば "ランダム RPC ポート" と呼ばれます。 これらの場合、RPC クライアントは RPC エンドポイント マッパーを使用して、サーバーにどの動的ポートが割り当てられたかを指示します。 RPC ベースのサービスによっては、RPC によってポートが動的に割り当てられるのではなく、ユーザーが特定のポートを構成できます。 サービスに関係なく、RPC によって動的に割り当てられるポートを狭い範囲に制限することもできます。 ポート 135 は多くのサービスで使用されるので、悪意のあるユーザーによって頻繁に攻撃されます。 ポート 135 を開く場合は、ファイアウォール ルールのスコープを制限することを検討してください。  
  
 ポート 135 の詳細については、次の資料を参照してください。  
  
-   [Windows サーバー システムのサービス概要とネットワーク ポート要件](https://support.microsoft.com/kb/832017)  
  
-   [製品 CD-ROM の Windows Server 2003 サポート ツールを使用した、RPC エンドポイント マッパー エラーのトラブルシューティング](https://support.microsoft.com/kb/839880)  
  
-   [リモート プロシージャ呼び出し (RPC)](https://go.microsoft.com/fwlink/?LinkId=118375)  
  
-   [ファイアウォールで動作するように RPC の動的ポート割り当てを構成する方法](https://support.microsoft.com/kb/154596/)  
  
##  <a name="BKMK_other_rules"></a> その他のファイアウォール ルールの操作  
 Windows ファイアウォールでは、ルールおよびルール グループを使用して、その構成が設定されます。 各ルールまたはルール グループは一般に、特定のプログラムやサービスに関連付けられており、そのプログラムやサービスによって、ユーザーの知らない間にそのルールが変更されたり削除されたりする場合があります。 たとえば、ルール グループ **[World Wide Web サービス (HTTP)]** と **[セキュア World Wide Web サービス (HTTPS)]** は IIS に関連付けられています。 これらのルールを有効にすると、ポート 80 とポート 443 が開き、これらのルールが有効になっている場合にポート 80 とポート 443 に依存する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能が有効になります。 ただし、IIS を構成する管理者が、それらのルールを変更するか無効にする可能性があります。 したがって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にポート 80 またはポート 443 を使用している場合は、他の IIS ルールとは別に希望のポート構成を維持する独自のルールまたはルール グループを作成する必要があります。  
  
 セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、該当する許可ルールと一致するトラフィックを許可できます。 したがって、どちらもポート 80 に該当する、パラメーターの異なるルールが 2 つある場合、いずれかのルールと一致するトラフィックが許可されます。 一方のルールでローカル サブネットからのポート 80 経由のトラフィックが許可され、もう一方のルールで任意のアドレスからのトラフィックが許可される場合、結果として、発信元に関係なくポート 80 へのすべてのトラフィックが許可されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのアクセスを有効に管理するために、管理者はサーバーで有効になっているすべてのファイアウォール ルールを定期的に確認する必要があります。  
  
##  <a name="BKMK_profiles"></a> ファイアウォール プロファイルの概要  
 ファイアウォール プロファイルについては、「 [セキュリティが強化された Windows ファイアウォール ファースト ステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=116080) 」の「 **ネットワークの場所を認識するホスト ファイアウォール**」を参照してください。 要約すると、オペレーティング システムでは、接続性、接続状態、およびカテゴリに関して、接続する各ネットワークが識別され記憶されます。  
  
 セキュリティが強化された Windows ファイアウォールでは、ネットワークの場所として 3 種類の設定があります。  
  
-   ドメイン。 Windows では、コンピューターが参加しているドメインのドメイン コントローラーへのアクセスを認証できます。  
  
-   パブリック。 ドメイン ネットワーク以外のすべてのネットワークがパブリックとして最初に分類されます。 インターネットへの直接接続となるネットワーク、または空港やコーヒー ショップのような公共の場所にあるネットワークです。  
  
-   プライベート。 ユーザーまたはアプリケーションによってプライベートと見なされるネットワークです。 信頼されたネットワークだけをプライベート ネットワークと見なす必要があります。 通常は、ホーム ネットワークまたは小規模ビジネス ネットワークをプライベートと見なすことができます。  
  
 管理者はネットワークの場所の種類ごとにプロファイルを作成できます。各プロファイルに、さまざまなファイアウォール ポリシーを指定できます。 どの時点においても 1 つのプロファイルのみが適用されます。 次のようなプロファイル順序が適用されます。  
  
1.  Windows では、コンピューターが参加しているドメインのドメイン コントローラーへのアクセスに対してすべてのインターフェイスが認証される場合、ドメイン プロファイルが適用されます。  
  
2.  すべてのインターフェイスがドメイン コントローラーに対して認証されるか、プライベート ネットワークの場所として分類されるネットワークに接続されている場合、プライベート プロファイルが適用されます。  
  
3.  それ以外の場合は、パブリック プロファイルが適用されます。  
  
 セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、すべてのファイアウォール プロファイルを表示し、構成できます。 コントロール パネルの **[Windows ファイアウォール]** では、現在のプロファイルのみを構成できます。  
  
##  <a name="BKMK_additional_settings"></a> コントロール パネルの [Windows ファイアウォール] を使用した追加のファイアウォール設定  
 ファイアウォールに例外を追加した場合、特定のコンピューターまたはローカル サブネットからの着信接続のみに対してポートを開くように制限できます。 ポートを開くスコープを制限すると、コンピューターが悪意のあるユーザーの攻撃にさらされるリスクを軽減できるので、このように設定することをお勧めします。  
  
> [!NOTE]  
>  コントロール パネルの **[Windows ファイアウォール]** では、現在のファイアウォール プロファイルのみを構成できます。  
  
#### <a name="to-change-the-scope-of-a-firewall-exception-using-the-windows-firewall-item-in-control-panel"></a>コントロール パネルの [Windows ファイアウォール] を使用して、ファイアウォールの例外のスコープを変更するには  
  
1.  コントロール パネルの **[Windows ファイアウォール]** の **[例外]** タブでプログラムまたはポートを選択し、 **[プロパティ]** または **[編集]** をクリックします。  
  
2.  **[プログラムの編集]** または **[ポートの編集]** ダイアログ ボックスの **[スコープの変更]** をクリックします。  
  
3.  次のいずれかのオプションを選択します。  
  
    -   **[任意のコンピューター (インターネット上のコンピューターを含む)]**  
  
         推奨されません。 この設定によって、自分のコンピューターのアドレスを指定した任意のコンピューターが、特定のプログラムまたはポートに接続できるようになります。 このような設定は、インターネット上の匿名ユーザーに情報を提供できるようにするために必要な場合がありますが、悪意のあるユーザーの攻撃にさらされるリスクが大きくなります。 この設定を有効にし、[エッジ トラバーサルを許可する] オプションなどのネットワーク アドレス変換 (NAT) トラバーサルも許可する場合は、悪意のあるユーザーの攻撃にさらされる可能性がさらに高くなります。  
  
    -   **[ユーザーのネットワーク (サブネット) のみ]**  
  
         **[任意のコンピューター]** より安全な設定です。 ネットワークのローカル サブネット上のコンピューターのみがプログラムまたはポートに接続できます。  
  
    -   **[カスタムの一覧]**  
  
     作成した一覧に IP アドレスが載っているコンピューターだけが接続できます。 この設定は、 **[ユーザーのネットワーク (サブネット) のみ]** よりもさらに安全ですが、DHCP を使用するクライアント コンピューターでは、その IP アドレスが変更されることがあります。 その場合、意図していたコンピューターは接続することができません。 その代わり、認証の対象として意図していなかった別のコンピューターに一覧の IP アドレスが割り当てられてしまい、そのコンピューターから接続できるようになる可能性があります。 **[カスタムの一覧]** オプションは、固定 IP アドレスを使用するように構成されている他のサーバーの一覧を作成する場合に適しています。ただし、侵入者が IP アドレスを偽装する可能性もあります。 ファイアウォール ルールを制限することは、最低限のネットワーク インフラストラクチャです。  
  
##  <a name="BKMK_WF_msc"></a> セキュリティが強化された Windows ファイアウォールのスナップインの使用  
 セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、さらに詳細なファイアウォール設定を構成できます。 スナップインにはルール ウィザードが組み込まれており、コントロール パネルの **[Windows ファイアウォール]** では使用できない設定も表示されます。 これらの設定は次のとおりです。  
  
-   暗号化の設定  
  
-   サービスの制限  
  
-   名前によってコンピューターの接続を制限する  
  
-   特定のユーザーまたはプロファイルに接続を制限する  
  
-   エッジ トラバーサルにより、トラフィックが NAT (Network Address Translation) ルーターをバイパスするのを許可する  
  
-   送信ルールを構成する  
  
-   セキュリティ ルールを構成する  
  
-   着信接続用に IPsec を要求する  
  
#### <a name="to-create-a-new-firewall-rule-using-the-new-rule-wizard"></a>新しい規則ウィザードを使用して、新しいファイアウォール ルールを作成するには  
  
1.  [スタート] ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして「 **WF.msc**」と入力し、 **[OK]** をクリックします。  
  
2.  **[セキュリティが強化された Windows ファイアウォール]** の左ウィンドウの **[受信の規則]** を右クリックし、 **[新しい規則]** をクリックします。  
  
3.  **新規の受信の規則ウィザード** で、必要な設定を行います。  
  
##  <a name="BKMK_troubleshooting"></a> ファイアウォール設定のトラブルシューティング  
 ファイアウォールの問題をトラブルシューティングする場合は、次のツールと手法が役立ちます。  
  
-   有効なポート ステータスは、ポートに関連付けられているすべてのルールの和集合です。 ポートを経由するアクセスをブロックしようとするときは、そのポート番号を参照しているすべてのルールの確認が有効な場合があります。 このためには、セキュリティが強化された Windows ファイアウォールの MMC スナップインを使用して、ポート番号によって受信ルールと送信ルールを並べ替えます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターでアクティブになっているポートを確認します。 この確認処理では、リッスンしている TCP/IP ポートの確認とポートのステータスの確認も行います。  
  
     受信待ちしているポートを確認するには、 **netstat** コマンド ライン ユーティリティを使用します。 **netstat** ユーティリティでは、アクティブな TCP 接続の表示以外にさまざまな IP の統計および情報も表示されます。  
  
    #### <a name="to-list-which-tcpip-ports-are-listening"></a>リッスンしている TCP/IP ポートの一覧を表示するには  
  
    1.  コマンド プロンプト ウィンドウを開きます。  
  
    2.  コマンド プロンプトで、「`netstat -n -a`」と入力します。  
  
         **-n** スイッチは、 **netstat** に対して、アクティブな TCP 接続のアドレスおよびポート番号を数字で表示するように指示します。 **-a** スイッチは、 **netstat** に対して、コンピューターがリッスンしている TCP ポートおよび UDP ポートを表示するように指示します。  
  
-   **PortQry** ユーティリティを使用して、TCP/IP ポートのステータスを LISTENING、NOT LISTENING、FILTERED としてレポートできます。 (FILTERED ステータスは、ポートが、LISTENING、NOT LISTENING のどちらか不明で、ユーティリティがポートからの応答を受信していないことを示します)。 **PortQry** ユーティリティは、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=17148)からダウンロードできます。  
  
## <a name="see-also"></a>参照  
 [Windows サーバー システムのサービス概要とネットワーク ポート要件](https://support.microsoft.com/kb/832017)  
