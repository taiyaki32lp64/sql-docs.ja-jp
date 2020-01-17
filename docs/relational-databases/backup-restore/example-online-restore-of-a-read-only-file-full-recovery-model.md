---
title: 'オンライン復元: 読み取り専用ファイル (完全復旧モデル)'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 7ea2d2af-086f-48dc-9636-38dc194c7090
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 545a3cfe319732ca7cb0f9d5a51b1e172072e636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75227965"
---
# <a name="example-online-restore-of-a-read-only-file-full-recovery-model"></a>例:読み取り専用ファイルのオンライン復元 (完全復旧モデル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックは、複数のファイルやファイル グループを含む、完全復旧モデルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに関連しています。  
  
 この例では、完全復旧モデルを使用する `adb`というデータベースに 3 つのファイル グループが含まれているとします。 ファイル グループ `A` は読み取り/書き込みが可能で、ファイル グループ `B` とファイル グループ `C` は読み取り専用です。 最初は、すべてのファイル グループがオンラインです。  
  
 データベース `b1`のファイル グループ `B` に含まれている読み取り専用ファイル `adb` を復元する必要があります。 ファイルが読み取り専用になってからバックアップを行ったので、ログ バックアップは不要です。 復元の間、ファイル グループ `B` はオフラインになりますが、データベースの残りの部分はオンライン状態で維持されます。  
  
## <a name="restore-sequence"></a>復元シーケンス  
  
> [!NOTE]  
>  オンライン復元シーケンスでは、オフライン復元シーケンスと同じ構文を使用します。  
  
 ファイルを復元するには、データベース管理者が次の復元シーケンスを使用する必要があります。  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup  
WITH RECOVERY   
```  
  
 ファイル B がオンラインになります。  
  
## <a name="additional-examples"></a>その他の例  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: データベースの段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
## <a name="see-also"></a>参照  
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
