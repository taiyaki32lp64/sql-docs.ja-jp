---
title: コピーのみのバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96267b98d7e17b920e0a7cee70b69e4c964584e4
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798009"
---
# <a name="copy-only-backups-sql-server"></a>コピーのみのバックアップ (SQL Server)
  *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 通常、バックアップを行うとデータベースが変更され、その後のバックアップの復元方法に影響します。 ただし、データベース全体のバックアップや復元の手順に影響を与えない、特殊な目的にバックアップを行うと役に立つ場合があります。 このため、コピーのみのバックアップが導入されました。  
  
 コピーのみのバックアップには、次の種類があります。  
  
-   コピーのみの完全バックアップ (すべての復旧モデル)  
  
     コピーのみのバックアップは、差分ベースまたは差分バックアップとして使用できません。また、差分ベースに影響しません。  
  
     コピーのみの完全バックアップも、他の完全バックアップと同じ方法で復元できます。  
  
-   コピーのみのログ バックアップ (完全復旧モデルおよび一括ログ復旧モデルのみ)  
  
     コピーのみのログ バックアップは、既存のログ アーカイブ ポイントを保持するため、定期的なログ バックアップの一連の作業に影響を与えません。 通常、コピーのみのログ バックアップは不要です。 新しい定期的なログ バックアップを (WITH NORECOVERY を使用して) 作成してから、そのバックアップを、復元シーケンスに必要なすべての以前のログ バックアップと共に使用できます。 ただし、コピーのみのログ バックアップは、オンライン復元を実行する際に役立つ場合があります。 この例については、「[例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)」を参照してください。  
  
     コピーのみのバックアップの後、トランザクション ログは切り捨てられません。  
  
 コピーのみのバックアップは、 **backupset** テーブルの [is_copy_only](/sql/relational-databases/system-tables/backupset-transact-sql) 列に記録されます。  
  
## <a name="to-create-a-copy-only-backup"></a>コピーのみのバックアップを作成するには  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)]、または PowerShell を使用してコピーのみのバックアップを作成できます。  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
1.  **[データベースのバックアップ]** ダイアログ ボックスの **[全般]** ページで、 **[バックアップのみコピーする]** オプションを選択します。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 必須の [!INCLUDE[tsql](../../../includes/tsql-md.md)] 構文は次のとおりです。  
  
-   コピーのみの完全バックアップの場合:  
  
     データベース*database_name*を \<backup_device *>* にバックアップしています...COPY_ONLY...  
  
    > [!NOTE]  
    >  COPY_ONLY は、DIFFERENTIAL オプションと共に指定した場合には機能しません。  
  
-   コピーのみのログ バックアップの場合:  
  
     BACKUP LOG *database_name* *\<* backup_device *>* ...COPY_ONLY...  
  
###  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
`Backup-SqlDatabase` パラメーターを指定して `-CopyOnly` コマンドレットを使用します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  

### <a name="to-create-a-full-or-log-backup"></a>完全バックアップまたはログ バックアップを作成するには
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
### <a name="to-view-copy-only-backups"></a>コピーのみのバックアップを表示するには
  
-   [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
### <a name="to-set-up-and-use-the-sql-server-powershell-provider"></a>SQL Server PowerShell プロバイダーを設定して使用するには
  
-   [SQL Server PowerShell プロバイダー](../../powershell/sql-server-powershell-provider.md)  

## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
