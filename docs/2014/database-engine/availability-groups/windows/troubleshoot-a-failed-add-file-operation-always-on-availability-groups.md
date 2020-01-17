---
title: ファイル追加失敗の操作 (AlwaysOn 可用性グループ) のトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6940e9e40a09e5bd0c7afc591b34c17129350d74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813442"
---
# <a name="troubleshoot-a-failed-add-file-operation-alwayson-availability-groups"></a>失敗したファイルの追加操作のトラブルシューティング (AlwaysOn 可用性グループ)
  一部の AlwaysOn 可用性グループの配置では、プライマリ レプリカをホストするシステムとセカンダリ レプリカをホストするシステムのファイル パスが異なります。 ファイルの追加操作のファイル パスがセカンダリ レプリカ上に存在しない場合でも、プライマリ データベース上でのファイルの追加操作は成功します。 ただし、そのようなファイルの追加操作を行うと、セカンダリ データベースが中断します。 セカンダリ データベースが中断すると、セカンダリ レプリカが NOT SYNCHRONIZING 状態になります。  
  
> [!NOTE]  
>  可能であれば、特定のセカンダリ データベースのファイル パス (ドライブ文字を含む) は、対応するプライマリ データベースのパスと一致させることをお勧めします。  
  
## <a name="problem-resolution"></a>問題の解決策  
 この問題を解決するには、データベース所有者が次の手順を実行する必要があります。  
  
1.  セカンダリ データベースを可用性グループから削除します。 詳細については、「[可用性グループからのセカンダリ データベースの削除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)」を参照してください。  
  
2.  既存のセカンダリ データベースで、WITH NORECOVERY と WITH MOVE (セカンダリ レプリカをホストするサーバー インスタンス上のファイル パスを指定) を使用して、セカンダリ データベースに追加されたファイルを含むファイル グループの完全バックアップを復元します。 詳細については、「[データベースを新しい場所に復元する &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)」を参照してください。  
  
3.  ファイルの追加操作を含むトランザクション ログをプライマリ データベースでバックアップし、WITH NORECOVERY と WITH MOVE を使用して、そのログ バックアップをセカンダリ データベースに手動で復元します。  
  
4.  可用性グループに再度参加させるセカンダリ データベースを準備します。これは、プライマリ データベースでバックアップした他の未処理のログを、WITH NO RECOVERY で復元することによって行います。  
  
5.  セカンダリ データベースを可用性グループに再度参加させます。 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティングを行う&#40;SQL Server&#41;削除](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
