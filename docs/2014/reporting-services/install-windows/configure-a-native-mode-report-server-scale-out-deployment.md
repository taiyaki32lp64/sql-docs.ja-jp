---
title: ネイティブ モード レポート サーバー スケール アウト配置 (SSRS 構成マネージャー) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0281a487de123adfeb3739066628694b1da17a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108894"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment-ssrs-configuration-manager"></a>ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)

  Reporting Services ネイティブ モードでは、1 つのレポート サーバー データベースを共有する複数のレポート サーバー インスタンスを実行できる、スケールアウト配置モデルがサポートされています。 スケールアウト配置は、レポート サーバーのスケーラビリティを高めて、処理できる同時ユーザー数を増やしたり、より負荷の高いレポート実行に対応できるようにするために使用されます。 また、特定のサーバーを、対話型レポートまたはスケジュールされたレポートの処理専用にする場合にも使用できます。  
  
 SharePoint モードのレポート サーバーは、SharePoint 製品のインフラストラクチャを利用してスケールアウトを行います。SharePoint モードのスケールアウトは、SharePoint モードのレポート サーバーを SharePoint ファームに追加することによって実行されます。 SharePoint モードでのスケールアウトについては、 「[ファームへのレポート サーバーの追加 &#40;SSRS スケールアウト&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)」を参照してください。  
  
 **スケールアウト配置は次の要素で構成されます。**  
  
-   1 つのレポート サーバー データベースを共有する複数のレポート サーバー インスタンス。  
  
-   対話型ユーザー ロードを複数のレポート サーバー インスタンス間で分散するネットワーク負荷分散 (NLB) クラスター (オプション)。  
  
 NLB クラスターに Reporting Services を配置する場合は、レポート サーバー URL の構成で NLB 仮想サーバー名を使用し、各サーバーで同じビュー ステートが共有されるように構成する必要があります。  
  
 Reporting Services は Microsoft Cluster Services クラスターには参加しません。 ただし、フェールオーバー クラスターの一部であるデータベース エンジン インスタンス上にレポート サーバー データベースを作成することは可能です。  
  
 **スケールアウト配置を計画、インストール、および構成するには、次の手順を実行します。**  
  
-   レビュー[インストール ウィザードからの SQL Server 2014 のインストール&#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]レポート サーバー インスタンスをインストールする方法については、オンライン ブック。  
  
-   ネットワーク負荷分散 (NLB) クラスター上でスケールアウト配置をホストする場合は、NLB クラスターを構成してからスケールアウト配置を構成する必要があります。 詳細については、「 [ネットワーク負荷分散クラスターにおけるレポート サーバーの構成](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)」を参照してください。  
  
-   レポート サーバー データベースを共有してレポート サーバーをスケールアウトに加える方法については、このトピックの手順を確認してください。  
  
     この手順では、2 つのノードから成るレポート サーバーのスケールアウト配置を構成する方法について説明します。 他のレポート サーバー ノードを配置に追加するには、このトピックの手順を繰り返します。  
  
    -   セットアップを使用して、スケールアウト配置に追加する各レポート サーバー インスタンスをインストールします。  
  
         サーバー インスタンスを共有データベースに接続するときにデータベースの互換性エラーが発生しないようにするには、すべてのインスタンスが同じバージョンであることを確認します。 たとえば、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] レポート サーバー インスタンスを使用してレポート サーバー データベースを作成する場合は、同じ配置の他のすべてのインスタンスも [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]である必要があります。  
  
    -   Reporting Services 構成マネージャーを使用して、各レポート サーバーを共有データベースに接続します。 一度に接続および構成できるレポート サーバーは、1 つだけです。  
  
    -   Reporting Services 構成ツールを使用して、レポート サーバー データベースに既に接続されている最初のレポート サーバー インスタンスに新しいレポート サーバー インスタンスを追加してスケールアウトを完了します。  
  
### <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>SQL Server インスタンスをインストールしてレポート サーバー データベースをホストするには  
  
1.  レポート サーバー データベースをホストするコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをインストールします。 少なくとも、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]をインストールします。  
  
2.  必要に応じて、レポート サーバーでリモート接続を有効にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンの中には、既定で TCP/IP および名前付きパイプのリモート接続が有効になっていないバージョンもあります。 リモート接続が許可されているかどうかを確認するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、対象インスタンスのネットワーク構成設定を確認します。 リモート インスタンスが名前付きインスタンスの場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが有効になっていることと、ターゲット サーバーで実行されていることを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser によって、名前付きインスタンスへの接続に使用されるポート番号が提供されます。  
  
### <a name="to-install-the-first-report-server-instance"></a>最初のレポート サーバー インスタンスをインストールするには  
  
1.  配置の一部になる最初のレポート サーバー インスタンスをインストールします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]をインストールする際に、[レポート サーバー インストール オプション] ページで **[サーバーを構成せずにインストールする]** オプションを選択します。  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動します。  
  
