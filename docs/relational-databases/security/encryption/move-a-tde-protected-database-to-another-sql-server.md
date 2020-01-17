---
title: 別の SQL Server への TDE で保護されたデータベースの移動 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
author: aliceku
ms.author: aliceku
ms.openlocfilehash: 991af6f353fb4862bd66426e7fdeed2664f3d101
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594313"
---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>別の SQL Server への TDE で保護されたデータベースの移動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用して、Transparent Data Encryption (TDE) によってデータベースを保護し、そのデータベースを別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに移動する方法について説明します。 TDE では、データとログ ファイルの暗号化および暗号化解除がリアルタイムの I/O で実行されます。 暗号化にはデータベース暗号化キー (DEK) が使用されます。これは、復旧時に使用できるようにデータベース ブート レコードに保存されます。 DEK は、サーバーの **master** データベースに保存されている証明書を使用して保護される対称キーか、EKM モジュールによって保護される非対称キーです。   
   
##  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   TDE で保護されたデータベースを移動するとき、DEK を開くために使用される証明書または非対称キーも移動する必要があります。 この証明書または非対称キーは、 **からデータベース ファイルにアクセスできるように、移動先サーバーの** master [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースにインストールする必要があります。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  
  
-   証明書を復旧するために、証明書ファイルと秘密キー ファイルの両方のコピーを保持する必要があります。 秘密キーのパスワードは、データベース マスター キーのパスワードと同じにする必要はありません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、既定で、ここで作成したファイルを **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA** に保存します。 ただし、ファイル名と場所は異なる場合があります。  
  
##  <a name="Permissions"></a> Permissions  
  
-   データベース マスター キーを作成するには、 **master** データベースに対する **CONTROL DATABASE** 権限が必要です。  
  
-   DEK を保護する証明書を作成するには、 **master** データベースに対する **CREATE CERTIFICATE** 権限が必要です。  
  
-   暗号化されたデータベースに対する **CONTROL DATABASE** 権限と、データベース暗号化キーの暗号化に使用する証明書または非対称キーに対する **VIEW DEFINITION** 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> 透過的なデータ暗号化で保護されたデータベースを作成するには  

次の手順は、SQL Server Management Studio を使用し、TRANSACT-SQL を使用して、TDE で保護されたデータベースを作成する必要があることを示しています。
  
###  <a name="SSMSCreate"></a> SQL Server Management Studio の使用  
  
1.  データベース マスター キーと証明書を **master** データベース内に作成します。 詳細については、「 **Transact-SQL の使用** 」をご覧ください。  
  
2.  **master** データベースに、サーバー証明書のバックアップを作成します。 詳細については、「 **Transact-SQL の使用** 」をご覧ください。  
  
3.  オブジェクト エクスプローラーで、 **[データベース]** フォルダーを右クリックし、 **[新しいデータベース]** をクリックします。  
  
4.  **[新しいデータベース]** ダイアログ ボックスで、 **[データベース名]** ボックスに新しいデータベースの名前を入力します。  
  
5.  **[所有者]** ボックスに新しいデータベースの所有者を入力します。 または、省略記号 **[...]** をクリックして **[データベース所有者の選択]** ダイアログ ボックスを開きます。 新しいデータベースの作成の詳細については、「 [Create a Database](../../../relational-databases/databases/create-a-database.md)」をご覧ください。  
  
6.  オブジェクト エクスプローラーで、プラス記号をクリックして **[データベース]** フォルダーを展開します。  
  
7.  作成したデータベースを右クリックし、 **[タスク]** をポイントし、 **[データベース暗号化の管理]** をクリックします。  
  
     **[データベース暗号化の管理]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     **暗号化アルゴリズム**  
     データベース暗号化で使用するアルゴリズムを表示または設定します。 既定の暗号化アルゴリズムは**AES128** です。 このフィールドを空白にすることはできません。 暗号化アルゴリズムの詳細については、「 [Choose an Encryption Algorithm](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)」をご覧ください。  
  
     **サーバー証明書の使用**  
     証明書によって保護するように暗号化を設定します。 一覧から選択します。 サーバー証明書に対する **VIEW DEFINITION** 権限がない場合、このリストは空になります。 証明書による暗号化方法が選択されている場合、この値を空にすることはできません。 証明書の詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
     **[サーバー非対称キーの使用]**  
     暗号化が非対称キーで保護されるように設定します。 使用可能な非対称キーのみが表示されます。 TDE を使用してデータベースを暗号化できるのは、EKM モジュールによって保護される非対称キーだけです。  
  
     **[データベース暗号化をオンに設定]**  
     データベースを変更して TDE をオンまたはオフにします。  
  
