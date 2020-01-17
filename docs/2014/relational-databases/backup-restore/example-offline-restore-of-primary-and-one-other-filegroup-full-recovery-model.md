---
title: 例:オフラインで復元するは、プライマリ サーバーとその他の 1 つのグループ (完全復旧モデル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- offline restores [SQL Server]
- restore sequences [SQL Server], offline
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fec409bf6f391e14dd5e1a2b8b102df2fd00cfd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921757"
---
# <a name="example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model"></a>例:プライマリ ファイル グループと他のファイル グループを 1 つオフラインで復元する (完全復旧モデル)
  このトピックは、複数のファイル グループを含む、完全復旧モデルのデータベースだけに関連しています。  
  
 この例では、 `adb` というデータベースに 3 つのファイル グループが含まれているとします。 ファイル グループ `A` とファイル グループ `C` は読み取り/書き込みが可能で、ファイル グループ `B` は読み取り専用です。 プライマリ ファイル グループとファイル グループ `B` は破損していますが、ファイル グループ `A` とファイル グループ `C` は破損していません。 障害が発生する前は、すべてのファイル グループがオンラインになっていました。  
  
 データベース管理者は、プライマリ ファイル グループとファイル グループ `B`を復元および復旧することにしました。 データベースでは完全復旧モデルを使用しているため、復元を開始する前に、データベースのログ末尾のバックアップを作成する必要があります。 データベースがオンラインになると、ファイル グループ `A` とファイル グループ `C` は自動的にオンラインになります。  
  
> [!NOTE]  
>  オフライン復元シーケンスは、読み取り専用ファイルのオンライン復元の場合に比べ、少ない手順で済みます。 例については、次を参照してください。[例。読み取り専用ファイルのオンライン復元&#40;完全復旧モデル&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)します。 ただし、オフライン復元中は、データベース全体がオフラインになります。  
  
## <a name="tail-log-backup"></a>ログ末尾のバックアップ  
 データベースの管理者は、データベースを復元する前に、ログの末尾をバックアップする必要があります。 データベースが破損しているため、ログ末尾のバックアップを作成するには、NO_TRUNCATE オプションを使用する必要があります。  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 ログ末尾のバックアップは、次の復元シーケンスの最後に適用されます。  
  
## <a name="restore-sequence"></a>復元シーケンス  
 プライマリ ファイル グループとファイル グループ `B`を復元するために、データベース管理者は、次に示すように、PARTIAL オプションを使用せずに復元シーケンスを使用します。  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 復元しないファイルは、自動的にオンラインになります。 これで、すべてのファイル グループがオンラインになります。  
  
## <a name="see-also"></a>関連項目  
 [Online Restore &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](file-restores-full-recovery-model.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
