---
title: Always On 可用性グループのサーバーインスタンスの構成 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3dcd239c782f53ec11970e94f89e5acfac982785
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228814"
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>Always On 可用性グループのためのサーバー インスタンスの構成 (SQL Server)
  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] でサポートするために [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインスタンスを構成する際の要件について説明します。  
  
> [!IMPORTANT]  
>  Windows Server フェールオーバー クラスタリング (WSFC) ノードおよび [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の前提条件と制限に関する基本情報については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 
  
##  <a name="TermsAndDefinitions"></a>用語と定義  
  
 データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューション。 *可用性グループ*は、相互にフェールオーバーされる個別のユーザーデータベース (*可用性データベース*と呼ばれます) のフェールオーバー環境をサポートします。  
  
 可用性グループ  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 4 つの *セカンダリ レプリカ*) があります。 可用性グループの可用性レプリカをホストするサーバー インスタンスは、同じ Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の別のノードにある必要があります。  
  
 [データベースミラーリングエンドポイント](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 エンドポイントとは、SQL Server でネットワーク経由の通信を行うことができるようにする SQL Server オブジェクトです。 データベース ミラーリングおよび [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に参加する場合、サーバー インスタンスには特別な専用のエンドポイントが必要です。 サーバー インスタンスのすべてのミラーリングと可用性グループの接続は、同じデータベース ミラーリング エンドポイントを使用します。 このエンドポイントの用途は特殊で、他のサーバー インスタンスからこれらの接続を受信するためにのみ使用されます。  
  
##  <a name="ConfigSI"></a>AlwaysOn 可用性グループをサポートするようにサーバーインスタンスを構成するには  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートする場合、サーバー インスタンスは、可用性グループをホストする WSFC フェールオーバー クラスター内のノードにあり、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] が有効になっていて、データベース ミラーリング エンドポイントを持っている必要があります。  
  
1.  可用性グループに追加するすべてのサーバー インスタンスの AlwaysOn 可用性グループ機能を有効にします。 特定の可用性グループの特定のサーバー インスタンスがホストできる可用性レプリカは 1 つだけです。  
  
2.  サーバー インスタンスに、データベース ミラーリング エンドポイントが存在することを確認します。  
  
##  <a name="RelatedTasks"></a>関連タスク  
 **AlwaysOn 可用性グループを有効にするには**  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server を有効または無効にする&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **データベースミラーリングエンドポイントが存在するかどうかを確認するには**  
  
-   [database_mirroring_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **データベースミラーリングエンドポイントを作成するには**  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server PowerShell のデータベースミラーリングエンドポイントを作成&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証 &#40;Transact-sql&#41;のデータベースミラーリングエンドポイントを作成する](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベースミラーリングエンドポイントで、Transact-sql&#41;&#40;の送信接続に証明書を使用できるようにする](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   **Blog**  
  
     [AlwaysON - HADRON 学習シリーズ: HADRON 対応データベースのワーカー プールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ**  
  
     [Microsoft SQL Server コード ネーム "Denali" AlwaysOn シリーズ パート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" AlwaysOn シリーズ パート 2: AlwaysOn を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ペーパー**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 の Microsoft ホワイトペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server カスタマーアドバイザリチームのホワイトペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の前提条件、制限事項、推奨事項&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [データベースミラーリングエンドポイント &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性グループ: 相互運用性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [フェールオーバークラスタリングと AlwaysOn 可用性グループ &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Windows Server フェールオーバークラスタリング &#40;WSFC&#41; SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [AlwaysOn フェールオーバークラスターインスタンス](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