8.  完了したら、 **[OK]** をクリックします。  

###  <a name="TsqlCreate"></a> Transact-SQL の使用  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 詳細については、以下をご覧ください。  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> 透過的なデータ暗号化で保護されたデータベースを移動するには 

次の手順は、SQL Server Management Studio を使用し、TRANSACT-SQL を使用して、TDE で保護されたデータベースを移動する必要があることを示しています。
  
###  <a name="SSMSMove"></a> SQL Server Management Studio の使用  
  
1.  オブジェクト エクスプローラーで、暗号化したデータベースを右クリックし、 **[タスク]** をポイントして **[デタッチ]** をクリックします。  
  
     **[データベースのデタッチ]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     **[デタッチするデータベース]**  
     デタッチするデータベースを一覧表示します。  
  
     **Database Name**  
     デタッチするデータベースの名前を表示します。  
  
     **[接続の削除]**  
     指定したデータベースへの接続を切断します。  
  
    > [!NOTE]  
    >  アクティブな接続があるデータベースをデタッチすることはできません。  
  
     **統計の更新**  
     既定では、データベースをデタッチしても、古い最適化統計情報が保持されます。既存の最適化統計情報を更新するには、このチェック ボックスをオンにします。  
  
     **[フルテキスト カタログの保持]**  
     既定では、デタッチ操作を行っても、データベースに関連付けられたフルテキスト カタログが保持されます。 これらのカタログを削除するには、 **[フルテキスト カタログの保持]** チェック ボックスをオフにします。 このオプションは、データベースを [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]からアップグレードする場合にのみ表示されます。  
  
     **ステータス**  
     次のどちらかの状態が表示されます: **[準備完了]** または **[準備ができていません]** 。  
  
     **メッセージ**  
     **[メッセージ]** 列に、次のようにデータベースに関する情報が表示される場合があります。  
  
    -   データベースがレプリケーションに含まれている場合、 **[状態]** は **[準備ができていません]** になり、 **[メッセージ]** 列に **[データベースがレプリケートされました]** と表示されます。  
  
    -   データベースにアクティブな接続が 1 つ以上ある場合、 **[状態]** は **[準備ができていません]** になり、 **[メッセージ]** 列に **[\<_アクティブな接続の数_\> のアクティブな接続]** と表示されます。例: **[1 のアクティブな接続]** 。 データベースをデタッチするには、 **[接続の削除]** を選択してアクティブな接続を切断する必要があります。  
  
     メッセージについてより詳しい情報を得るには、ハイパーリンクのテキストをクリックして利用状況モニターを開きます。  
  
2.  **[OK]** をクリックします。  
  
3.  Windows エクスプローラーを使用して、移動元またはコピー元サーバーから移動先またはコピー先サーバーの同じ場所に、データベース ファイルを移動またはコピーします。  
  
4.  エクスプローラーを使用して、移動元またはコピー元サーバーから移動先またはコピー先サーバーの同じ場所に、サーバー証明書と秘密キー ファイルのバックアップを移動またはコピーします。  
  
5.  移動先またはコピー先の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに、データベース マスター キーを作成します。 詳細については、「 **Transact-SQL の使用** 」をご覧ください。  
  
6.  元のサーバー証明書のバックアップ ファイルを使用して、サーバー証明書を再作成します。 詳細については、「 **Transact-SQL の使用** 」をご覧ください。  
  
7.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーで、 **[データベース]** フォルダーを右クリックし、 **[アタッチ]** をクリックします。  
  
