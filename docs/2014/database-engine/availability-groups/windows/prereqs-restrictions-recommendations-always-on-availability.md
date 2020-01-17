---
title: AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b12b9030d27e371e0299e06917464b1467b9b10e
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782956"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 (SQL Server)
  このトピックでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の展開に関して、各種コンポーネント (ホスト コンピューター、Windows Server フェールオーバー クラスタリング (WSFC) クラスター、サーバー インスタンス、可用性グループ) の前提条件、制限、推奨事項などの考慮事項について説明します。 各コンポーネントのセキュリティに関する考慮事項のほか、要求される権限 (該当する場合) にも触れています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を配置する前に、このトピックのすべてのセクションを読むことを強くお勧めします。  
  
 
  
##  <a name="DotNetHotfixes"></a>AlwaysOn 可用性グループをサポートする .net 修正プログラム  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で使用する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]コンポーネントと機能によっては、次の表で指定されている追加の .Net 修正プログラムのインストールが必要になる場合があります。 これらの修正プログラムは任意の順序でインストールできます。  
  
||依存機能|修正プログラム|リンク|  
|------|-----------------------|------------|----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|.Net 3.5 SP1 の修正プログラムは、SQL クライアントに読み取り目的、読み取り専用、および multisubnetfailover の AlwaysOn 機能のサポートを追加します。 修正プログラムは、各 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート サーバーにインストールする必要があります。|KB 2654347: [AlwaysOn 機能のサポートを追加する .Net 3.5 SP1 の修正プログラム](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a> Windows のシステム要件と推奨事項  
  
  
###  <a name="SystemRequirements"></a> チェック リスト: 要件 (Windows システム)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の機能を利用するには、1 つまたは複数の可用性グループに参加するすべてのコンピューターが、次の基本要件を満たしている必要があります。  
  
||要件|リンク|  
|------|-----------------|----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|システムがドメイン コントローラーではないことを確認します。|可用性グループは、ドメイン コントローラーではサポートされていません。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべてのコンピューターで x86 (WOW64 は不可) または x64 Windows Server 2008 以降のバージョンが実行されていることを確認します。|WOW64 (Windows 64 ビット上の Windows 32 ビット) では、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]がサポートされません。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべてのコンピューターが、Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のノードであることを確認します。|[Windows Server フェールオーバー クラスタリン &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|必要な可用性グループの構成に耐える十分なノードが WSFC クラスターに存在することを確認します。|WSFC ノードは、1 つの可用性グループにつき 1 つだけ可用性レプリカをホストすることができます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスは、特定の WSFC ノード上で複数の可用性グループの可用性レプリカをホストできます。<br /><br /> 予定している可用性グループの可用性レプリカをサポートするために必要な WSFC ノードの数については、データベース管理者にお問い合わせください。<br /><br /> [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべての適用可能な Windows 修正プログラムが WSFC クラスター内のすべてのノードにインストールされていることを確認します。|**\*\* 重要な \*\*** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] が展開される WSFC クラスターのノードには、いくつかの修正プログラムが必要または推奨されます。 詳細については、後の「[AlwaysOn 可用性グループをサポートする Windows 修正プログラム (Windows システム)](#WinHotfixes)」を参照してください。|  
  
> [!IMPORTANT]  
>  可用性グループへの接続に必要な構成が環境に対して正しく実施されていることも確認します。 詳細については、「 [AlwaysOn クライアント接続 (SQL Server)](always-on-client-connectivity-sql-server.md)」を参照してください。  
  
####  <a name="WinHotfixes"></a>AlwaysOn 可用性グループをサポートする windows 修正プログラム (Windows システム)  
 クラスター トポロジに応じて、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートするために Windows Server 2008 Service Pack 2 (SP2) または Windows Server 2008 R2 のいくつかの追加の修正プログラムを適用できます。 次の表で、これらの修正プログラムを示します。 これらの修正プログラムは任意の順序でインストールできます。  
  
||Windows 2008 SP2 への適用|Windows 2008 R2 SP1 への適用|Windows 2012 に含まれている|サポート対象...|修正プログラム|リンク|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|はい|**最適な WSFC クォーラムの構成**|サポート技術情報の記事 2494036 に記載されている修正プログラムが、各 WSFC ノードにインストールされていることを確認します。<br /><br /> この修正プログラムは、非自動フェールオーバー ターゲットでの最適なクォーラム構成をサポートします。 投票するノードを自分で選択できるようにすることで、マルチサイト クラスターの改善を図ります。|KB 2494036:  [クォーラムの投票のないクラスター ノードを Windows Server 2008 および Windows Server 2008 R2 で構成できる修正プログラムを公開](https://support.microsoft.com/kb/2494036)<br /><br /> クォーラムの投票の詳細については、「[WSFC クォーラム モードと投票構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」を参照してください。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|はい|**ネットワーク帯域幅の効率的な使用**|サポート技術情報の記事 2616514 に記載されている修正プログラムが、各 WSFC ノードにインストールされていることを確認します。<br /><br /> この修正プログラムがないと、クラスター サービスはクラスター ノード間で不要なレジストリ通知を送信します。 この動作によりネットワークの帯域幅が制限され、 [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)]にとって深刻な問題となります。|KB 2616514:  [クラスター サービスは、Windows Server 2008 または Windows Server 2008 R2 のクラスター ノード間で不要なレジストリ キー変更通知を送信する](https://support.microsoft.com/kb/2616514)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")||はい|適用なし|**すべての WSFC ノードで使用できないディスク上の VPD ストレージテスト**|WSFC ノードで Windows Server 2008 R2 Service Pack 1 (SP1) が実行されている場合に、オンラインの (なおかつ WSFC クラスター内の一部のノードから利用できない) ディスクに対して誤って Validate SCSI Device Vital Product Data (VPD) ストレージ テストを実行し、その結果不合格になった場合は、サポート技術情報の記事 2531907 に掲載されている修正プログラムをインストールします。<br /><br /> この修正プログラムは、ディスクがオンラインである場合に、誤った警告やエラーが検証レポートに出力されるのを防ぎます。|KB 2531907: [Windows Server 2008 R2 SP1 のインストール後、Validate SCSI Device Vital Product Data (VPD) テストで不合格になる](https://support.microsoft.com/kb/2531907)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")||はい|はい|**ローカルレプリカへのフェールオーバーの高速化**|WSFC ノードで Windows Server 2008 R2 Service Pack 1 (SP1) を実行している場合は、サポート技術情報の記事 2687741 に記載されている修正プログラムがインストールされていることを確認します。<br /><br /> この修正プログラムにより、ローカル レプリカへの [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] フェールオーバーのパフォーマンスが向上します。|KB 2687741:  [Windows server 2008 R2 で使用できる、SQL Server 2012 の "AlwaysOn 可用性グループ" 機能のパフォーマンスを向上させる修正プログラム](https://support.microsoft.com/KB/2687741)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|はい|**非対称ストレージ-フェールオーバークラスターインスタンス (FCIs)**|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に対してフェールオーバー クラスター インスタンス (FCI) が有効になっている場合は、Windows Server 2008 修正プログラム 976097 をインストールします。<br /><br /> この修正プログラムにより、フェールオーバークラスター管理 Microsoft 管理コンソール (MMC) スナップインが有効になり、一部の WSFC ノードでのみ使用できる非対称の記憶域共有ディスクがサポートされます。|KB 976097: [非対称ストレージのサポートをフェールオーバー クラスターの管理 MMC スナップインに追加するための修正プログラム (Windows Server 2008 または Windows Server 2008 R2 を実行するフェールオーバー クラスター用)](https://support.microsoft.com/kb/976097)<br /><br /> [AlwaysOn アーキテクチャガイド: フェールオーバークラスターインスタンスと可用性グループを使用した高可用性およびディザスターリカバリーソリューションの構築](https://technet.microsoft.com/library/jj215886.aspx)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|適用なし|**インターネットプロトコルセキュリティ (IPsec)**|環境で IPsec 接続を使用する場合、クライアント コンピューターが仮想ネットワーク名 (このコンテキストでは可用性グループ リスナー) への IPsec 接続を再確立するときに、長時間 (約 2 ～ 3 分) の遅延が発生する可能性があります。 IPsec 接続を使用する場合は、サポート技術情報の記事 (KB 980915) に詳細が記載されている特定のシナリオについてお読みになることをお勧めします。|KB 980915:  [Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7、または Windows Server 2008 R2 を実行しているコンピューターからの IPSec 接続の再接続時に長時間の遅延が発生する](https://support.microsoft.com/kb/980915)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|はい|**IPv6**|IPv6 を使用する場合は、Windows Server オペレーティング システムに応じて、サポート技術情報の記事 2578103 または 2578113 に詳細が記載されている特定のシナリオについてお読みになることをお勧めします。<br /><br /> Windows Server トポロジが IP version 6 (IPv6) を使用する場合、WSFC クラスター サービスが IPv6 IP アドレスのフェールオーバーに約 30 秒かかります。 このため、クライアントは IPv6 IP アドレスに再接続するまでに、約 30 秒待機することになります。|KB 2578103 (Windows Server 2008): [クラスター サービスが Windows Server 2008 で IPv6 IP アドレスのフェールオーバーに約 30 秒かかる](https://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113 (Windows Server 2008 R2): **Windows Server 2008 R2:** [クラスター サービスが Windows Server 2008 R2 で IPv6 IP アドレスのフェールオーバーに約 30 秒かかる](https://support.microsoft.com/kb/2578113)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|はい|はい|はい|**クラスターとアプリケーションサーバーの間にルーターがない**|フェールオーバー クラスターとアプリケーション サーバー間にルーターがない場合に、クラスター サービスのネットワーク関連リソースのフェールオーバー操作が遅くなります。 これにより、可用性グループがフェールオーバーした後でクライアントの再接続が遅延します。 ルーターがない場合は、サポート技術情報の記事 2582281 に詳細が記載されている特定のシナリオについてお読みになり、環境に該当する場合は修正プログラムをインストールすることをお勧めします。|KB 2582281:  [クラスターとアプリケーション サーバー間にルーターがない場合にフェールオーバー操作が遅い](https://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> 可用性レプリカをホストするコンピューターに関する推奨事項 (Windows システム)  
  
-   **同程度のシステム:**  可用性グループ内の可用性レプリカはすべて、ワークロードの処理能力が同程度であるシステム上で運用する必要があります。  
  
-   **専用のネットワーク アダプター:** 最適なパフォーマンスを得るには、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に専用のネットワーク アダプター (ネットワーク インターフェイス カード) を使用します。  
  
-   **十分なディスク領域:**  可用性レプリカをホストするサーバー インスタンスのあるすべてのコンピューターには、可用性グループ内のすべてのデータベースを格納できるだけのディスク領域が存在する必要があります。 プライマリ データベースが大きくなるにつれて、対応するセカンダリ データベースも同じだけ大きくなる点に注意してください。  
  
###  <a name="PermissionsWindows"></a> 権限 (Windows システム)  
 WSFC クラスターを管理するユーザーは、すべてのクラスター ノードのシステム管理者であることが必要です。  
  
 クラスターを管理するためのアカウントの詳細については、「 [付録 A: フェールオーバー クラスターの要件](https://technet.microsoft.com/library/dd197454\(WS.10\).aspx)」を参照してください。  
  
###  <a name="RelatedTasksWindows"></a> 関連タスク (Windows システム)  
  
|タスク|リンク|  
|----------|----------|  
|HostRecordTTL の値を設定します。|[HostRecordTTL の変更 (Windows PowerShell を使用)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> HostRecordTTL の変更 (Windows PowerShell を使用)  
  
1.  **[管理者として実行]** を選択して PowerShell ウィンドウを開きます。  
  
2.  FailoverClusters モジュールをインポートします。  
  
3.  `Get-ClusterResource` コマンドレットを使用してネットワーク名リソースを検索し、次に `Set-ClusterParameter` コマンドレットを使用して `HostRecordTTL` 値を設定します。次に例を示します。  
  
     Get-ClusterResource " *\<NetworkResourceName>* " | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     次に示す PowerShell の例では、"`SQL Network Name (SQL35)`" というネットワーク名リソースの HostRecordTTL を 300 秒に設定します。  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  新しい PowerShell ウィンドウを開くたびに、`FailoverClusters` モジュールをインポートする必要があります。  
  
##### <a name="related-content-powershell"></a>関連コンテンツ (PowerShell)  
  
-   [クラスターと高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (フェールオーバー クラスタリングとネットワーク負荷分散のチームのブログ)  
  
-   [フェールオーバー クラスターの Windows PowerShell の概要](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [クラスター リソースのコマンドと同等の Windows PowerShell コマンドレット](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> 関連コンテンツ (Windows システム)  
  
-   [マルチサイト フェールオーバー クラスターの DNS 設定を構成する](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [ネットワーク名リソースを使用した DNS 登録](https://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Windows 2008 R2 フェールオーバーマルチサイトクラスタリング](https://kiruba4u.blogspot.com/2012/03/failover-clustering-in-windows-server.html)  
  
##  <a name="ServerInstance"></a> SQL Server インスタンスの前提条件と制限  
 可用性グループにはそれぞれ、 *のインスタンスによってホストされる一連のフェールオーバー パートナー (* 可用性レプリカ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) が必要です。 サーバー インスタンスには、*スタンドアロン インスタンス* または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *フェールオーバー クラスター インスタンス* (FCI) を使用できます。  
  
 
  
###  <a name="PrerequisitesSI"></a> チェック リスト: 前提条件 (サーバー インスタンス)  
  
||前提条件|リンク|  
|-|------------------|-----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|ホスト コンピューターは、Windows Server フェールオーバー クラスタリング (WSFC) ノードであることが必要です。 可用性グループの可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスは、同じ WSFC クラスターの別のノードに存在する必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。|[Windows Server フェールオーバー クラスタリン &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [フェールオーバークラスタリングと&#40;AlwaysOn 可用性グループ SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループで Kerberos を操作するには:<br /><br /> 可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで、同じ SQL Server サービス アカウントを使用する必要があります。<br /><br /> ドメイン管理者は、可用性グループ リスナーの仮想ネットワーク名 (VNN) の SQL Server サービス アカウントに、Active Directory でサーバー プリンシパル名 (SPN) を手動で登録する必要があります。 SQL Server サービス アカウント以外のアカウントに SPN が登録されている場合は、認証が失敗します。<br /><br /> **\*\* 重要 \*\*** SQL Server サービス アカウントを変更した場合は、ドメイン管理者が SPN を手動で再登録する必要があります。|[Kerberos 接続用のサービス プリンシパル名の登録](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **簡単な説明:**<br /><br /> Kerberos と SPN は相互認証を行います。 SPN は、SQL Server サービスを起動する Windows アカウントにマップされます。 SPN が正常に登録されていないか登録に失敗した場合、Windows セキュリティ レイヤーは、SPN に関連するアカウントを決定することができず、Kerberos 認証は使用できません。<br /><br /> 注: NTLM には、この要件はありません。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストする予定がある場合は、FCI の制限を確実に理解し、FCI の要件が満たされていることを確認してください。|[SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と要件](#FciArLimitations) (このトピックの後半)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべてのサーバー インスタンスで Enterprise Edition の [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]が実行されている必要があります。|[SQL Server 2014 の各エディションがサポートする機能](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|特定の可用性グループの可用性レプリカをホストするすべてのサーバー インスタンス間で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の照合順序を統一する必要があります。|[サーバーの照合順序の設定または変更](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能を有効にします。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のサーバー インスタンスは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 環境がサポートする範囲内であれば、1 台のコンピューターでいくつでも有効にすることができます。|[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> **\*\* 重要 \*\*** WSFC クラスターを削除してから再作成した場合は、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を有効にしていた、元の WSFC クラスター上の各サーバー インスタンスについて、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能を無効にしてからもう一度有効にする必要があります。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべてのサーバー インスタンスには、データベース ミラーリング エンドポイントが必要です。 このエンドポイントは、サーバー インスタンス上のミラーリング監視サーバーとデータベース ミラーリング パートナー、および可用性レプリカすべてによって共有されます。<br /><br /> 可用性レプリカのホストとして選んだサーバー インスタンスがドメイン ユーザー アカウントで実行されていて、まだデータベース ミラーリング エンドポイントが存在しない場合、[新しい可用性グループ ウィザード](use-the-availability-group-wizard-sql-server-management-studio.md) (または[可用性グループへのレプリカの追加ウィザード](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) でエンドポイントを作成し、サーバー インスタンス サービス アカウントに CONNECT 権限を許可することができます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがビルトイン アカウント (Local System、Local Service、Network Service など) で実行されている場合または非ドメイン アカウントで実行されている場合は、エンドポイント認証に証明書を使用する必要があります。ウィザードは、サーバー インスタンス上でデータベース ミラーリング エンドポイントを作成できなくなります。 この場合は、データベース ミラーリング エンドポイントを手動で作成してからウィザードを起動することをお勧めします。<br /><br /> **\*\* セキュリティに関する注意 \*\*** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のトランスポート セキュリティは、データベース ミラーリングと同じです。|[データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [データベースミラーリングと AlwaysOn 可用性グループ&#40;SQL Server のトランスポートセキュリティ&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|FILESTREAM を使用するデータベースを可用性グループに追加する場合は、その可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで FILESTREAM が有効になっていることを確認してください。|[FILESTREAM の有効化と構成](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|包含データベースを可用性グループに追加する場合は、その可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで `contained database authentication` サーバー オプションが `1` に設定されていることを確認してください。|[contained database authentication サーバー構成オプション](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [サーバー構成オプション &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> 可用性グループによるスレッドの使用  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] には、ワーカー スレッドに関する次の要件があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のアイドル状態のインスタンスでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] はスレッドを使用しません。  
  
-   可用性グループが使用するスレッドの最大数は、サーバー スレッドの最大数 (`max worker threads`) から 40 を引いた数にあらかじめ設定されています。  
  
-   特定のサーバー インスタンスでホストされる可用性レプリカは 1 つのスレッド プールを共有します。  
  
     スレッドは、次のように要求に基づいて共有されます。  
  
    -   通常は 3 個から 10 個の共有スレッドがありますが、プライマリ レプリカのワークロードに応じてこの数が増える場合があります。  
  
    -   特定のスレッドが一定期間アイドル状態になると、そのスレッドは解放され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の汎用スレッド プールに戻されます。 通常、非アクティブ スレッドは、非アクティブな状態のまま最大 15 秒経過すると解放されます。 ただし、最後の利用状況によっては、アイドル状態のスレッドが保持される時間が延長される場合があります。  
  
-   さらに、可用性グループでは非共有スレッドを次のように使用します。  
  
    -   各プライマリ レプリカでは、プライマリ データベースごとにログ キャプチャ スレッドを 1 つ使用します。 また、セカンダリ データベースごとにログ送信スレッドを 1 つ使用します。 ログ送信スレッドは、非アクティブな状態のまま最大 15 秒経過すると解放されます。  
  
    -   各セカンダリ レプリカでは、セカンダリ データベースごとに再実行スレッドを 1 つ使用します。 再実行スレッドは、非アクティブな状態のまま最大 15 秒経過すると解放されます。  
  
    -   セカンダリ レプリカでのバックアップでは、バックアップ操作の間、プライマリ レプリカにスレッドが保持されます。  
  
 詳細については、「[AlwaysON - HADRON 学習シリーズ: HADRON 対応データベースのワーカー プールの使用」](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)(CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エンジニアのブログ) を参照してください。  
  
###  <a name="PermissionsSI"></a> 権限 (サーバー インスタンス)  
  
|タスク|必要な権限|  
|----------|--------------------------|  
|データベース ミラーリング エンドポイントを作成する|CREATE ENDPOINT 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  また、CONTROL ON ENDPOINT 権限も必要です。 詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)」を参照してください。|  
|有効にする [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|ローカル コンピューターの **Administrator** グループのメンバーシップおよび WSFC クラスターに対するフル コントロール権限が必要です。|  
  
###  <a name="RelatedTasksSI"></a> 関連タスク (サーバー インスタンス)  
  
|タスク|トピック|  
|----------|-----------|  
|データベース ミラーリング エンドポイントが存在するかどうかを確認する|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|データベース ミラーリング エンドポイントを作成する (まだ存在しない場合)|[Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [AlwaysOn 可用性グループ&#40;SQL Server PowerShell のデータベースミラーリングエンドポイントを作成する&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|AlwaysOn 可用性グループを有効にする|[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> 関連コンテンツ (サーバー インスタンス)  
  
-   [AlwaysON-HADRON 学習シリーズ: HADRON 対応データベースのワーカープールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> ネットワーク接続の推奨事項  
 WSFC クラスター メンバー間の通信と、可用性レプリカ間の通信には、同じネットワーク リンクを使用することを強くお勧めします。  別々のネットワーク リンクを使用すると、一部のリンクにエラーが発生した場合に (断続的なエラーであっても)、予期しない動作が発生する可能性があります。  
  
 たとえば、自動フェールオーバーをサポートする可用性グループでは、自動フェールオーバー パートナーであるセカンダリ レプリカの状態が SYNCHRONIZED である必要があります。 このセカンダリ レプリカへのネットワーク リンクにエラーが発生した場合 (断続的なエラーであっても)、レプリカが UNSYNCHRONIZED 状態になり、リンクが復元されるまで再同期を開始できません。 セカンダリ レプリカが非同期状態にある間に WSFC クラスターが自動フェールオーバーを要求しても、自動フェールオーバーは行われません。  
  
##  <a name="ClientConnSupport"></a> クライアント接続のサポート  
 クライアント接続の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] サポートの詳細については、「 [AlwaysOn クライアント接続 (SQL Server)](always-on-client-connectivity-sql-server.md)」を参照してください。  
  
##  <a name="FciArLimitations"></a> SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と制限  
 
  
###  <a name="RestrictionsFCI"></a> 制限 (FCI)  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 以降では、AlwaysOn フェールオーバー クラスター インスタンスは、[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] と [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] の両方でクラスター化ボリューム (CSV) をサポートしています。 CSV の詳細については、「 [フェールオーバー クラスターのクラスターの共有ボリュームについて](https://technet.microsoft.com/library/dd759255.aspx)」を参照してください。  
  
-   **FCI のクラスター ノードでホストできるレプリカは、特定の可用性グループに対して 1 つだけである:**  FCI に可用性レプリカを追加する場合、FCI の有効な所有者である WSFC クラスター ノードで、同じ可用性グループに対して別のレプリカをホストすることはできません。  
  
     さらに、その他の各レプリカは、同じ WSFC クラスター内の別の WSFC ノードに存在する SQL Server 2012 のインスタンスによってホストされている必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。  
  
-   **可用性グループによる自動フェールオーバーは FCI ではサポートされない:**  FCI は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
-   **FCI ネットワーク名の変更:**  可用性レプリカがホストされている FCI のネットワーク名を変更する必要がある場合、レプリカをその可用性グループから削除してから再度、可用性グループに追加する必要があります。 プライマリ レプリカを削除することはできません。そのため、プライマリ レプリカがホストされている FCI の名前を変更するには、セカンダリ レプリカにフェールオーバーしてから、以前のプライマリ レプリカを削除し、再度追加する必要があります。 FCI の名前を変更すると、そのデータベース ミラーリング エンドポイントの URL が変わる可能性があります。 レプリカを追加する際は、必ず最新のエンドポイントの URL を指定してください。  
  
###  <a name="PrerequisitesFCI"></a> チェック リスト: 前提条件 (FCI)  
  
||前提条件|リンク|  
|-|------------------|----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|FCI を使用して可用性レプリカをホストする場合は、サポート技術情報の記事 KB 976097 に記載されている Windows Server 2008 の修正プログラムが、システム管理者によってインストール済みであることを事前に確認してください。 この修正プログラムにより、フェールオーバークラスター管理 Microsoft 管理コンソール (MMC) スナップインが有効になり、一部の WSFC ノードでのみ使用できる非対称の記憶域共有ディスクがサポートされます。|KB 976097: [非対称ストレージのサポートをフェールオーバー クラスターの管理 MMC スナップインに追加するための修正プログラム (Windows Server 2008 または Windows Server 2008 R2 を実行するフェールオーバー クラスター用)](https://support.microsoft.com/kb/976097)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|標準の SQL Server フェールオーバー クラスター インスタンスのインストールと同様、各 SQL Server フェールオーバー クラスター インスタンス (FCI) が必要な共有ストレージを所有していることを確認してください。||  
  
###  <a name="RelatedTasksFCIs"></a> 関連タスク (FCI)  
  
|タスク|トピック|  
|----------|-----------|  
|SQL Server フェールオーバー クラスターのインストール|[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|既存の SQL Server フェールオーバー クラスターのインプレース アップグレード|[SQL Server フェールオーバー クラスター インスタンスのアップグレード &#40;セットアップ&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|既存の SQL Server フェールオーバー クラスターのメンテナンス|[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> 関連コンテンツ (FCI)  
  
-   [フェールオーバークラスタリングと&#40;AlwaysOn 可用性グループ SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn アーキテクチャガイド: フェールオーバークラスターインスタンスと可用性グループを使用した高可用性およびディザスターリカバリーソリューションの構築](https://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> 可用性グループの前提条件と制限  

  
###  <a name="RestrictionsAG"></a> 制限 (可用性グループ)  
  
-   **可用性レプリカは、1 つの WSFC クラスターの別々のノードによってホストされている必要がある:**  各可用性グループで、個々の可用性レプリカは、同じ WSFC クラスターの別々のノード上で動作するサーバー インスタンスによってホストされる必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。  
  
    > [!NOTE]  
    >  同じ物理コンピューター上の各仮想マシンは独立したコンピューターとして動作するため、同じ可用性グループの可用性レプリカをそれぞれの仮想マシンがホストできます。  
  
-   **一意の可用性グループ名:**  各可用性グループの名前は、WSFC クラスター上で一意である必要があります。 可用性グループ名の最大文字数は 128 文字です。  
  
-   **可用性レプリカ:**  各可用性グループは、1 つのプライマリ レプリカと最大 8 つのセカンダリ レプリカをサポートします。 すべてのレプリカを非同期コミット モードで実行することも、最大 3 つのレプリカを同期コミット モードで実行することもできます (1 つのプライマリ レプリカと 2 つの同期セカンダリ レプリカ)。  
  
-   **コンピューターあたりの可用性グループおよび可用性データベースの最大数:** コンピューター (VM または物理コンピューター) に実際に配置できるデータベースおよび可用性グループの数はハードウェアとワークロードによって異なりますが、強制的な制限はありません。 マイクロソフトでは、物理コンピューターあたり 10 の AG と 100 の DB を使用して広範なテストを行いました。 過剰な負荷がかかっているシステムには、ワーカー スレッドの枯渇、AlwaysOn システム ビューおよび DMV の応答の遅延、ディスパッチャー システム ダンプの一時停止などの症状があります (ただし、これだけではありません)。 アプリケーション SLA 内でピーク ワークロード容量を処理できることを確認するために、実稼働環境と同様のワークロードを使用して環境を十分にテストしてください。 SLA を検討する際は、障害条件下の負荷や期待される応答時間を考慮してください。  
  
-   **フェールオーバー クラスター マネージャーを使用して可用性グループを操作しないでください。**  
  
     例 :  
  
    -   可用性グループのプロパティ (たとえば、有効な所有者) を変更しないでください。  
  
    -   フェールオーバー クラスター マネージャーを使用して可用性グループをフェールオーバーしないでください。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用する必要があります。  
  
###  <a name="RequirementsAG"></a> 前提条件 (可用性グループ)  
 可用性グループの構成を作成したり再構成したりする場合は、次の要件を満たす必要があります。  
  
||前提条件|[説明]|  
|-|------------------|-----------------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストする予定がある場合は、FCI の制限を確実に理解し、FCI の要件が満たされていることを確認してください。|[SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と制限](#FciArLimitations) (このトピックの前半)|  
  
###  <a name="SecurityAG"></a> セキュリティ (可用性グループ)  
  
-   セキュリティは、Windows Server フェールオーバー クラスタリング (WSFC) クラスターから継承されます。 WSFC には、WSFC クラスター API 全体の粒度で 2 レベルのユーザー セキュリティが用意されています。  
  
    -   読み取り専用アクセス  
  
    -   フル コントロール  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] はフル コントロールを必要とします。また、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を有効にした [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスには、WSFC クラスターのフル コントロール権限が (サービス SID を介して) 与えられます。  
  
         サーバー インスタンスのセキュリティを WSFC フェールオーバー クラスター マネージャーで直接追加したり削除したりすることはできません。 WSFC セキュリティ セッションを管理するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーまたはそれに相当する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の WMI を使用します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスには、レジストリやクラスターにアクセスするための権限が必要です。  
  
-   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可用性レプリカをホストするサーバー インスタンス間の接続は暗号化するようにお勧めします。  
  
#### <a name="permissions-availability-groups"></a>権限 (可用性グループ)  
  
|タスク|必要な権限|  
|----------|--------------------------|  
|可用性グループの作成|**sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。|  
|可用性グループの変更|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。<br /><br /> さらに、データベースを可用性グループに参加させるには、 **db_owner** 固定データベース ロールのメンバーシップが必要です。|  
|可用性グループの削除|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。 ローカル レプリカの場所でホストされていない可用性グループを削除するには、その可用性グループ上の CONTROL SERVER 権限または CONTROL 権限が必要です。|  
  
###  <a name="RelatedTasksAGs"></a> 関連タスク (可用性グループ)  
  
|タスク|トピック|  
|----------|-----------|  
|可用性グループの作成|[可用性グループ (新しい可用性グループ ウィザード)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [可用性グループの作成 (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [可用性グループの作成 (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|可用性レプリカの数の変更|[可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|可用性グループ リスナーの作成|[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|可用性グループの削除|[可用性グループの削除 &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> 可用性データベースの前提条件と制限  
 可用性グループに追加するデータベースは、次の前提条件と制限を満たしている必要があります。  
  
 
  
###  <a name="RequirementsDb"></a> チェック リスト: 要件 (可用性データベース)  
 可用性グループに追加するデータベースは、次の条件を満たしている必要があります。  
  
||の要件|リンク|  
|-|------------------|----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|ユーザー データベースであること。 システム データベースを可用性グループに追加することはできません。||  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの作成先となる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス上に存在し、そのサーバー インスタンスからアクセスできること。||  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|読み取り/書き込み可能なデータベースであること。 読み取り専用データベースを可用性グループに追加することはできません。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|マルチユーザー データベースであること。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|AUTO_CLOSE が使用されていないこと。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|完全復旧モデル (完全復旧モードとも呼ばれます) を使用すること。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|データベースの完全バックアップが少なくとも 1 つ存在すること。<br /><br /> 注: データベースを完全復旧モードに設定した後、完全復旧ログ チェーンを開始するには完全バックアップが必要です。|[データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|既存の可用性グループに属していないこと。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|データベース ミラーリング用に構成されていないこと。|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) (データベースがミラー化の対象となっていない場合、"mirroring_" で始まるすべての列は NULL)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|FILESTREAM を使用するデータベースを可用性グループに追加する前に、その可用性グループの可用性レプリカをホストしている (またはこれからホストする) すべてのサーバー インスタンスで FILESTREAM が有効になっていることを確認してください。|[FILESTREAM の有効化と構成](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|包含データベースを可用性グループに追加する前に、その可用性グループの可用性レプリカをホストしている (またはこれからホストする) 各サーバー インスタンスで、`contained database authentication` サーバー オプションが `1` に設定されていることを確認してください。|[contained database authentication サーバー構成オプション](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [サーバー構成オプション &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、サポートされているすべてのデータベース互換性レベルで動作します。  
  
###  <a name="RestrictionsDb"></a> 制限事項 (可用性データベース)  
  
-   セカンダリ データベースのファイル パス (ドライブ文字を含む) が、対応するプライマリ データベースのパスと異なる場合、次の制限が適用されます。  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  **[完全]** オプションはサポートされません ([[最初のデータの同期を選択]](select-initial-data-synchronization-page-always-on-availability-group-wizards.md) ページ)、  
  
    -   **RESTORE WITH MOVE:**  セカンダリ データベースを作成するには、セカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンス上で、WITH MOVE を使用してデータベース ファイルを復元する必要があります。  
  
    -   **ファイルの追加操作への影響:**  後でファイルの追加操作をプライマリ レプリカで実行した場合、セカンダリ データベースでエラーが発生する可能性があります。 この操作の失敗によってセカンダリ データベースが中断する可能性があります。 セカンダリ データベースが中断すると、セカンダリ レプリカが "NOT SYNCHRONIZING" 状態になります。  
  
        > [!NOTE]  
        >  ファイルの追加操作が失敗した場合の対処については、「[失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)」を参照してください。  
  
-   可用性グループに現在属しているデータベースを削除することはできません。  
  
###  <a name="TDEdbs"></a> TDE で保護されたデータベースの補足情報  
 透過的なデータ暗号化 (TDE) を使用する場合、他のキーの作成および暗号化解除を行うための証明書または非対称キーは、可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで同じである必要があります。 詳細については、「 [別の SQL Server への TDE で保護されたデータベースの移動](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)」を参照してください。  
  
###  <a name="PermissionsDbs"></a> 権限 (可用性データベース)  
 データベースに対する ALTER 権限が必要です。  
  
###  <a name="RelatedTasksADb"></a> 関連タスク (可用性データベース)  
  
|タスク|トピック|  
|----------|-----------|  
|セカンダリ データベースの準備 (手動)|[可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|可用性グループへのセカンダリ データベースの参加 (手動)|[可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|可用性データベースの数の変更|[可用性グループへのデータベースの追加 &#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [可用性グループからのセカンダリ データベースの削除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [可用性グループからのプライマリ データベースの削除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性とディザスターリカバリーのための AlwaysOn ソリューションガイドの Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn チームのブログ: AlwaysOn チームの公式 SQL Server のブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
-   [AlwaysON-HADRON 学習シリーズ: HADRON 対応データベースのワーカープールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [フェールオーバークラスタリングと&#40;AlwaysOn 可用性グループ&#41; SQL Server](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn クライアント接続 (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
