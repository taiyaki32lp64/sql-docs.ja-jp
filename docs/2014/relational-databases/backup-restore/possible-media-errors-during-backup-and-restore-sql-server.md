---
title: バックアップ中および復元中に発生する可能性があるメディア エラー (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46b9fef97433609310169c98d8ffc623a21a10c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876116"
---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>バックアップ中および復元中に発生する可能性があるメディア エラー (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、エラーが検出されてもデータベースを復旧するオプションを選択できるようになりました。 エラー検出の重要なメカニズムとして、バックアップ チェックサムを任意で作成できるようになりました。バックアップ チェックサムは、バックアップ操作で生成して、復元操作で検証できます。 操作中にエラーを検出するかどうかと、エラー発生時に操作を停止するか続行するかを制御できます。 バックアップにバックアップ チェックサムが含まれている場合、RESTORE ステートメントおよび RESTORE VERIFYONLY ステートメントでエラーを検査できます。  
  
> [!NOTE]  
>  ミラー化バックアップでは、メディア セットのコピー (ミラー) が最大で 4 つ作成され、メディアの破損によるエラーから復旧するために使用する代替コピーが提供されます。 詳細については、「 [Mirrored Backup Media Sets &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)」を参照してください。  
  
  
  
##  <a name="BckChecksums"></a> バックアップ チェックサム  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているチェックサムは、ページ チェックサム、ログ ブロック チェックサム、およびバックアップ チェックサムの 3 種類です。 バックアップ チェックサムの生成時には、データベースから読み取ったデータについて、データベース内に存在するチェックサムや破損ページ情報との整合性が BACKUP によって検証されます。  
  
 BACKUP ステートメントではオプションで、バックアップ ストリームのバックアップ チェックサムを計算できます。特定のページにページ チェックサムまたは破損ページ情報がある場合、ページのバックアップ時に、そのページのチェックサムおよび破損ページの状態とページ ID も検証されます。 バックアップ操作でバックアップ チェックサムを作成する際に、チェックサムがページに追加されることはありません。 ページはデータベースに存在するままの状態でバックアップされます。バックアップでページは変更されません。  
  
 バックアップ チェックサムを使用すると、検証および生成の際のオーバーヘッドによって、パフォーマンスに影響を及ぼす可能性があります。 影響はワークロードおよびバックアップ スループットの両方に及ぶ場合があります。 このため、バックアップ チェックサムの使用は任意です。 バックアップ時にチェックサムを生成する場合は、システムで進行中のワークロードへの影響だけでなく、発生する CPU オーバーヘッドも注意深く監視してください。  
  
 BACKUP を実行してもディスク上の元のページおよびページの内容は変更されません。  
  
 バックアップ チェックサムを有効にすると、バックアップ操作では、次の手順が実行されます。  
  
1.  ページをバックアップ メディアに書き込む前に、ページ レベルの情報が検証されます (ページ チェックサムまたは破損ページ検出のいずれかが存在する場合)。 いずれの情報も存在しない場合は、ページを検証できません。 未検証のページはそのまま書き込まれ、内容が全体のバックアップ チェックサムに追加されます。  
  
     検証中にページ エラーが検出された場合、バックアップは失敗します。  
  
    > [!NOTE]  
    >  ページ チェックサムおよび破損ページ検出の詳細については、ALTER DATABASE ステートメントの PAGE_VERIFY オプションを参照してください。 詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)」を参照してください。  
  
2.  ページ チェックサムが存在するかどうかに関係なく、BACKUP によってバックアップ ストリームに個別のバックアップ チェックサムが生成されます。 復元操作でバックアップ チェックサムを使用し、バックアップが破損していないかどうかを検証することもできます。 バックアップ チェックサムは、データベース ページにではなくバックアップ メディアに格納されます。 バックアップ チェックサムは、復元時に使用することもできます。  
  
3.  バックアップ セットは ( **msdb..backupset** の **has_backup_checksums**列に) バックアップ チェックサムがあるものとしてフラグが付けられます。 詳細については、「 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)」を参照してください。  
  
 復元操作中、バックアップ メディアにバックアップ チェックサムがある場合、既定では RESTORE ステートメントと RESTORE VERIFYONLY ステートメントの両方でバックアップ チェックサムとページ チェックサムが検証されます。 バックアップ チェックサムがない場合、いずれの復元操作も検証が行われずに続行されます。これは、バックアップ チェックサムがないと、ページ チェックサムの検証を確実に実行できないためです。  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>バックアップまたは復元操作中のページ チェックサム エラーへの応答  
 既定では、ページ チェックサム エラーが発生した後、BACKUP 操作または RESTORE 操作は失敗し、RESTORE VERIFYONLY 操作が続行されます。 ただし、エラー発生時に特定の操作を失敗させるか、できる限り続行させるかを制御できます。  
  
 エラー発生後に BACKUP 操作を続行する場合は、次の手順が実行されます。  
  
1.  バックアップ メディア上のバックアップ セットに対し、エラーが存在するというフラグを設定し、**msdb** データベースの **suspect_pages** テーブルでそのページを追跡します。 詳細については、「[suspect_pages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/suspect-pages-transact-sql)」を参照してください。  
  
2.  SQL Server エラー ログにエラーを記録します。  
  
3.  バックアップ セットに対し、この種類のエラーが存在するというマークを ( **msdb.backupset** の **is_damaged**列に) 付けます。 詳細については、「 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)」を参照してください。  
  
4.  正常にバックアップが生成されたがページ エラーが含まれていることを示すメッセージを表示します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **バックアップ チェックサムを有効または無効にするには**  
  
-   [バックアップ中または復元中にバックアップ チェックサムを有効または無効にする &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **バックアップ操作中のエラーへの応答を制御するには**  
  
-   [バックアップまたは復元の操作をエラー発生後に続行するか停止するかを指定する &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [Mirrored Backup Media Sets &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  
