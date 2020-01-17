---
title: 'Always On 可用性グループ: 相互運用性'
description: Always On 可用性グループと共に使用できる機能および使用できない機能について説明します。
ms.custom: seodec18
ms.date: 04/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f42630e101a60c9d3265ab96a5b126551eeaff0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991589"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Always On 可用性グループ: 相互運用性 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このトピックでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能との間の [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の相互運用性について説明します。

## <a name="Interop"></a> Always On 可用性グループと相互運用可能な機能

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] と相互運用可能な [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]機能を次の表に示します。 **詳細情報** 列のリンクは、特定の機能に関して相互運用性に関する考慮事項が存在することを示します。

|機能|詳細情報|
|:------|:---------------|
|変更データ キャプチャ|[レプリケーション、変更の追跡、変更データ キャプチャ、および Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|変更の追跡|[レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|包含データベース|[包含データベースと Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|
|データベース暗号化|[暗号化されたデータベースと Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|
|データベース スナップショット|[Always On 可用性グループを含むデータベース スナップショット &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|
|FILESTREAM と FileTable|[FILESTREAM および FileTable と Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|
|フルテキスト検索|注:フルテキスト インデックスは、Always On セカンダリ データベースと同期されます。|
|ログ配布|[ログ配布から Always On 可用性グループへの移行の前提条件 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|
|リモート BLOB ストア (RBS)|[リモート BLOB ストア &#40;RBS&#41; と Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|
|レプリケーション|[Always On 可用性グループ用のレプリケーションの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Always On パブリケーション データベースのメンテナンス &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [レプリケーション、変更の追跡、変更データ キャプチャ、および Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [レプリケーション サブスクライバーと Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|
|Analysis Services|[Analysis Services と Always On 可用性グループ](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|
|Reporting Services|読み取り専用セカンダリ レプリカをレポート データ ソースとして使用し、読み取り/書き込み可能なプライマリ レプリカの負荷を軽減します。<br /><br /> [Reporting Services と Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|
|Service Broker|[Service Broker と Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|
|SQL Server エージェント|&nbsp;|

## <a name="restrictions"></a> 制限付きの Always On 可用性グループと相互運用可能な機能

次の機能は、特定の制限付きで [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] と相互運用します。 詳細については、リンク先のトピックを参照してください。

- データベースをまたがるトランザクション/分散トランザクション ([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] と Windows Server 2016)。 詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。
- 読み取り不可のセカンダリがある環境では、[クエリ統計システム データ コレクター](../../../relational-databases/data-collection/system-data-collection-set-reports.md#Query)を確実に実行することができません。 クエリ統計システム データ コレクターを使用するには、[読み取りアクセス](configure-read-only-access-on-an-availability-replica-sql-server.md)を許可するように、可用性グループのセカンダリ レプリカを設定してください。 

## <a name="NoInterop"></a> Always On 可用性グループと相互運用不可能な機能

[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、次の機能との相互運用はできません。

- データベース ミラーリング 詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。

## <a name="RelatedContent"></a> 関連コンテンツ

- **ブログ:**

  [移行ガイド: 以前のクラスタリングおよびミラーリングの展開による SQL Server 2012 フェールオーバークラスタリングおよび可用性グループへの移行](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)
  [SQL Server Always On チームのブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)
  [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)

- **ホワイト ペーパー:**

  [移行ガイド: 以前の配置の結合データベース ミラーリングとログ配布から Always On 可用性グループに移行する](https://msdn.microsoft.com/library/jj635217)
  [高可用性とディザスター リカバリーのための Microsoft SQL Server Always On ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)
  [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)
  [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)

## <a name="see-also"></a>参照

[AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)
