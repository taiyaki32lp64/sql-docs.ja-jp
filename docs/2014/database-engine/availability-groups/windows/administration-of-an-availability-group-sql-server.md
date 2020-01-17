---
title: 可用性グループの管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8d826201f44bb666050f5229b4824b5c2198dc0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75229004"
---
# <a name="administration-of-an-availability-group-sql-server"></a>可用性グループの管理 (SQL Server)
  
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] の既存の AlwaysOn 可用性グループの管理には、次のタスクが 1 つ以上含まれます。  
  
-   既存の可用性レプリカのプロパティを変更する。たとえば、読み取り可能なセカンダリ レプリカを構成するためにクライアント接続アクセスを変更する場合は、フェールオーバー モード、可用性モード、またはセッション タイムアウトの設定を変更します。  
  
-   セカンダリ レプリカを追加または削除する。  
  
-   データベースを追加または削除する。  
  
-   データベースを中断または再開する。  
  
-   計画的な手動フェールオーバー ( *手動フェールオーバー*) または強制手動フェールオーバー ( *強制フェールオーバー*) を実行する。  
  
-   可用性グループ リスナーを作成または構成する。  
  
-   可用性グループの [読み取り可能なセカンダリ レプリカ](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) を管理する。 セカンダリ ロールで実行されているときに読み取り専用アクセスを行うように 1 つ以上のレプリカを構成し、読み取り専用ルーティングを構成する必要があります。  
  
-   可用性グループの [セカンダリ レプリカでのバックアップ](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) を管理する。 バックアップ ジョブを優先的に実行する場所を構成し、バックアップ設定を実装するためにバックアップ ジョブのスクリプトを作成する必要があります。 可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のすべてのインスタンスで、可用性グループの各データベースのバックアップ ジョブのスクリプトを作成する必要があります。  
  
-   可用性グループを削除する。  
  
-   OS アップグレードのための AlwaysOn 可用性グループのクラスター間での移行  
  
  
##  <a name="RelatedTasks"></a>関連タスク  
 **既存の可用性グループを構成するには**  
  
-   [セカンダリレプリカを可用性グループ &#40;SQL Server に追加&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからセカンダリレプリカを削除する &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [可用性グループにデータベースを追加 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [可用性グループからセカンダリデータベースを削除する &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [可用性グループからのプライマリデータベースの削除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [自動フェールオーバー &#40;AlwaysOn 可用性グループの条件を制御する柔軟なフェールオーバーポリシーを構成&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **可用性グループを管理するには**  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [可用性グループ &#40;SQL Server の計画的な手動フェールオーバーを実行&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [可用性グループ &#40;SQL Server の強制手動フェールオーバーを実行&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [可用性グループ &#40;SQL Server の削除&#41;](remove-an-availability-group-sql-server.md)  
  
 **可用性レプリカを管理するには**  
  
-   [セカンダリレプリカを可用性グループ &#40;SQL Server に追加&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [セカンダリレプリカを可用性グループに参加させる &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからセカンダリレプリカを削除する &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [可用性レプリカの可用性モードを変更する &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのフェールオーバーモードを変更する &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [可用性レプリカの読み取り専用アクセスを構成する &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [可用性レプリカのセッションタイムアウト期間を変更する &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **可用性データベースを管理するには**  
  
-   [可用性グループにデータベースを追加 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [セカンダリデータベースを可用性グループに参加させる &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからのプライマリデータベースの削除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [可用性グループからセカンダリデータベースを削除する &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [可用性データベース &#40;SQL Server を中断&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [可用性データベース &#40;SQL Server の再開&#41;](resume-an-availability-database-sql-server.md)  
  
 **可用性グループを監視するには**  
  
-   [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
 **新しい WSFC クラスターへの可用性グループの移行 (クラスター間の移行) をサポートするには**  
  
-   [サーバーインスタンスの HADR クラスターコンテキストを変更する &#40;SQL Server&#41;](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [可用性グループをオフラインにする &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   **Blog**  
  
     [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ**  
  
     [Microsoft SQL Server コード ネーム "Denali" AlwaysOn シリーズ パート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" AlwaysOn シリーズ パート 2: AlwaysOn を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイトペーパー:**  
  
     [SQL Server 2012 の Microsoft ホワイトペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server カスタマーアドバイザリチームのホワイトペーパー](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server のサーバーインスタンスの構成&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [アクティブなセカンダリ: 読み取り可能なセカンダリレプリカ &#40;AlwaysOn 可用性グループ&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [アクティブなセカンダリ: セカンダリレプリカでのバックアップ &#40;AlwaysOn 可用性グループ&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [可用性グループリスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server での運用上の問題のための AlwaysOn ポリシー&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ: 相互運用性 &#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の Transact-sql ステートメントの概要&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の PowerShell コマンドレットの概要&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
