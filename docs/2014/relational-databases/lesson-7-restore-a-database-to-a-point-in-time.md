---
title: 'レッスン 8: データベースを Azure Storage に復元する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b30a9f60f52b8b19875f5fb3c15242ce2c632fd
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175430"
---
# <a name="lesson-8-restore-a-database-to-azure-storage"></a>レッスン 8: Azure Storage にデータベースを復元する
  このレッスンでは、バックアップファイルをローカルに作成し、Azure Storage に復元する方法について説明します。 データベースは、オンプレミスまたは Azure の仮想マシンのいずれかにあることに注意してください。 このレッスンを続行するには、レッスン 4、5、6 および 7 を実行する必要はありません。  
  
 このレッスンでは、次の手順を既に完了していることを前提としています。  
  
-   Azure Storage アカウントを持っています。  
  
-   Azure Storage アカウントでコンテナーを作成しました。  
  
-   読み取り、書き込み、一覧表示の権限のあるコンテナーに対するポリシーを作成しました。 SAS キーも生成しました。  
  
-   Shared Access Signature に基づいてソース コンピューターで SQL Server 資格情報を作成しました。  
  
-   ソース コンピューターにデータベースを作成しました。  
  
 データベースを Azure Storage に復元するには、次の手順を実行します。  
  
1.  ソース コンピューターで、SQL Server Management Studio を起動します。  
  
2.  新しく作成したデータベースに接続すると、クエリ ウィンドウが開きます。 次のステートメントを実行します。  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  次に、クエリ ウィンドウに次のステートメントをコピーして実行します。  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     この手順が終了すると、管理ポータルにコンテナーのデータ ファイル (.mdf) とログ ファイル (.ldf) が表示されます。  
  
 SQL Server Management Studio ユーザーインターフェイスを使用して Azure Storage を指すデータファイルとログファイルを含むデータベースを復元するには、次の手順を実行します。  
  
1.  **オブジェクトエクスプローラー**で、サーバー名をクリックしてサーバーツリーを展開します。  
  
2.  **[データベース]** を展開し、データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をクリックします。  
  
4.  **[全般]** ページの **[復元]** 元 セクションで、 **[ソース]** デバイス をクリックします。  
  
5.  **[ソース]** デバイス ボックスの参照ボタンをクリックして、 **[バックアップデバイスの選択]** ダイアログボックスを開きます。  
  
6.  バックアップメディア ボックスで、**ファイル** を選択し、**追加** ボタンをクリックしてバックアップ (.bak) ファイルを指定します。 **[OK]** をクリックします。  
  
7.  最初のページの **[ファイル]** をクリックします。  
  
8.  **[データベースファイルの復元]** セクションの **[復元元]** フィールドに、次のように入力します。  
  
     データファイルの場合は、 `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`「」と入力します。 ログファイルの場合は、 `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`「」と入力します。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. **[OK]** をクリックします。  
  
 復元を実行したら、管理ポータルにログインします。 コンテナーの .mdf ファイルおよび .ldf ファイルを次のように確認できる必要があります。  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **次のレッスン:**  
  
 [レッスン 9:Azure Storage からデータベースを復元する](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
