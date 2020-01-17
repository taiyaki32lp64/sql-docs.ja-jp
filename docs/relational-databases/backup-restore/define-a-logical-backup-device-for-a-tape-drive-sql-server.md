---
title: テープ ドライブの論理バックアップ デバイスの定義 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f260ee4737f1d493986e5cfa8e308d8882328140
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908955"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>テープ ドライブの論理バックアップ デバイスの定義 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でテープ ドライブの論理バックアップ デバイスを定義する方法について説明します。 論理バックアップ デバイスとは、特定の物理バックアップ デバイス (ディスク ファイルまたはテープ ドライブ) を示すユーザー定義名です。  物理デバイスは、後で、つまりバックアップがバックアップ デバイスに書き込まれたときに初期化されます。  
  
> [!NOTE]  
>  テープ バックアップ デバイスは、将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされなくなる予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **テープ ドライブの論理バックアップ デバイスを定義する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   テープ ドライブまたはドライブは、Microsoft Windows オペレーティング システムによってサポートされている必要があります。  
  
-   テープ デバイスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスが動作しているコンピューターに物理的に接続する必要があります。 リモートのテープ デバイスへのバックアップはサポートされません。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **diskadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
 ディスクに対する書き込み権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>テープ ドライブの論理バックアップ デバイスを定義するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[サーバー オブジェクト]** を展開し、 **[バックアップ デバイス]** を右クリックします。  
  
3.  **[新しいバックアップ デバイス]** をクリックし、 **[バックアップ デバイス]** ダイアログ ボックスを開きます。  
  
4.  デバイス名を入力します。  
  
5.  バックアップ先として **[テープ]** をクリックし、まだ別のバックアップ デバイスに関連付けられていないテープ ドライブを選択します。 使用できるテープ ドライブがない場合、 **[テープ]** オプションはアクティブになりません。  
  
6.  新しいデバイスを定義するには、 **[OK]** をクリックします。  

 この新しいデバイスをバックアップするには、このデバイスを **[データベースのバックアップ]** ダイアログ ボックス ( **[全般]** ページ) の **[バックアップ先]** フィールドに追加します。 詳細については、データベースの完全バックアップの作成 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)を使用してデータベースの差分バックアップを作成します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>テープ ドライブの論理バックアップ デバイスを定義するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) を使用して、テープの論理バックアップ デバイスを定義します。 この例では、 `tapedump1`というテープ バックアップ デバイスを物理名 `\\.\tape0`で追加します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
