---
title: 高可用性 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfa0548bc526b007c4301572cd1a8e47a2851e18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109022"
---
# <a name="high-availability-reporting-services"></a>高可用性 (Reporting Services)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーは、アプリケーションのデータ、コンテンツ、プロパティ、およびセッション情報を 2 つの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] リレーショナル データベースに格納するステートレス サーバーです。 したがって、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の可用性を確保するには、次のことを検討する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] の高可用性機能を使用して、レポート サーバー データベースの稼働時間を最大限に保つ。 [!INCLUDE[ssDE](../includes/ssde-md.md)] インスタンスをフェールオーバー クラスターで実行するように構成した場合、そのインスタンスをレポート サーバー データベースの作成時に選択できます。  
  
-   できるだけ、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)]を、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] データベースと共に、またデータ ソース用に使用する。 詳細については、「[Reporting Services with AlwaysOn Availability Groups (SQL Server)](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)」(Reporting Services と AlwaysOn 可用性グループ (SQL Server)) を参照してください。  
  
-   複数のレポート サーバーをスケールアウト配置で実行するように構成する。この場合、すべてのサーバーは単一のレポート サーバー データベースを共有することになります。 複数のレポート サーバー インスタンスを (可能であれば異なるサーバーに) スケールアウト配置することにより、いずれかのレポート サーバー インスタンスがダウンした場合でも、サービスの中断を効果的に防ぐことができます。  
  
 スケールアウト配置により、データベースの共有が可能となります。 どれか 1 つのレポート サーバーがダウンしても、同じ配置内の他のサーバーが処理を続行します。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] はクラスターに対応していません。 スケールアウト配置自体は負荷分散機能を備えていないため、レポート サーバーの処理負荷を検出したり、新しい処理要求を最も負荷の低いサーバーにルーティングしたりすることはできません。 エラーが発生して完了しなかった処理要求が再ルーティングされることもありません。 負荷分散機能を実現するためには、レポート サーバーをホストする Web サーバーに対して負荷分散を構成し、それらのレポート サーバーが同じレポート サーバー データベースを共有するようにスケールアウト配置で構成する必要があります。  
  
 レポート サーバーの Web サービスと Windows サービスは単一のレポート サーバー インスタンスとして緊密に統合され、互いに連携して動作します。 どちらか一方のサービスに対して個別に可用性を構成することはできません。  
  
## <a name="see-also"></a>関連項目  
 [高可用性ソリューション &#40;SQL Server&#41;](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
