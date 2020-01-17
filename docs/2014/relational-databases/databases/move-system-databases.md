---
title: システム データベースの移動 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- moving system databases
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- tempdb database [SQL Server], moving
- system databases [SQL Server], moving
- scheduled disk maintenace [SQL Server]
- moving databases
- msdb database [SQL Server], moving
- moving database files
- relocating database files
- planned database relocations [SQL Server]
- master database [SQL Server], moving
- model database [SQL Server], moving
- Resource database [SQL Server]
- databases [SQL Server], moving
ms.assetid: 72bb62ee-9602-4f71-be51-c466c1670878
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da6b02061ca12210f78ee48b9d3a78c30d43e0b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871539"
---
# <a name="move-system-databases"></a>システム データベースの移動
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のシステム データベースを移動する方法について説明します。 システム データベースの移動は、次の状況で便利な場合があります。  
  
-   障害復旧。 たとえば、ハードウェア障害により、データベースが問題のあるモードになっている場合や、シャットダウンされた場合など。  
  
-   計画に従った再配置。  
  
-   スケジュールされたディスク メンテナンスとしての再配置。  
  
 次の手順は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の同じインスタンス内でデータベース ファイルを移動する場合に適用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスにデータベースを移動する場合や、別のサーバーに移動する場合は、 [バックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md) 操作か [デタッチとアタッチ](move-a-database-using-detach-and-attach-transact-sql.md) 操作を使用します。  
  
 このトピックの手順では、データベース ファイルの論理名が必要です。 論理名を取得するには、 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) カタログ ビューで name 列に対するクエリを実行します。  
  
> [!IMPORTANT]  
>  システム データベースを移動した後に master データベースを再構築すると、すべてのシステム データベースがそれぞれ既定の場所にインストールされるため、システム データベースを再度移動する必要があります。  
  
##  <a name="Intro"></a> **このトピックの「**  
  
