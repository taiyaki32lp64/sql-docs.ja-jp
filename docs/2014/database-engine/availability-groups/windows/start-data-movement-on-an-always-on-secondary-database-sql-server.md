---
title: AlwaysOn セカンダリ データベース (SQL Server) 上のデータ移動の開始 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], databases
ms.assetid: 498eb3fb-6a43-434d-ad95-68a754232c45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0626ce7dee34ed21aad3e902e3c3f555f27ab97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813558"
---
# <a name="start-data-movement-on-an-alwayson-secondary-database-sql-server"></a>AlwaysOn セカンダリ データベース上のデータ移動の開始 (SQLServer)
  このトピックでは、AlwaysOn 可用性グループにデータベースを追加した後、データの同期を開始する方法について説明します。 新しい各プライマリ レプリカに対して、セカンダリ レプリカをホストするサーバー インスタンス上でセカンダリ データベースを準備する必要があります。 その後、各セカンダリ データベースを手動で可用性グループに参加させる必要があります。  
  
> [!NOTE]  
>  可用性グループの可用性レプリカをホストするすべてのサーバー インスタンス上のファイル パスが同じである場合は、 [新しい可用性グループ ウィザード](use-the-availability-group-wizard-sql-server-management-studio.md)、 [可用性グループへのレプリカ追加ウィザード](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)、または [可用性グループへのデータベース追加ウィザード](availability-group-add-database-to-group-wizard.md) を使用してデータ同期を自動的に開始できます。  
  
 データ同期を手動で開始するには、可用性グループのセカンダリ レプリカをホストする各サーバー インスタンスに接続し、次の手順を実行する必要があります。  
  
1.  各プライマリ データベースとそのトランザクション ログの最新のバックアップを復元します (RESTORE WITH NORECOVERY を使用)。 次のいずれかの代替方法を使用できます。  
  
    -   RESTORE WITH NORECOVERY を使用してプライマリ データベースの最新のデータベース バックアップを手動で復元し、その後、RESTORE WITH NORECOVERY を使用して後続のログ バックアップを復元する。 可用性グループのセカンダリ レプリカをホストする各サーバー インスタンスで、この復元シーケンスを実行します。  
  
         **詳細:**  
  
         [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
    -   可用性グループに 1 つ以上のログ配布プライマリ データベースを追加する場合は、対応する 1 つ以上のセカンダリ データベースをログ配布から AlwaysOn 可用性グループに移行できる場合があります。 ログ配布セカンダリ データベースを移行するには、それがプライマリ データベースと同じデータベース名を使用していて、可用性グループのセカンダリ レプリカをホストしているサーバー インスタンス上に存在している必要があります。 さらに、可用性グループを、プライマリ レプリカがバックアップ用に推奨され、バックアップの実行の候補になるように構成する (つまり、バックアップの優先順位を >0 にする) 必要があります。 バックアップ ジョブをプライマリ データベース上で実行した後は、バックアップ ジョブを無効にし、復元ジョブを特定のセカンダリ データベース上で実行した後は、復元ジョブを無効にする必要があります。  
  
        > [!NOTE]  
        >  可用性グループのすべてのセカンダリ データベースを作成した後、セカンダリ レプリカにバックアップを実行する場合は、可用性グループの自動バックアップ設定を再構成する必要があります。  
  
         **詳細:**  
  
         [AlwaysOn 可用性グループへのログ配布を移行する前提条件&#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
         [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
2.  新しく準備された各セカンダリ データベースを可用性グループにできるだけ早く参加させます。  
  
     **詳細:**  
  
     [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="LaunchWiz"></a> 関連タスク  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
