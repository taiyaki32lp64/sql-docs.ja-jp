---
title: スケーラビリティ | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2762e024f3a94ed20c900833e56840b67af1685d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111780"
---
# <a name="scalability"></a>スケーラビリティ
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] では、メモリ最適化テーブル用のディスク上ストレージに対するスケーラビリティ機能が強化されています。 

## <a name="multiple-threads-to-persist-memory-optimized-tables"></a>メモリ最適化テーブルを保持する複数のスレッド  
  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] には、メモリ最適化テーブルへの変更についてトランザクション ログをスキャンし、メモリ最適化テーブルをチェックポイント ファイル (データ ファイルや差分ファイルなど) に保持する 1 つのオフライン チェックポイント スレッドがありました。 コア数が多いコンピューターの場合、1 つのオフライン チェックポイント スレッドでは処理が遅れることがありました。  
  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、メモリ最適化テーブルへの変更を保持する複数の同時実行スレッドがあります。  
  
## <a name="multi-threaded-recovery"></a>マルチ スレッドの回復
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のリリースでは、回復操作の一環としてのログ適用がシングル スレッド化されていました。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、ログ適用はマルチ スレッドです。  
  
## <a name="merge-operation"></a>MERGE 操作  
MERGE 操作はマルチ スレッドになりました。  
   
> [!NOTE]
> マルチ スレッドのマージは負荷に応じて実行されるため、手動マージは無効になっています。 

## <a name="dynamic-management-views"></a>動的管理ビュー  
DMV の [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) と [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) が大幅に変更されました。  

## <a name="storage-management"></a>記憶域の管理
インメモリ OLTP エンジンは FILESTREAM に基づくメモリ最適化ファイル グループを引き続き使用しますが、ファイル グループ内の個々のファイルは FILESTREAM から切り離されています。 これらのファイルは、インメモリ OLTP エンジンによってフル マネージドです (作成、削除、ガベージ コレクションなど)。 

> [!NOTE]
> [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) はサポートされていません。  
  
## <a name="see-also"></a>参照   
[メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)     
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[ALTER DATABASE の File および Filegroup オプション (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)    
