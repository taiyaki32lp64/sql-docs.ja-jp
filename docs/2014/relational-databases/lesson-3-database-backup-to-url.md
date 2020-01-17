---
title: レッスン 4:Azure Storage | でデータベースを作成します。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee331966984a12d309e71a7040edac6343e296c6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175630"
---
# <a name="lesson-4-create-a-database-in-azure-storage"></a>レッスン 4:Azure Storage でのデータベースの作成
  このレッスンでは、Azure 機能の SQL Server データファイルを使用してデータベースを作成する方法について説明します。 このレッスンの前に、レッスン 1、2、および 3 を完了する必要があることに注意してください。 レッスン3は非常に重要な手順です。レッスン4の前に、Azure ストレージコンテナーとそれに関連付けられているポリシー名と SAS キーに関する情報を SQL Server 資格情報ストアに格納する必要があるためです。  
  
 データ ファイルまたはログ ファイルによって使用されるストレージ コンテナーごとに、名前がコンテナーのパスに一致する SQL Server 資格情報を作成する必要があります。 次に、で新しいデータベースを作成でき Azure Storage  
  
 このレッスンでは、次の手順を既に完了していることを前提としています。  
  
-   Azure Storage アカウントを持っています。  
  
-   Azure Storage アカウントでコンテナーを作成しました。  
  
-   読み取り、書き込み、一覧表示の権限のあるコンテナーに対するポリシーを作成しました。 SAS キーも生成しました。  
  
-   ソース コンピューターで SQL Server 資格情報を作成しました。  
  
 Azure Storage 機能の SQL Server データファイルを使用して Azure にデータベースを作成するには、次の手順に従います。  
  
1.  SQL Server Management Studio に接続します。  
  
2.  オブジェクト エクスプローラーで、インストールしたデータベース エンジンのインスタンスに接続します。  
  
3.  標準ツールバーで、[新しいクエリ] をクリックします。  
  
4.  次の例をコピーしてクエリ ウィンドウに貼り付け、必要に応じて変更します。 FILENAME フィールドがストレージ コンテナーにあるデータベース ファイルの URI パスを指し、先頭は https にする必要があることに注意してください。  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     データベースにデータを追加します。  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  内部設置型 SQL Server の新しい TestDB1 を表示するには、オブジェクト エクスプローラーでデータベースの表示を更新します。  
  
6.  同様に、ストレージ アカウントに新しく作成したデータベースを表示するには、SQL Server Management Studio (SSMS) 経由でストレージ アカウントに接続します。 SQL Server Management Studio を使用して Azure storage に接続する方法については、次の手順に従います。  
  
    1.  まず、ストレージ アカウント情報を取得します。 管理ポータルにログインします。 次に、 **[ストレージ]** をクリックし、ストレージアカウントを選択します。 ストレージアカウントを選択したら、ページの下部にある **[アクセスキーの管理]** をクリックします。 次のようなダイアログ ウィンドウが開きます。  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  **ストレージアカウント名**と**プライマリアクセスキー**の値を、SSMS の **[Azure Storage への接続]** ダイアログウィンドウにコピーします。 次に、 **[接続]** をクリックします。 これで、次のスクリーン ショットに示すように、ストレージ アカウント コンテナーについての情報が SSMS に表示されます。  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 次のスクリーンショットは、オンプレミス環境と Azure Storage 環境の両方で作成された新しいデータベースを示しています。  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **注:** コンテナー内のデータファイルに対するアクティブな参照が存在する場合、関連付けられている SQL Server 資格情報を削除しようとすると失敗します。 同様に、既に BLOB の特定のデータベース ファイルにリースが設定されていて、そのデータベースを削除する場合、まず、BLOB のリースを解除する必要があります。 リースを中断するには、[リース Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx)を使用します。  
  
 この新しい機能を使用して、CREATE DATABASE ステートメントの既定値がクラウド対応データベースになるように、SQL Server を構成できます。 つまり、データベースを作成するたびに、すべてのデータベースファイル (.mdf、.ldf) が Azure Storage のページ blob として作成されるように、SQL Server Management Studio サーバーインスタンスのプロパティで既定のデータとログの場所を設定できます。  
  
 SQL Server Management Studio ユーザーインターフェイスを使用して Azure Storage でデータベースを作成するには、次の手順を実行します。  
  
1.  オブジェクト エクスプローラーで、SQL Server データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。  
  
2.  [データベース] を右クリックし、[新しいデータベース] をクリックします。  
  
3.  [新しいデータベース] ダイアログ ウィンドウで、データベース名を入力します。  
  
4.  プライマリ データ ファイルとトランザクション ログ ファイルの既定値を変更します。[データベース ファイル] グリッドで該当するセルをクリックして、新しい値を入力します。 また、ファイルの場所のパスも指定します。 パスとしては、ストレージ コンテナーの URL パスを入力します (たとえば、`https://teststorageaccnt.blob.core.windows.net/testcontainer/`)。 ファイル名としては、データベース ファイル (.mdf、.ldf) の物理ファイル名を入力します。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     詳細については、「 [データベースに対するデータ ファイルまたはログ ファイルの追加](databases/add-data-or-log-files-to-a-database.md)」をご覧ください。  
  
5.  その他の値は既定値のままにします。  
  
6.  [OK] をクリックします。  
  
 内部設置型 SQL Server の新しい TestDB1 を表示するには、オブジェクト エクスプローラーでデータベースの表示を更新します。 同様に、ストレージ アカウントに新しく作成したデータベースを表示するには、このレッスンの前の方で説明したように、SQL Server Management Studio (SSMS) 経由でストレージ アカウントに接続します。  
  
 **次のレッスン:**  
  
 [レッスン 5.&#40;オプション&#41; tde を使用してデータベースを暗号化する](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
