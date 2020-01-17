---
title: バックアップの有効期限の設定 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], expiration dates
- expiration [SQL Server]
- database backups [SQL Server], expiration dates
ms.assetid: 76e814df-6487-4893-9f09-7759f1863a5c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 91cc33a4f9cec62dd88f153bd02339d561918130
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041435"
---
# <a name="set-the-expiration-date-on-a-backup-sql-server"></a>バックアップの有効期限の設定 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、バックアップの有効期限を設定する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **バックアップの有効期限を設定する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>バックアップの有効期限を設定するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
4.  **[全般]** ページの **[バックアップ セットの有効期限]** で、バックアップ セットを別のバックアップで上書きできる期日を示す有効期限を指定します。  
  
    -   バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** (既定のオプション) をクリックし、セットを作成してからセットが期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ( **[データベースの設定]** ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックします。次に、 **[データベースの設定]** ページをクリックします。  
  
    -   バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>バックアップの有効期限を設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  [BACKUP](../../t-sql/statements/backup-transact-sql.md) ステートメントで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] がいつバックアップを上書きできるようになるかを決定する EXPIREDATE または RETAINDAYS オプションを指定します。 どちらのオプションも指定しない場合、失効日は [media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) (メディア保持期間) のサーバー設定によって決まります。 この例では、 `EXPIREDATE` オプションを使用して、2015 年 6 月 30 日 (`6/30/2015`) の有効期限を指定します。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH EXPIREDATE = '6/30/2015' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
  