8.  **[データベースのインポート]** ダイアログ ボックスで、 **[アタッチするデータベース]** の下の **[追加]** をクリックします。  
  
9. **[データベース ファイルの検索 -** _server\_name_] ダイアログ ボックスで、新しいサーバーにアタッチするデータベース ファイルを選択し、 **[OK]** をクリックします。  
  
     **[データベースのインポート]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     **[アタッチするデータベース]**  
     選択されたデータベースに関する情報を表示します。  
  
     \<空白の列ヘッダー>  
     アタッチ操作の状態を示すアイコンが表示されます。 表示されるアイコンの種類は、下の **[状態]** の説明に示します。  
  
     **[MDF ファイルの場所]**  
     選択した MDF ファイルのパスとファイル名が表示されます。  
  
     **Database Name**  
     データベースの名前が表示されます。  
  
     **[次の名前でアタッチ]**  
     データベースを別の名前でアタッチする場合に、その名前を指定します。  
  
     **[所有者]**  
     データベースの所有者のドロップダウン リストです。これを使用して、必要に応じて別の所有者を選択できます。  
  
     **ステータス**  
     次の表に示すように、データベースの状態を表示します。  
  
    |アイコン|状態テキスト|[説明]|  
    |----------|-----------------|-----------------|  
    |(アイコンなし)|(テキストなし)|このオブジェクトのアタッチ操作が開始されていないか、保留されています。 これは、ダイアログ ボックスを開いたときの既定の状態です。|  
    |緑の右向き三角形|[実行中]|アタッチ操作が開始されましたが、完了していません。|  
    |緑のチェック マーク|成功|オブジェクトは正常にアタッチされました。|  
    |赤い丸の中に白い×印|エラー|アタッチ操作でエラーが発生し、正常に完了しませんでした。|  
    |4 つに区切られた丸印 (左右の領域が黒、上下の領域が白)|停止|ユーザーがアタッチ操作を停止したため、正常に完了しませんでした。|  
    |丸の中に反時計回りの矢印|[ロールバックされました]|アタッチ操作は正常に完了しましたが、他のオブジェクトのアタッチ中にエラーが発生したため、ロールバックされました。|  
  
     **メッセージ**  
     空白のメッセージ、または "ファイルが見つかりません" のハイパーリンクが表示されます。  
  
     **[追加]**  
     主な必須データベース ファイルを検索します。 ユーザーが .mdf ファイルを選択した場合、 **[アタッチするデータベース]** グリッドの対応するフィールドに、対応する情報が自動的に入力されます。  
  
     **[削除]**  
     選択したファイルを **[アタッチするデータベース]** グリッドから削除します。  
  
     **"** _<database_name>_ **" データベースの詳細**  
     デタッチするファイルの名前を表示します。 ファイルのパス名を確認または変更するには、**参照**ボタン ( **[...]** ) をクリックしてください。  
  
    > [!NOTE]  
    >  ファイルが存在しなかった場合、 **[メッセージ]** 列に "見つかりませんでした" と表示されます。 ログ ファイルが見つからない場合は、ログ ファイルが別のディレクトリに置かれているか、削除されています。 **[データベースの詳細]** グリッドでファイル パスを更新し、正しい場所を指定するか、そのログ ファイルをグリッドから削除します。 .ndf データ ファイルが見つからない場合、グリッドのパスを更新して、正しい場所を指定する必要があります。  
  
     **[元のファイル名]**  
     データベースに属している、アタッチされたファイルの名前が表示されます。  
  
     **[ファイルの種類]**  
     ファイルの種類を表します。 **[データ]** または **[ログ]** になります。  
  
     **[現在のファイル パス]**  
     選択されているデータベース ファイルのパスを表示します。 このパスは手作業で編集できます。  
  
     **メッセージ**  
     空白のメッセージ、または **"ファイルが見つかりません"** ハイパーリンクが表示されます。  
  
###  <a name="TsqlMove"></a> Transact-SQL の使用  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 詳細については、以下をご覧ください。  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Azure SQL Database での Transparent Data Encryption](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
  
  
