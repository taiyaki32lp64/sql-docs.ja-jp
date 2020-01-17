---
title: 'レッスン 9: Azure Storage からのデータベースの復元 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 464961600f69f14a2b66515a75906c0fd4af3f82
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175355"
---
# <a name="lesson-9-restore-a-database-from-azure-storage"></a>レッスン 9: Azure Storage からデータベースを復元する
  このレッスンでは、データベースバックアップファイルを Azure Storage からデータベースに復元する方法について説明します。このデータベースは、オンプレミスまたは Azure の仮想マシンに存在します。 このレッスンを続行するには、レッスン 4、5、6、7 および 8 を実行する必要はありません。  
  
 このレッスンでは、次の手順を既に完了していることを前提としています。  
  
-   ソース コンピューターにデータベースを作成しました。  
  
-   「 [Azure Blob Storage サービスを使用したバックアップと復元](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」機能を使用して SQL Server、Azure Storage でデータベース (.bak) のバックアップを作成しました。 この手順では、SQL Server 資格情報をもう 1 つ作成する必要があることに注意してください。 この資格情報はストレージ アカウント キーを使用します。  
  
-   Azure Storage アカウントを持っています。  
  
-   Azure Storage アカウントでコンテナーを作成しました。  
  
-   読み取り、書き込み、一覧表示の権限のあるコンテナーに対するポリシーを作成しました。 SAS キーも生成しました。  
  
-   Azure Storage 統合機能用のコンピューターに SQL Server 資格情報を作成しました。 この資格情報には Shared Access Signature (SAS) キーが必要であることに注意してください。  
  
 Azure Storage からデータベースを復元するには、次の手順を実行します。  
  
1.  [SQL Server Management Studio] を起動します。 既定のインスタンスに接続します。  
  
2.  標準 ツールバーの **新しいクエリ** をクリックします。  
  
3.  次の完全なスクリプトをコピーして、クエリ ウィンドウに貼り付けます。 必要に応じて、スクリプトを変更します。  
  
     **注:** `RESTORE`ステートメントを実行して、Azure Storage 内のデータベースバックアップ (.bak) を別のコンピューターのデータベースインスタンスに復元します。  
  
    ```sql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **チュートリアルの終了:Azure Storage サービスのデータファイルの SQL Server**  
  
  
