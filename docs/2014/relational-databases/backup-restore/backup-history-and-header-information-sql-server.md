---
title: バックアップの履歴とヘッダーの情報 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup headers [SQL Server]
- history tables [SQL Server]
- file restores [SQL Server], status information
- backup sets [SQL Server], status information
- listing backed up databases
- status information [SQL Server], backups
- backing up [SQL Server], viewing backup sets
- restoring [SQL Server], history tables
- restoring databases [SQL Server], status information
- backups [SQL Server], status information
- headers [SQL Server]
- media headers [SQL Server]
- backup history tables [SQL Server]
- viewing backup information
- restoring files [SQL Server], viewing backup information
- restoring databases [SQL Server], history tables
- displaying backup information
- restoring files [SQL Server], status information
- historical information [SQL Server], backups
- database restores [SQL Server], history tables
- restore history tables [SQL Server]
- listing backed up files
ms.assetid: 799b9934-0ec2-4f43-960b-5c9653f18374
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1ab8545714e84c8ecf8ee6c9cb89b7b8c0d3831
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922240"
---
# <a name="backup-history-and-header-information-sql-server"></a>バックアップの履歴とヘッダーの情報 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースには、サーバー インスタンスで行われた** のすべてのバックアップ操作および復元操作の完全な履歴が格納されます。 このトピックでは、バックアップと復元の履歴テーブルに加え、バックアップ履歴へのアクセスに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントについても説明します。 また、データベース ファイルとトランザクション ログ ファイルの一覧表示が役立つ状況について説明し、メディア ヘッダー情報を使用する状況とバックアップ ヘッダー情報を使用する状況の比較についても説明します。  
  
