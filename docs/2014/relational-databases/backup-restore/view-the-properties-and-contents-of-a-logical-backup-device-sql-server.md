---
title: 論理バックアップ デバイスのプロパティと内容の表示 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e593a5d64b6a1b009a68c434fe9ce1a32cb2de20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921070"
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>論理バックアップ デバイスのプロパティと内容の表示 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]の論理バックアップ デバイスのプロパティと内容を表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **論理バックアップ デバイスのプロパティと内容を表示する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティについては、「[RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)」を参照してください。  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、バックアップ セットやバックアップ デバイスに関する情報の取得には CREATE DATABASE 権限が必要になります。 詳細については、「[GRANT (データベースの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>論理バックアップ デバイスのプロパティと内容を表示するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[サーバー オブジェクト]** を展開し、 **[バックアップ デバイス]** を展開します。  
  
3.  デバイスをクリックし、 **[プロパティ]** を右クリックして **[バックアップ デバイス]** ダイアログ ボックスを開きます。  
  
4.  **[全般]** ページにデバイス名とバックアップ先が表示されます。これはテープ ドライブまたはファイル パスです。  
  
5.  **[ページの選択]** ペインで **[メディアの内容]** をクリックします。  
  
6.  右側のペインに次のプロパティ パネルが表示されます。  
  
    -   **[メディア]**  
  
         メディアのシーケンス情報 (メディア シーケンス番号、ファミリ シーケンス番号、ミラー識別子など) とメディアの作成日時。  
  
    -   **[メディア セット]**  
  
         メディア セットの情報 (メディア セットの名前および説明) とメディア セット内のファミリ数。  
  
7.  **[バックアップ セット]** グリッドには、メディア セットの内容に関する情報が表示されます。  
  
> [!NOTE]  
>  詳細については、「 [[バックアップ デバイス] ([メディアの内容] ページ)](backup-device-media-contents-page.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>論理バックアップ デバイスのプロパティと内容を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  [RESTORE LABELONLY](/sql/t-sql/statements/restore-statements-labelonly-transact-sql) ステートメントを使用します。 この例は、 `AdvWrks2008R2Backup` 論理バックアップ デバイスに関する情報を返します。  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>関連項目  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