-   [計画的再配置とスケジュールされたディスク メンテナンスの手順](#Planned)  
  
-   [障害復旧の手順](#Failure)  
  
-   [Master データベースの移動](#master)  
  
-   [Resource データベースの移動](#Resource)  
  
-   [補足情報:すべてのシステム データベースを移動した後](#Follow)  
  
-   [使用例](#Examples)  
  
##  <a name="Planned"></a> 計画に従った再配置とスケジュールされたディスク メンテナンスの手順  
 計画に従った再配置やスケジュールされたメンテナンス操作の中でシステム データベースのデータ ファイルやログ ファイルを移動するには、次の手順を実行します。 この手順は、master データベースと Resource データベース以外のすべてのシステム データベースに適用されます。  
  
1.  移動対象のそれぞれのファイルに対して、次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
2.  メンテナンスを行うため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを停止するか、システムをシャットダウンします。 詳しくは、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」をご覧ください。  
  
3.  ファイルを新しい場所に移動します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスまたはサーバーを再起動します。 詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md) 」を参照してください。  
  
5.  次のクエリを実行して、ファイルが変更されたことを確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
 msdb データベースが移動され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで [データベース メール](../database-mail/database-mail.md)が構成されている場合は、次の追加の手順を実行します。  
  
1.  次のクエリを実行して、msdb データベースで [!INCLUDE[ssSB](../../../includes/sssb-md.md)] が有効になっていることを確認します。  
  
    ```  
    SELECT is_broker_enabled   
    FROM sys.databases  
    WHERE name = N'msdb';  
    ```  
  
     [!INCLUDE[ssSB](../../../includes/sssb-md.md)] を有効にする方法の詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
2.  テスト メールを送信して、データベース メールが動作していることを確認します。  
  
##  <a name="Failure"></a> 障害復旧の手順  
 ハードウェア障害が原因でファイルを移動する必要がある場合、次の手順に従って別の場所にファイルを再配置します。 この手順は、master データベースと Resource データベース以外のすべてのシステム データベースに適用されます。  
  
> [!IMPORTANT]  
>  データベースを起動できないとき、つまり、データベースが問題のあるモードか復旧できない状態にある場合、ファイルを移動できるのは、sysadmin 固定ロールのメンバーだけです。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが起動していたら停止します。  
  
2.  コマンド プロンプトで次のいずれかのコマンドを入力し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを master のみを復旧するモードで開始します。 これらのコマンドで指定されるパラメーターでは、大文字と小文字が区別されます。 パラメーターが次のように指定されていない場合、コマンドは失敗します。  
  
    -   既定 (MSSQLSERVER) のインスタンスの場合は、次のコマンドを実行します。  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   名前付きインスタンスの場合は、次のコマンドを実行します。  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     詳しくは、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」をご覧ください。  
  
3.  移動対象の各ファイルに対して、 **sqlcmd** コマンドか [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
     **sqlcmd** ユーティリティの使用方法については、「 [sqlcmd ユーティリティの使用](../scripting/sqlcmd-use-the-utility.md)」を参照してください。  
  
4.  **sqlcmd** ユーティリティまたは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を終了します。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを停止します。 たとえば、 `NET STOP MSSQLSERVER`を実行します。  
  
6.  ファイルを新しい場所に移動します。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを再起動します。 たとえば、 `NET START MSSQLSERVER`を実行します。  
  
8.  次のクエリを実行して、ファイルが変更されたことを確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
##  <a name="master"></a> master データベースの移動  
 master データベースを移動するには、次の手順を実行します。  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントし、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **[SQL Server のサービス]** ノードで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス (たとえば、 **[SQL Server (MSSQLSERVER)]** ) を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[SQL Server (***instance_name***) のプロパティ]** ダイアログ ボックスで、 **[起動時のパラメーター]** タブをクリックします。  
  
4.  **[既存のパラメーター]** ボックスで -d パラメーターを選択して、マスター データ ファイルを移動します。 **[更新]** をクリックして変更を保存します。  
  
     **[起動時のパラメーターの指定]** ボックスで、パラメーターを master データベースの新しいパスに変更します。  
  
5.  **[既存のパラメーター]** ボックスで -l パラメーターを選択して、マスター ログ ファイルを移動します。 **[更新]** をクリックして変更を保存します。  
  
     **[起動時のパラメーターの指定]** ボックスで、パラメーターを master データベースの新しいパスに変更します。  
  
     `-d` パラメーターの後にデータ ファイルのパラメーター値を指定し、 `-l` パラメーターの後にログ ファイルのパラメーター値を指定します。 次の例は、マスター データ ファイルの既定の場所のパラメーター値を示します。  
  
     `-dC:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\master.mdf`  
  
     `-lC:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\mastlog.ldf`  
  
     マスター データ ファイルの計画に従った再配置場所が `E:\SQLData`の場合、パラメーター値を次のように変更します。  
  
     `-dE:\SQLData\master.mdf`  
  
     `-lE:\SQLData\mastlog.ldf`  
  
6.  インスタンス名を右クリックして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [停止] **をクリックし、** のインスタンスを停止します。  
  
7.  master.mdf ファイルおよび mastlog.ldf ファイルを新しい場所に移動します。  
  
8.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを再起動します。  
  
9. master データベースのファイルが変更されたことを確認するため、次のクエリを実行します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID('master');  
    GO  
    ```  
  
##  <a name="Resource"></a> Resource データベースの移動  
 Resource データベースの既定の場所は、\<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\\ です。 データベースを移動することはできません。  
  
##  <a name="Follow"></a> 補足情報:すべてのシステム データベースを移動した後  
 すべてのシステム データベースを、新しいドライブやボリューム、または別のドライブ文字を使用した別のサーバーに移動した場合は、次の更新を行います。  
  
-   SQL Server エージェントのログ パスを変更します。 このパスを更新しないと、SQL Server エージェントは起動しません。  
  
-   データベースの既定の場所を変更します。 既定の場所として指定したドライブ文字やパスが存在しない場合、新しいデータベースが作成されない可能性があります。  
  
#### <a name="change-the-sql-server-agent-log-path"></a>SQL Server エージェントのログ パスの変更  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、 **[SQL Server エージェント]** を展開します。  
  
2.  **[エラー ログ]** を右クリックし、 **[構成]** をクリックします。  
  
3.  **SQL Server エージェント エラー ログの構成］** ダイアログ ボックスで、SQLAGENT.OUT ファイルの新しい場所を指定します。 既定の場所は C:\Program files \microsoft SQL Server\MSSQL12。 < instance_name > \MSSQL\Log\\します。  
  
#### <a name="change-the-database-default-location"></a>データベースの既定の場所の変更  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、SQL Server のサーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[サーバーのプロパティ]** ダイアログ ボックスで、 **[データベースの設定]** を選択します。  
  
3.  **[データベースの既定の場所]** で、データ ファイルとログ ファイルの両方の新しい場所を参照します。  
  
4.  変更を完了するため、SQL Server サービスをいったん停止してから開始します。  
  
##  <a name="Examples"></a> 使用例  
  
### <a name="a-moving-the-tempdb-database"></a>A. tempdb データベースを移動する  
 次の例では、計画に従った再配置の一環として、 `tempdb` データ ファイルとログ ファイルを新しい場所に移動します。  
  
> [!NOTE]  
>  tempdb は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが開始されるたびに再作成されるので、データ ファイルとログ ファイルを物理的に移動する必要はありません。 手順 3. でサービスを再起動すると、新しい場所にファイルが作成されます。 サービスを再起動するまでは、tempdb は既存の場所のデータ ファイルとログ ファイルを使用し続けます。  
  
1.  `tempdb` データベースの論理ファイル名と、ディスク上での現在の場所を確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    GO  
    ```  
  
2.  `ALTER DATABASE`を使用して、各ファイルの場所を変更します。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'F:\SQLLog\templog.ldf');  
    GO  
    ```  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスをいったん停止してから再起動します。  
  
4.  ファイルの変更を確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    ```  
  
5.  `tempdb.mdf` ファイルおよび `templog.ldf` ファイルを元の場所から削除します。  
  
## <a name="see-also"></a>参照  
 [Resource データベース](resource-database.md)   
 [tempdb データベース](tempdb-database.md)   
 [master データベース](master-database.md)   
 [msdb データベース](msdb-database.md)   
 [model データベース](model-database.md)   
 [ユーザー データベースの移動](move-user-databases.md)   
 [データベース ファイルの移動](move-database-files.md)   
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [システム データベースの再構築](system-databases.md)  
  
  
