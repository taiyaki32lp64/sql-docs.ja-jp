---
title: レポート サーバーのパフォーマンスの監視 | Microsoft Docs
ms.date: 06/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d277089fded73524e55d05bbc21078d5df426e3
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412656"
---
# <a name="monitoring-report-server-performance"></a>レポート サーバーのパフォーマンスの監視
  パフォーマンス監視ツールを使用してレポート サーバーのパフォーマンスを監視することにより、サーバーの利用状況の評価、傾向の監視、システムのボトルネックの診断、および現在のシステム構成で十分かどうかを判断するためのデータの収集を行うことができます。 サーバーのパフォーマンスを調整するには、レポート サーバー アプリケーション ドメインを再利用する頻度を指定します。 詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。  
  
## <a name="sources-of-performance-data"></a>パフォーマンス データのソース  
 システムの実行状況に関する包括的な情報を取得するには、各種のテクノロジとツールを組み合わせて使用します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server オペレーティング システムでは、以下のツールでパフォーマンス情報を提供します。  
  
-   タスク マネージャー  
  
-   イベント ビューアー  
  
-   パフォーマンス コンソール  
  
 タスク マネージャーは、コンピューター上で現在実行されているプログラムおよびプロセスに関する情報を提供します。 タスク マネージャーを使用することで、レポート サーバーのパフォーマンスに関する重要な指標を監視することができます。 また、実行中のプロセスの利用状況を査定したり、CPU やメモリの使用状況に関するグラフやデータを参照することもできます。 タスク マネージャーの使用方法については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の製品マニュアルを参照してください。  
  
 パフォーマンス コンソールとイベント ビューアーは、レポートの処理やリソースの消費に関するログおよび警告を作成する際に使用できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で生成される Windows イベントの詳細については、「 [Windows アプリケーション ログ](../../reporting-services/report-server/windows-application-log.md)」を参照してください。 パフォーマンス コンソールの詳細については、この記事で後述する「Windows パフォーマンス カウンター」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでは、キャッシュおよびセッション管理に使用するレポート サーバー データベースと一時データベースに関する情報も提供されます。  
  
## <a name="windows-performance-counters"></a>Windows パフォーマンス カウンター  
 個々のパフォーマンス カウンターを監視することで、次のことが可能になります。  
  
-   予測される負荷をサポートするために必要なシステム要件を算出する。  
  
-   構成の変更やアプリケーションのアップグレードの影響を測定するために、パフォーマンスのベースラインを作成する。  
  
-   実際の負荷、または人為的に生成した負荷の下で、アプリケーションのパフォーマンスを監視する。  
  
-   ハードウェアのアップグレードがパフォーマンスに所定の効果をもたらしたかどうかを検証する。  
  
-   システム構成の変更がパフォーマンスに所定の効果をもたらしたかどうかを検証する。  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="reporting-services-performance-objects"></a>Reporting Services パフォーマンス オブジェクト  
SQL Server 2016 Reporting Services またはそれ以降 (SSRS) は、次のパフォーマンス オブジェクトが含まれています。  
  
-   レポート サーバーのパフォーマンスを監視するための**MSRS 2011 Web Service** および **MSRS 2011 SharePoint Mode Web Service** 。 これらのパフォーマンス オブジェクトには複数のカウンターが含まれ、主に対話的なレポート表示操作によって開始されるレポート サーバー処理の追跡に使用されます。 これらのカウンターは、 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] がレポート サーバー Web サービスを停止した時点でリセットされます。  
  
-   スケジュール設定した操作、およびレポートの配信を監視するための**MSRS 2011 Windows Service** および **MSRS 2011 Windows Service SharePoint Mode** to monitor scheduled operations および report delivery. これらのパフォーマンス オブジェクトには複数のカウンターが含まれ、スケジュールされた操作を介して開始されるレポート処理の追跡に使用されます。 スケジュールされた操作には、サブスクリプションと配信、レポート実行スナップショット、およびレポート履歴が含まれます。  
  
-   HTTP 関連のイベントおよびメモリ管理を監視するための **ReportServer サービス**および **ReportServerSharePoint サービス**。 これらは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に固有のカウンターです。要求、接続、サインイン試行など、レポート サーバーにおける HTTP 関連のイベントが追跡されます。 このパフォーマンス オブジェクトには、メモリ管理に関連したカウンターも含まれています。  
  
 1 台のコンピューターに複数のレポート サーバー インスタンスが存在する場合、インスタンスをまとめて監視することも個別に監視することもできます。 カウンターを追加する場合は、監視対象に含めるインスタンスを選択してください。 パフォーマンス コンソール (perfmon.msc) の使用およびカウンターの追加に関する詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の製品マニュアルを参照してください。  
  
## <a name="other-performance-counters"></a>その他のパフォーマンス カウンター  
 **MSRS 2008 Web Service**、**MSRS 2008 Windows Service**、および **ReportServer サービス**専用に、カスタムの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] パフォーマンス カウンターが用意されています。 次のパフォーマンス オブジェクトにより、レポート サーバーに関する補足的なパフォーマンス監視データが提供されます。  
  
|パフォーマンス オブジェクト|注|  
|------------------------|-----------|  
|**.NET CLR データ** および **.NET CLR メモリ**|Web ポータルを使用して[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]パフォーマンス カウンター。 詳細については、MSDN の「Improving .NET Application Performance and Scalability」を参照してください。|  
|**[処理]**|ReportingServicesService のインスタンスでプロセス ID ごとの稼働時間を追跡するための **Elapsed Time** および **ID Process** パフォーマンス カウンターを追加します。|  
  
## <a name="sharepoint-events"></a>SharePoint のイベント  
 レポート サーバーを SharePoint 統合モードで実行しており、SharePoint 製品を使用するようにレポート環境を構成している場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のパフォーマンス オブジェクトだけでなく、SharePoint のイベントを構成することもできます。 このセクションでは、「SharePoint 統合モードにおけるレポート サーバーのイベント」を基に、SharePoint と統合されたレポート環境で役立てることのできる診断イベントについて確認します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [MSRS 2011 Web Service と MSRS 2011 Windows Service パフォーマンス オブジェクトのパフォーマンス カウンター (ネイティブ モード)](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)  
 レポート サーバー Web サービスで使用するパフォーマンス カウンターについて説明します。  
  
 [MSRS 2011 Web Service SharePoint Mode と MSRS 2011 Windows Service SharePoint Mode パフォーマンス オブジェクトのパフォーマンス カウンター &#40;SharePoint モード&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 レポート サーバー Windows サービスで使用するパフォーマンス カウンターについて説明します。  
  
 [ReportServer:Service と ReportServerSharePoint:Service パフォーマンス オブジェクトのパフォーマンス カウンター](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]における HTTP およびメモリに関連したパフォーマンス カウンターについて説明します。  

::: moniker-end
  
## <a name="see-also"></a>参照  
 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)  
  