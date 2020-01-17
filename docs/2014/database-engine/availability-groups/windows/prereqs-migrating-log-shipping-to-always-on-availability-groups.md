---
title: AlwaysOn 可用性グループ (SQL Server) のログ配布を移行する前提条件 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 865e8d720e9977f582ac5ae8a0e75d995fc82629
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789557"
---
# <a name="prerequisites-for-migrating-from-log-shipping-to-alwayson-availability-groups-sql-server"></a>ログ配布から AlwaysOn 可用性グループへの移行の前提条件 (SQL Server)
  このトピックでは、ログ配布プライマリ データベースと 1 つまたは複数のセカンダリ データベースを、AlwaysOn プライマリ データベースとセカンダリ データベースに変換するための前提条件について説明します。  
  
> [!NOTE]  
>  可用性グループのプライマリまたはセカンダリ データベース (場合によっては読み取り可能) は、ログ配布プライマリ データベースとして構成できます。  
  
 **このトピックの内容**  
  
-   [可用性グループの前提条件](#AGPrereqsRealAddress)  
  
-   [ログ配布の前提条件](#LogShipPrereqs)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a> 可用性グループの前提条件  
 バックアップ ジョブを可用性グループのプライマリ レプリカ上で実行できるようにするには、AlwaysOn 可用性グループの次のバックアップ設定を使用します。  
  
|プロパティ|設定|  
|--------------|-------------|  
|可用性グループの自動バックアップ設定|[プライマリ レプリカ上のみ]|  
|プライマリ レプリカのバックアップの優先順位。|>0|  
  
 **詳細:**  
  
 [可用性グループのプロパティの表示 &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
 [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> ログ配布の前提条件  
  
-   ログ配布プライマリ データベースは、可用性グループの初期/現在のプライマリ レプリカをホストしている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに存在している必要があります。  
  
-   AlwaysOn セカンダリ データベースに変換するには、ログ配布セカンダリ データベースは次の条件を満たしている必要があります。  
  
    -   プライマリ データベースと同じ名前を使用している。  
  
    -   可用性グループのセカンダリ レプリカをホストしているサーバー インスタンスに存在している。  
  
 バックアップ ジョブをプライマリ データベース上で実行した後は、バックアップ ジョブを無効にし、復元ジョブを特定のセカンダリ データベース上で実行した後は、復元ジョブを無効にします。  
  
 可用性グループのすべてのセカンダリ データベースを作成した後、セカンダリ レプリカにバックアップを実行する場合は、可用性グループの自動バックアップ設定を再構成する必要があります。  
  
 **詳細:**  
  
 [可用性グループへのログ配布構成の変換](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx) (SQL Server ブログ)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **ログ配布**  
  
-   [SQL Server 2014 へのログ配布のアップグレード&#40;TRANSACT-SQL&#41;](../../log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [ログ配布の削除 &#40;SQL Server&#41;](../../log-shipping/remove-log-shipping-sql-server.md)  
  
 **AlwaysOn 可用性グループ**  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループの作成 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [可用性グループへのログ配布構成の変換](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx)  
  
     [Add a Log Shipping Primary Database and Secondary Database(s) to an Existing Availability Group](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/01/use-log-shipping-to-prepare-secondary-databases-for-an-existing-availability-group.aspx)  
  
     [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [移行ガイド: AlwaysOn 可用性グループへの移行前の配置の結合データベース ミラーリングとログ配布から](https://msdn.microsoft.com/library/jj635217)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../log-shipping/about-log-shipping-sql-server.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
