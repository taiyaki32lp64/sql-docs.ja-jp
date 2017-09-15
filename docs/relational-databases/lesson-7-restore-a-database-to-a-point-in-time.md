---
title: "レッスン 7: 特定の時点にデータベースを復元する | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a25788a3b7eda518aeff01329eb5e207d9092bd6
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>レッスン 7: 特定の時点にデータベースを復元する
このレッスンでは、2 つのトランザクション ログ バックアップ間の特定のポイントに AdventureWorks2014 データベースを復元します。  
  
従来のバックアップの場合、ポイント イン タイム リストアを実行するには、復元する時点までの、およびその直後の完全なデータベース バックアップ (場合によっては差分バックアップ) とすべてのトランザクション ログ ファイルを使用する必要がありました。 ファイルスナップショット バックアップの場合、復元先の時点を枠内に入れたゴール ポストを設定する 2 つ隣接するログ バックアップ ファイルを必要とするだけです。 各ログ バックアップによって各データベース ファイルのファイル スナップショット (各データ ファイルとログ ファイル) が作成されるので、ログ ファイル スナップショット バックアップ セットが 2 つ必要なだけです。  
  
ファイル スナップショット バックアップ セットから、指定した時点にデータベースを復元するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。  
  
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。  
  
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けて実行します。 Production.Location テーブルの行数が 29,939 行であることを確認してから、手順 5 で示すこれより行数が少なかった特定の時点にこのテーブルを復元します。  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![29,939 の行カウントが表示されている状態](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "29,939 の行カウントが表示されている状態")  
  
4.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 2 つの隣接するログ バックアップ ファイルを選択し、そのファイル名を、次のスクリプトで必要となる日付と時刻に変換します。 レッスン 1 で指定したコンテナーとストレージ アカウント名に合わせて URL を適切に変更し、1 番目と 2 番目のバックアップ ファイルの名前を指定し、STOPAT 時間を "June 26, 2015 01:48 PM" の形式で指定し、次のスクリプトを実行します。 このスクリプトは完了するまで数分かかります  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  出力を確認します。 復元後、行数は 18,389 行になっています。この値は、ログ バックアップ 5 の行数 ～ ログ バックアップ 6 の行数の範囲内の値です (行数は変動します)。  
  
    ![ポイントインタイム リストア後の行数を示す結果ペイン](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "ポイントインタイム リストア後の行数を示す結果ペイン")  
  
**次のレッスン:**  
  
[レッスン 8:ログ バックアップから新しいデータベースとして復元する](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  
