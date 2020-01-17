---
title: 例:一部のファイル グループのみを復元する段階的な部分復元 (完全復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a3ea7a4c7d9189ace988ef57f25e99d61a4273dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876162"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>例:一部のファイル グループのみを復元する段階的な部分復元 (完全復旧モデル)
  このトピックは、複数のファイルやファイル グループを含む、完全復旧モデルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに関連しています。  
  
 段階的な部分復元シーケンスでは、プライマリ ファイル グループからすべての読み取り/書き込みセカンダリ ファイル グループの順に、ファイル グループ レベルで段階的にデータベースが復元および復旧されます。  
  
 この例では、完全復旧モデルを使用する `adb`というデータベースに 3 つのファイル グループが含まれているとします。 ファイル グループ `A` は読み取り/書き込みが可能で、ファイル グループ `B` とファイル グループ `C` は読み取り専用です。 最初は、すべてのファイル グループがオンラインです。  
  
 データベース `B` のプライマリ ファイル グループとファイル グループ `adb` が破損しているようです。 プライマリ ファイル グループは比較的サイズが小さいので、すぐに復元できます。 データベース管理者は、段階的な部分復元シーケンスを使用して、これらのファイル グループを復元することにしました。 まず、プライマリ ファイル グループと後続のトランザクション ログを復元し、データベースを復旧します。  
  
 変更されていないファイル グループ `A` と `C` には重要なデータが含まれています。 そのため、次にこれらのファイル グループをできるだけ早く復元して、オンラインにします。 最後に、破損したセカンダリ ファイル グループ `B`を復元および復旧します。  
  
## <a name="restore-sequences"></a>復元シーケンス  
  
> [!NOTE]  
>  オンライン復元シーケンスでは、オフライン復元シーケンスと同じ構文を使用します。  
  
1.  データベース `adb`のログ末尾のバックアップを作成します。 データベースの復旧ポイントに対して、破損していないファイル グループ `A` および `C` を最新の状態にするには、この手順が必要です。  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  プライマリ ファイル グループの部分復元を行います。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     この時点では、プライマリ ファイル グループはオンラインです。 ファイル グループ `A`、 `B`、および `C` はオフラインで、これらのファイル グループのファイルは復旧待ち状態です。  
  
3.  ファイル グループ `A` と `C`をオンライン復元します。  
  
     これらのファイル グループのデータは破損していないため、バックアップから復元する必要はありません。ただし、これらのファイル グループをオンラインにするために、復旧する必要があります。  
  
     データベース管理者は、すぐにファイル グループ `A` と `C` を復旧します。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     この時点で、プライマリ ファイル グループ、ファイル グループ `A` 、およびファイル グループ `C` はオンラインです。 ファイル グループ `B` はオフラインで、このファイル グループのファイルは復旧待ち状態のままです。  
  
4.  ファイル グループ `B`をオンライン復元します。  
  
     ファイル グループ `B` のファイルは、これ以降の任意の時点で復元します。  
  
    > [!NOTE]  
    >  ファイル グループ `B` のバックアップは、ファイルをロールフォワードする必要がないように、ファイル グループ B が読み取り専用になってから行います。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
    ```  
  
     すべてのファイル グループがオンラインになります。  
  
## <a name="additional-examples"></a>その他の例  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;単純復旧モデル&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: データベースの段階的な部分復元 &#40;完全復旧モデル&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Online Restore &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [段階的な部分復元 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
