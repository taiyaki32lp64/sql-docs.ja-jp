---
title: ログ末尾のバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6da8f9de22f1b3191d6fba1918e8c05a64d062f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920677"
---
# <a name="tail-log-backups-sql-server"></a>ログ末尾のバックアップ (SQL Server)
  このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのバックアップと復元のみに関連しています。  
  
 *ログ末尾のバックアップ* は、まだバックアップされていないすべてのログ レコード ( *ログの末尾*) をキャプチャし、作業内容の消失を防いで、ログ チェーンの完全性を維持します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをその最新の時点まで復元するには、トランザクション ログの末尾をあらかじめバックアップしておく必要があります。 ログ末尾のバックアップは、データベースの復旧プランの対象になる最後のバックアップとなります。  
  
> [!NOTE]  
>  ログ末尾のバックアップは、すべての復元シナリオで必要となるわけではありません。 復旧ポイントが、それより前のログ バックアップに含まれているのであれば、ログ末尾のバックアップは不要です。 また、データベースを移動するか置き換えて (上書きして) いる場合、ログ末尾のバックアップは不要であり、最新のバックアップ以降の特定の時点に復元する必要もありません。  
  
 
  
##  <a name="TailLogScenarios"></a> ログ末尾のバックアップが必要となるシナリオ  
 以下に示すシナリオでは、ログ末尾のバックアップをお勧めします。  
  
-   データベースがオンライン状態であり、データベースに対して復元操作を実行する予定がある場合に、ログ末尾のバックアップを最初に行う。 オンライン データベースのエラーを防ぐには、WITH NORECOVERY オプション、[バックアップ](/sql/t-sql/statements/backup-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。  
  
-   データベースがオフラインで起動できず、データベースを復元する必要がある場合に、まずログの末尾をバックアップする。 このとき、トランザクションは発生しないので、WITH NORECOVERY の指定は省略できます。  
  
-   データベースが破損したとき、BACKUP ステートメントの WITH CONTINUE_AFTER_ERROR オプションを使用してログ末尾のバックアップを試す。  
  
     破損しているデータベースでログ末尾のバックアップが成功するのは、ログ ファイルが破損しておらず、データベースがログ末尾のバックアップをサポートしている状態であり、一括ログ記録された変更がデータベースに含まれていない場合に限られます。 ログ末尾のバックアップを作成できない場合、最新のログ バックアップの後にコミットされたトランザクションはすべて失われます。  
  
 次の表は、BACKUP NORECOVERY と CONTINUE_AFTER_ERROR オプションをまとめたものです。  
  
|BACKUP LOG オプション|コメント|  
|-----------------------|--------------|  
|NORECOVERY|データベースの復元操作を続行する場合は、必ず NORECOVERY を使用します。 NORECOVERY を指定すると、データベースは復元中の状態になります。 これにより、ログ末尾のバックアップの後にデータベースが変化しないことが保障されます。  ログには、NO_TRUNCATE オプションまたは COPY_ONLY オプションが指定されてもいない場合は切り捨てられます。<br /><br /> **\*\* 重要な\* \*** データベースが破損している場合を除き、NO_TRUNCATE を使用しないことをお勧めします。|  
|CONTINUE_AFTER_ERROR|破損したデータベースの末尾をバックアップする場合に限り、CONTINUE_AFTER_ERROR を使用します。<br /><br /> 注:破損したデータベースにログ末尾のバックアップを適用する場合、通常であればログ バックアップにキャプチャされるメタデータの一部を使用できない場合があります。 詳細については、後の「[不完全なバックアップ メタデータが含まれたログ末尾のバックアップ](#IncompleteMetadata)」を参照してください。|  
  
##  <a name="IncompleteMetadata"></a> 不完全なバックアップ メタデータが含まれたログ末尾のバックアップ  
 データベースがオフラインである場合、データベースが破損している場合、またはデータ ファイルが欠落している場合でも、ログ末尾のバックアップではログの末尾がキャプチャされます。 これが原因で、復元情報コマンドや **msdb**のメタデータが不完全になる場合があります。 ただし、メタデータが不完全なだけで、キャプチャされたログは完全であり、使用できます。  
  
 ログ末尾のバックアップに不完全なメタデータが含まれている場合は、 [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) テーブルの **has_incomplete_metadata** が **1**に設定されます。 また、 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)の出力で **HasIncompleteMetadata** が **1**に設定されます。  
  
 ログ末尾のバックアップのメタデータが不完全な場合、ログ末尾のバックアップ時に、ファイル グループに関する情報の大部分が [backupfilegroup](/sql/relational-databases/system-tables/backupfilegroup-transact-sql) テーブルから欠落します。 **backupfilegroup** テーブルのほとんどの列は NULL になり、意味を持つ列は次の列のみです。  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **型**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 ログ末尾のバックアップを作成するには、「[データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)」をご覧ください。  
  
 トランザクション ログ バックアップを復元するには、「[トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)   
 [コピーのみのバックアップ &#40;SQL Server&#41;](copy-only-backups-sql-server.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