> [!IMPORTANT]  
>  バックアップと復元の履歴に対する最新の変更情報の損失リスクを管理するために、頻繁に **msdb** をバックアップしてください。 バックアップする必要があるシステム データベースの詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   [バックアップと復元の履歴テーブル](#BnRHistoryTables)  
  
-   [バックアップ履歴にアクセスするための Transact-SQL ステートメント](#TsqlStatementsForBackupHistory)  
  
-   [データベース ファイルとトランザクション ログ ファイル](#ListDbTlogFiles)  
  
-   [メディア ヘッダー情報](#MediaHeader)  
  
-   [バックアップ ヘッダー情報](#BackupHeader)  
  
-   [メディア ヘッダーとバックアップ ヘッダーの情報の比較](#CompareMediaHeaderBackupHeader)  
  
-   [バックアップの検証](#Verification)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BnRHistoryTables"></a> バックアップと復元の履歴テーブル  
 ここでは、 **msdb** システム データベース内のバックアップ メタデータおよび復元メタデータが保存される履歴テーブルについて説明します。  
  
|履歴テーブル|説明|  
|-------------------|-----------------|  
|[backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)|バックアップされるデータ ファイルまたはログ ファイルごとに 1 行のデータを格納します。|  
|[backupfilegroup](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)|バックアップ セットのファイル グループごとに 1 行のデータを格納します。|  
|[backupmediafamily](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)|メディア ファミリごとに 1 行のデータを格納します。 メディア ファミリがミラー化されたメディア セット内にある場合は、メディア セット内のミラーごとに個別の行が格納されます。|  
|[backupmediaset](/sql/relational-databases/system-tables/backupmediaset-transact-sql)|バックアップ メディア セットごとに 1 行のデータを格納します。|  
|[backupset](/sql/relational-databases/system-tables/backupset-transact-sql)|バックアップ セットごとに 1 行のデータを格納します。|  
|[restorefile](/sql/relational-databases/system-tables/restorefile-transact-sql)|復元されたファイルごとに 1 行のデータを格納します。 これには、ファイル グループ名から間接的に復元されたファイルも含まれます。|  
|[restorefilegroup](/sql/relational-databases/system-tables/restorefilegroup-transact-sql)|復元されたファイル グループごとに 1 行のデータを格納します。|  
|[restorehistory](/sql/relational-databases/system-tables/restorehistory-transact-sql)|復元操作ごとに 1 行のデータを格納します。|  
  
> [!NOTE]  
>  復元を実行すると、バックアップ履歴テーブルと復元履歴テーブルが変更されます。  
  
##  <a name="TsqlStatementsForBackupHistory"></a> バックアップ履歴にアクセスするための Transact-SQL ステートメント  
 復元情報ステートメントは、特定のバックアップ履歴テーブルに格納されている情報に対応しています。  
  
> [!IMPORTANT]  
>  RESTORE FILELISTONLY、RESTORE HEADERONLY、RESTORE LABELONLY、および RESTORE VERIFYONLY の各 Transact-SQL ステートメントを実行するために CREATE DATABASE 権限が必要です。 この要件により、以前のバージョンよりも、バックアップ ファイルの安全性が高くなり、バックアップ情報が十分保護されます。 このアクセス許可の詳細については、「[データベースの権限の許可&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql)」を参照してください。  
  
|情報ステートメント|バックアップ履歴テーブル|説明|  
|---------------------------|--------------------------|-----------------|  
|[RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)|[backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)|指定したバックアップ セットに含まれるデータベース ファイルとログ ファイルの一覧を含む結果セットを返します。<br /><br /> 詳細については、このトピックの「データベース ファイルとトランザクション ログ ファイルの一覧表示」を参照してください。|  
|[RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)|[backupset](/sql/relational-databases/system-tables/backupset-transact-sql)|特定のバックアップ デバイス上のすべてのバックアップ セットについて、バックアップ ヘッダーに関するすべての情報を取得します。 RESTORE HEADERONLY を実行して得られる結果は、結果セットです。<br /><br /> 詳細については、このトピックの「バックアップ ヘッダー情報の表示」を参照してください。|  
|[RESTORE LABELONLY](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)|[backupmediaset](/sql/relational-databases/system-tables/backupmediaset-transact-sql)|指定したバックアップ デバイス上のバックアップ メディアに関する情報を含む結果セットを返します。<br /><br /> 詳細については、このトピックの「メディア ヘッダー情報の表示」を参照してください。|  
  
##  <a name="ListDbTlogFiles"></a> データベース ファイルとトランザクション ログ ファイル  
 バックアップ内のデータベース ファイルおよびトランザクション ログ ファイルの一覧を表示すると、論理名、物理名、ファイルの種類 (データベースまたはログ)、ファイル グループのメンバーシップ、ファイルのサイズ (バイト単位)、ファイルの最大許容サイズ、および定義済みのファイル拡張サイズ (バイト単位) が表示されます。 この情報は、次のような場合に、データベース バックアップを復元する前にそのバックアップ内のファイルの名前を調べる際に役立ちます。  
  
-   データベースの 1 つ以上のファイルが格納されているディスク ドライブに障害が発生した場合。  
  
     データベース バックアップ内のファイルを一覧表示して、影響を受けたファイルを調べ、そのファイルはデータベース全体の復元時に別のドライブに復元することができます。影響を受けたファイルだけを復元して、データベースのバックアップ後に作成されたすべてのトランザクション ログのバックアップを適用することもできます。  
  
-   ディレクトリ構造やネットワーク ドライブが割り当てられていない別のサーバーにデータベースを復元する場合。  
  
     バックアップ内のファイルを一覧表示すると、影響を受けるファイルを調べることができます。 たとえば、ドライブ E に復元する必要があるファイルがバックアップに含まれているのに、復元先サーバーにドライブ E が存在しない場合があります。この場合、ファイルの復元時に、ドライブ Z など、別の場所にファイルを配置し直す必要があります。  
  
##  <a name="MediaHeader"></a> メディア ヘッダー情報  
 メディア ヘッダーを表示すると、メディア上のバックアップではなくメディアそのものに関する情報が表示されます。 メディア ヘッダー情報として、メディア名、説明、メディア ヘッダーを作成したソフトウェアの名前、およびメディア ヘッダーが書き込まれた日付が表示されます。  
  
> [!NOTE]  
>  メディア ヘッダーの表示にはごくわずかな時間しかかかりません。  
  
 詳細については、このトピックの後の方の「 [メディア ヘッダーとバックアップ ヘッダーの情報の比較](#CompareMediaHeaderBackupHeader)」を参照してください。  
  
##  <a name="BackupHeader"></a> バックアップ ヘッダー情報  
 バックアップ ヘッダーを表示すると、メディア上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ セットおよび[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のバックアップ セットに関する情報が表示されます。 表示される情報には、使用しているバックアップ デバイスの種類、バックアップの種類 (データベース、トランザクション、ファイル、差分データベースなど)、およびバックアップの開始と終了の日時が含まれています。 この情報は、テープ上のどのバックアップ セットを復元するかを判断したり、メディアに書き込まれているバックアップを調べる場合に役立ちます。  
  
> [!NOTE]  
>  メディア上の各バックアップに関する情報を表示するにはメディア全体をスキャンする必要があるため、大容量のテープの場合はバックアップ ヘッダー情報を表示するのに時間がかかることがあります。  
  
 詳細については、このトピックの後の方の「 [メディア ヘッダーとバックアップ ヘッダーの情報の比較](#CompareMediaHeaderBackupHeader)」を参照してください。  
  
### <a name="which-backup-set-to-restore"></a>復元するバックアップ セットの特定  
 バックアップ ヘッダーの情報を使用して、復元するバックアップ セットを識別できます。 バックアップ メディアの各バックアップ セットには、データベース エンジンによって番号が付けられます。 この番号を使用すると、復元するバックアップ セットをメディア内での位置によって識別できます。 たとえば、次のメディアには 3 つのバックアップ セットが含まれています。  
  
 ![SQL Server バックアップ セットを含むバックアップ メディア](../../database-engine/media/bnr-media-backup-sets.gif "SQL Server バックアップ セットを含むバックアップ メディア")  
  
 特定のバックアップ セットを復元するには、復元対象のバックアップ セットの位置番号を指定します。 たとえば、2 番目のバックアップ セットを復元するには、復元するバックアップ セットとして「2」を指定します。  
  
##  <a name="CompareMediaHeaderBackupHeader"></a> メディア ヘッダーとバックアップ ヘッダーの情報の比較  
 次の図で、バックアップ ヘッダー情報とメディア ヘッダー情報の表示の違いを例示します。 メディア ヘッダーを取得するには、テープの先頭にある情報のみを取得する必要があります。 バックアップ ヘッダーを取得するには、テープ全体をスキャンして各バックアップ セットのヘッダーを確認する必要があります。  
  
 ![3 つの SQL Server バックアップ セットを含むメディア セット](../../database-engine/media/bnr-media-label.gif "3 つの SQL Server バックアップ セットを含むメディア セット")  
  
> [!NOTE]  
>  複数のメディア ファミリを持ったメディア セットを使用すると、メディア ヘッダーおよびバックアップ セットがすべてのメディア ファミリに書き込まれます。 したがって、このような報告操作には、メディア ファミリを 1 つ提供するだけで十分です。  
  
 メディア ヘッダーの表示方法については、このトピックの「メディア ヘッダー情報の表示」を参照してください。  
  
 バックアップ デバイス上のすべてのバックアップ セットに関するバックアップ ヘッダー情報の表示方法については、このトピックの「バックアップ ヘッダー情報の表示」を参照してください。  
  
##  <a name="Verification"></a> バックアップの検証  
 必須ではありませんが、バックアップの確認は役に立つ作業です。 バックアップを確認することで、バックアップが物理的に損傷していないことが確認されます。これにより、バックアップのすべてのファイルの読み取りと復元が可能であること、必要なときにそのバックアップを復元できることが保証されます。 バックアップの確認では、バックアップのデータの構造は確認されないことに注意してください。 ただし、WITH CHECKSUMS を使用してバックアップが作成された場合、WITH CHECKSUMS を使用してバックアップを確認すると、バックアップのデータの信頼性がわかります。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **バックアップ履歴テーブルと復元履歴テーブルから古い行を削除するには**  
  
-   [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)  
  
 **バックアップ履歴テーブルと復元履歴テーブルから特定のデータベースのすべての行を削除するには**  
  
-   [sp_delete_database_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql)  
  
 **バックアップ セットに含まれているデータ ファイルおよびログ ファイルを表示するには**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A> (SMO)  
  
 **メディア ヘッダー情報を表示するには**  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadMediaHeader%2A> (SMO)  
  
 **バックアップ ヘッダー情報を表示するには**  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadBackupHeader%2A> (SMO)  
  
 **バックアップ履歴テーブルと復元履歴テーブルから古い行を削除するには**  
  
-   [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)  
  
 **バックアップ履歴テーブルと復元履歴テーブルから特定のデータベースのすべての行を削除するには**  
  
-   [sp_delete_database_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql)  
  
 **メディア ヘッダー情報を表示するには**  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadMediaHeader%2A> (SMO)  
  
 **バックアップ ヘッダー情報を表示するには**  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadBackupHeader%2A> (SMO)  
  
 **バックアップ セットに含まれているファイルを表示するには**  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
 **バックアップを検証するには**  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlVerify%2A> (SMO)  
  
## <a name="see-also"></a>関連項目  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [ミラー化バックアップ メディア セット &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)   
 [バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)  
  
  
