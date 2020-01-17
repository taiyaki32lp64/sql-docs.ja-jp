---
title: 'レッスン 6: オンプレミスのソースマシンから Azure のターゲットコンピューターにデータベースを移行する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 689c3a734a5b4eb424511da52032dc348b5757ea
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75231804"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-azure"></a>レッスン 6: オンプレミスのソースマシンから Azure のターゲットコンピューターにデータベースを移行する
  このレッスンでは、別のオンプレミスコンピューターまたは Azure の仮想マシンに存在する可能性がある別の SQL Server が既にあることを前提としています。 Azure で SQL Server 仮想マシンを作成する方法の詳細については、「 [azure での SQL Server 仮想マシンのプロビジョニング](https://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/)」を参照してください。 Azure に SQL Server 仮想マシンをプロビジョニングした後、別のコンピューターの SQL Server Management Studio を使用して、この仮想マシンの SQL Server のインスタンスに接続できることを確認してください。  
  
 このレッスンは、次の手順を完了済みであることも前提としています。  
  
-   Azure Storage アカウントを持っています。  
  
-   Azure Storage アカウントでコンテナーを作成しました。  
  
-   読み取り、書き込み、一覧表示の権限のあるコンテナーに対するポリシーを作成しました。 SAS キーも生成しました。  
  
-   ソース コンピューターで SQL Server 資格情報を作成しました。  
  
-   Azure に仮想マシン SQL Server 仮想マシンが既に作成されています。 仮想マシンは、SQL Server 2014 を含んでいるプラットフォーム イメージを選択して作成することをお勧めします。  
  
 オンプレミスの SQL Server から Azure の別の仮想マシンにデータベースを移行するには、次の手順を実行します。  
  
1.  ソース コンピューター (このチュートリアルでは内部設置型コンピューター) で、SQL Server Management Studio のクエリ ウィンドウを開きます。 次のステートメントを実行して、データベースをデタッチし、別のコンピューターに移動します。  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  ターゲット コンピューターにデータベースを転送する必要がある場合は、まずデータベースを準備しておく必要があります。 ターゲット コンピューターを準備するには、まずターゲット コンピューターで SQL Server 資格情報を作成する必要があります。 暗号化されたデータベースの場合は、証明書もソース コンピューターからターゲット コンピューターにインポートする必要があります。  
  
    1.  ターゲット コンピューターで SQL Server 資格情報を作成するには、次の手順を実行します。  
  
        1.  ソース コンピューターの SQL Server Management Studio 経由でターゲット コンピューターに接続します。  または、ターゲット コンピューターで SQL Server Management Studio を直接起動します。  
  
        2.  
  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
        3.  次の例をコピーしてクエリ ウィンドウに貼り付け、必要に応じて変更します。 次のステートメントは、ストレージコンテナーの共有アクセス証明書を格納するための SQL Server 資格情報を作成します。  
  
            ```sql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  使用可能なすべての資格情報を表示するには、クエリ ウィンドウで次のステートメントを実行します。  
  
            ```sql  
            SELECT * from sys.credentials   
            ```  
  
        5.  ターゲット サーバーに接続して、クエリ ウィンドウを開き、次のステートメントを実行します。  
  
            ```sql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             この手順が終了すると、ソース コンピューターからバックアップされた暗号化証明書がターゲット コンピューターにインポートされます。 次に、ターゲット コンピューターでデータ ファイルをアタッチできます。  
  
    2.  次に、FOR ATTACH オプションを使用して Azure Storage 内の既存のファイルを指すデータファイルとログファイルを含むデータベースを作成します。 クエリ ウィンドウで、次のステートメントを実行します。  
  
        ```sql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  オブジェクト エクスプローラーで、[データベース] を右クリックし、[更新] をクリックします。 新しく作成したデータベース TestDB1onDest が一覧に表示されることを確認します。  
  
    4.  次に、クエリ ウィンドウで次のステートメントを実行します。  
  
        ```sql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         これでレッスン 4 で入力したデータがすべて表示されます。  
  
 暗号化されたデータベースがデータ移動なしで別のコンピューター インスタンスに転送されたことに注意してください。  
  
 SQL Server Management Studio ユーザーインターフェイスを使用して Azure Storage 内の既存のファイルを指すデータファイルとログファイルを含むデータベースを作成するには、次の手順を実行します。  
  
1.  **オブジェクトエクスプローラー**で、SQL Server データベースエンジンのインスタンスに接続し、そのインスタンスを展開します。  
  
2.  [**データベース**] を右クリックし、[**新しいデータベース**] をクリックします。 次に [TestDB1] を右クリックします。 [タスク] をクリックし、[デタッチ] をクリックします。 [デタッチ] ダイアログ ウィンドウで、[接続の削除] チェック ボックスをオンにします。 [**OK**] をクリックすると、  
  
3.  SQL Server 2014 CTP2 以降がインストールされたターゲット コンピューターに接続します。 ターゲット コンピューターを準備するには、ターゲット コンピューターで、TestDB1 を格納した同じコンテナーを指す SQL Server 資格情報を作成する必要があります。 同じコンピューターで再アタッチする場合、別の資格情報を作成する必要はありません。  
  
4.  **オブジェクトエクスプローラー**で、[**データベース**] を右クリックし、[**アタッチ**] をクリックします。  
  
5.  [**データベースのアタッチ**] ダイアログボックスで、アタッチするデータベースを指定するために、[**追加**] をクリックします。 [**データベースファイルの検索**] ダイアログウィンドウで次のようにします。  
  
     [データベースデータファイルの場所] に`https://teststorageaccnt.blob.core.windows.net/testcontainer/`、「」と入力します。  
  
     [ファイル名] に「 `TestDB1Data.mdf`」と入力します。  
  
6.  [**OK**] をクリックすると、  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **次のレッスン:**  
  
 [レッスン 7: Azure Storage にデータファイルを移動する](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
