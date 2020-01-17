---
title: 可用性グループのファイルの追加操作の失敗
decription: Possible resolutions for failing to add a file to an availability group.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1655992526096035eb109821d8950980921951ad
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251226"
---
# <a name="troubleshoot-a-failed-add-file-operation-always-on-availability-groups"></a>失敗したファイルの追加操作のトラブルシューティング (AlwaysOn 可用性グループ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  一部の AlwaysOn 可用性グループの配置では、プライマリ レプリカをホストするシステムとセカンダリ レプリカをホストするシステムのファイル パスが異なります。 ファイルの追加操作のファイル パスがセカンダリ レプリカ上に存在しない場合でも、プライマリ データベース上でのファイルの追加操作は成功します。 ただし、そのようなファイルの追加操作を行うと、セカンダリ データベースが中断します。 セカンダリ データベースが中断すると、セカンダリ レプリカが NOT SYNCHRONIZING 状態になります。  
  
> [!NOTE]  
>  可能であれば、特定のセカンダリ データベースのファイル パス (ドライブ文字を含む) は、対応するプライマリ データベースのパスと一致させることをお勧めします。  
  
## <a name="problem-resolution"></a>問題解決  
 この問題を解決するには、データベース所有者が次の手順を実行する必要があります。  
  
1.  セカンダリ データベースを可用性グループから削除します。 詳細については、「[可用性グループからのセカンダリ データベースの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)」をご覧ください。  
  
2.  既存のセカンダリ データベースで、WITH NORECOVERY と WITH MOVE (セカンダリ レプリカをホストするサーバー インスタンス上のファイル パスを指定) を使用して、セカンダリ データベースに追加されたファイルを含むファイル グループの完全バックアップを復元します。 詳細については、「[データベースを新しい場所に復元する &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)」を参照してください。  
  
3.  ファイルの追加操作を含むトランザクション ログをプライマリ データベースでバックアップし、WITH NORECOVERY と WITH MOVE を使用して、そのログ バックアップをセカンダリ データベースに手動で復元します。  
  
4.  可用性グループに再度参加させるセカンダリ データベースを準備します。これは、プライマリ データベースでバックアップした他の未処理のログを、WITH NO RECOVERY で復元することによって行います。  
  
5.  セカンダリ データベースを可用性グループに再度参加させます。 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)