3.  レポート サーバー Web サービスの URL、レポート マネージャーの URL、およびレポート サーバー データベースを構成します。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[レポート サーバーの構成 &#40;Reporting Services ネイティブ モード&#41;](../report-server/configure-a-report-server-reporting-services-native-mode.md)」を参照してください。  
  
4.  レポート サーバーが稼働することを確認します。 詳細については、 [オンライン ブックの「](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) Reporting Services のインストール状態の検証 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
### <a name="to-install-and-configure-the-second-report-server-instance"></a>2 番目のレポート サーバー インスタンスをインストールして構成するには  
  
1.  セットアップを実行し、2 番目の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスを別のコンピューターにインストールするか、同じコンピューターに名前付きインスタンスとしてインストールします。 Reporting Services をインストールする際に、[レポート サーバー インストール オプション] ページで **[サーバーを構成せずにインストールする]** オプションを選択します。  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動し、インストールした新しいインスタンスに接続します。  
  
3.  最初のレポート サーバー インスタンスのときに使用したデータベースにレポート サーバーを接続します。  
  
    1.  クリックして**データベース**データベース ページを開きます。  
  
    2.  **[データベースの変更]** をクリックします。  
  
    3.  **[既存のレポート サーバー データベースを選択する]** をクリックします。  
  
    4.  使用するレポート サーバー データベースをホストする SQL Server データベース エンジン インスタンスのサーバー名を入力します。 前の作業で接続したサーバーの名前を入力する必要があります。  
  
    5.  クリックして**接続のテスト**、順にクリックします**次**します。  
  
    6.  **レポート サーバー データベース**最初のレポート サーバー用に作成したデータベースを選択し、クリックして**次**します。 既定の名前は ReportServer です。 ReportServerTempDB は選択しないでください。ReportServerTempDB は、レポート処理時に一時データを格納するためにのみ使用されます。 データベースの一覧が空の場合は、前の 4 つの手順を繰り返してサーバーへの接続を確立します。  
  
    7.  [資格情報] ページで、レポート サーバーがレポート サーバー データベースに接続する際に使用するアカウントと資格情報の種類を選択します。 最初のレポート サーバー インスタンスと同一の資格情報、または別の資格情報を使用できます。 **[次へ]** をクリックします。  
  
    8.  クリックして**概要**順にクリックします**完了**します。  
  
4.  レポート サーバー Web サービスの URL を構成します。 URL のテストはまだ行わないでください。 URL は、レポート サーバーがスケールアウト配置に参加するまで解決されません。  
  
5.  レポート マネージャーの URL を構成します。 URL のテストや配置の確認はまだ行わないでください。 レポート サーバーは、スケールアウト配置に参加するまで使用できません。  
  
### <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>2 番目のレポート サーバー インスタンスをスケールアウト配置に追加するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを開き、最初のレポート サーバー インスタンスに再接続します。 最初のレポート サーバーは、暗号化と暗号化解除の操作に対する初期化が既に行われています。そのため、このレポート サーバーを使用して、他のレポート サーバー インスタンスをスケールアウト配置に追加できます。  
  
2.  **[スケールアウト配置]** をクリックして、[スケールアウト配置] ページを開きます。 レポート サーバー データベースに接続されている各レポート サーバーに対応する 2 つのエントリが表示されます。 最初のレポート サーバー インスタンスは既に参加済みで、 2 番目のレポート サーバー インスタンスは "参加を待っています" になっているはずです。 このようなエントリが表示されない場合は、レポート サーバー データベースを使用するように構成および初期化されている最初のレポート サーバーに接続していることを確認してください。  
  
     ![[スケール アウト配置] ページの部分的なスクリーン ショット](../../../2014/sql-server/install/media/scaloutscreen.gif "[スケール アウト配置] ページの部分的なスクリーン ショット")  
  
3.  [スケール アウト配置] ページで、配置に参加し、をクリックを待機しているレポート サーバー インスタンスを選択します。**サーバーの追加**します。  
  
    > [!NOTE]  
    >  **問題点:** Reporting Services レポート サーバー インスタンスをスケール アウト配置に参加しようとしたときに"へのアクセスが拒否されました"のようなエラー メッセージが発生する可能性があります。  
    >   
    >  **回避策:** バックアップ、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]最初から暗号化キー[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]インスタンスし、2 番目のキーを復元[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]レポート サーバー。 その後、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のスケールアウト配置に 2 番目のサーバーの追加を試行します。  
  
4.  これで、両方のレポート サーバー インスタンスが動作していることを確認できるようになります。 2 番目のインスタンスを確認するには、Reporting Services 構成ツールを使用してレポート サーバーに接続し、Web サービスまたはレポート マネージャーの URL をクリックします。  
  
 負荷分散されたサーバー クラスター内でレポート サーバーを実行する場合、追加の構成が必要です。 詳細については、「 [ネットワーク負荷分散クラスターにおけるレポート サーバーの構成](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
