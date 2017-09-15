---
title: "コピーのみのバックアップ (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
caps.latest.revision: 48
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a63e882e79ec725cca126e80369a70bbc4bc774
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="copy-only-backups-sql-server"></a>コピーのみのバックアップ (SQL Server)
  *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 通常、バックアップを行うとデータベースが変更され、その後のバックアップの復元方法に影響します。 ただし、データベース全体のバックアップや復元の手順に影響を与えない、特殊な目的にバックアップを行うと役に立つ場合があります。 このため、コピーのみのバックアップが導入されました。  
  
 コピーのみのバックアップには、次の種類があります。  
  
-   コピーのみの完全バックアップ (すべての復旧モデル)  
  
     コピーのみのバックアップは、差分ベースまたは差分バックアップとして使用できません。また、差分ベースに影響しません。  
  
     コピーのみの完全バックアップも、他の完全バックアップと同じ方法で復元できます。  
  
-   コピーのみのログ バックアップ (完全復旧モデルおよび一括ログ復旧モデルのみ)  
  
     コピーのみのログ バックアップは、既存のログ アーカイブ ポイントを保持するため、定期的なログ バックアップの一連の作業に影響を与えません。 通常、コピーのみのログ バックアップは不要です。 新しい定期的なログ バックアップを (WITH NORECOVERY を使用して) 作成してから、そのバックアップを、復元シーケンスに必要なすべての以前のログ バックアップと共に使用できます。 ただし、コピーのみのログ バックアップは、オンライン復元を実行する際に役立つ場合があります。 この例については、「[例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)」を参照してください。  
  
     コピーのみのバックアップの後、トランザクション ログは切り捨てられません。  
  
 コピーのみのバックアップは、 **backupset** テーブルの [is_copy_only](../../relational-databases/system-tables/backupset-transact-sql.md) 列に記録されます。  
  
## <a name="to-create-a-copy-only-backup"></a>コピーのみのバックアップを作成するには  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または PowerShell を使用してコピーのみのバックアップを作成できます。  

### <a name="examples"></a>使用例  
###  <a name="SSMSProcedure"></a> A.  SQL Server Management Studio の使用  
次の例では、 `Sales` データベースのコピーのみのバックアップを既定のバックアップ場所にあるディスクにバックアップします。

1.  **オブジェクト エクスプローラー**で、SQL Server データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。

2.  **[データベース]**を展開して `Sales`を右クリックし、 **[タスク]**をポイントしてから **[バックアップ]**をクリックします。

3.  **[全般]** ページの **[ソース]** セクションにある **[コピーのみのバックアップ]** チェック ボックスをオンします。

4.  **[OK]**をクリックします。

  
###  <a name="TsqlProcedure"></a>B.  Transact-SQL の使用  
次の例では、COPY_ONLY parameter パラメーターを使用して `Sales` データベースに対するコピーのみのバックアップが作成されます。  トランザクション ログのコピーのみのバックアップも同様に取得されます。

```tsql
BACKUP DATABASE Sales
TO DISK = 'E:\BAK\Sales_Copy.bak'
WITH COPY_ONLY;

BACKUP LOG Sales
TO DISK = 'E:\BAK\Sales_LogCopy.trn'
WITH COPY_ONLY;
```
  
> [!NOTE]  
> COPY_ONLY は、DIFFERENTIAL オプションと共に指定した場合には機能しません。  

  
###  <a name="PowerShellProcedure"></a>C.  PowerShell の使用  
次の例では、-CopyOnly パラメーターを使用して `Sales` データベースに対するコピーのみのバックアップが作成されます。  
```powershell
Backup-SqlDatabase -ServerInstance 'SalesServer' -Database 'Sales' -BackupFile 'E:\BAK\Sales_Copy.bak' -CopyOnly
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **完全バックアップまたはログ バックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **コピーのみのバックアップを表示するには**  
  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[Backup-SqlDatabase](https://technet.microsoft.com/library/mt683378.aspx)

  
