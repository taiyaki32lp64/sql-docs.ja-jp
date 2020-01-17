---
title: 別のコンピューターへのレポート サーバー データベースの移動 (SSRS ネイティブ モード) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 44a9854d-e333-44f6-bdc7-8837b9f34416
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: be1e4f34356f611e4c76ba57aa12bd13b0bf8f30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65619686"
---
# <a name="moving-the-report-server-databases-to-another-computer-ssrs-native-mode"></a>別のコンピューターへのレポート サーバー データベースの移動 (SSRS ネイティブ モード)

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインストールで使用されるレポート サーバー データベースは、別のコンピューター上のインスタンスに移動できます。 reportserver と reportservertempdb データベースは、一緒に移動またはコピーする必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の使用環境には、両方のデータベースが必要です。reportservertempdb データベースは、移動する reportserver プライマリ データベースに名前を関連付ける必要があります。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モード。  
  
 データベースの移動は、レポート サーバー アイテムに現在定義されているスケジュールされた操作には影響しません。  
  
-   レポート サーバー サービスを初めて再起動したときに、スケジュールが再作成されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、スケジュールを開始する際に使用され、新しいデータベース インスタンスで再作成されます。 このジョブを新しいコンピューターに移動する必要はありませんが、そのコンピューターで今後使用しないジョブは削除することをお勧めします。  
  
-   サブスクリプション、キャッシュされたレポート、およびスナップショットは、移動したデータベースに保持されます。 データベースの移動後にスナップショットが更新されたデータを取得していない場合は、スナップショット オプションを解除し、 **[適用]** を選択して変更を保存します。次に、スケジュールを再作成し、もう一度 **[適用]** を選択して変更を保存します。  
  
-   reportservertempdb に格納される一時的なレポートとユーザー セッション データは、データベースを移動すると保存されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、バックアップと復元、アタッチとデタッチ、コピーなど、データベースを移動するための方法がいくつかあります。 ただし、既存のデータベースを新しいサーバー インスタンスに再配置する場合に、これらすべての方法が適切とは限りません。 レポート サーバー データベースを移動するために使用する方法は、システムの可用性要件によって異なります。 レポート サーバー データベースを移動する最も簡単な方法は、レポート サーバー データベースをアタッチおよびデタッチすることです。 ただし、この方法を使用する場合、データベースをデタッチするときにレポート サーバーをオフラインにする必要があります。 サービスの中断を最小限に抑えるには、バックアップと復元が適しています。ただし、この操作を行うには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行する必要があります。 権限設定がデータベースに保持されないため、データベースをコピーすること (特に、データベース コピー ウィザードの使用) は推奨されていません。  
  
> [!IMPORTANT]  
>  この記事の手順をお勧めできるのは、既存環境に対して行う変更が、レポート サーバー データベースの再配置のみの場合です。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストール全体を移行する場合 (データベースの移動と、データベースを使用するレポート サーバー Windows サービスの ID の変更を行う場合)、接続を再構成して、暗号化キーを再設定する必要があります。  
  
## <a name="detaching-and-attaching-the-report-server-databases"></a>レポート サーバー データベースのデタッチとアタッチ  
 レポート サーバーをオフラインにすると、データベースをデタッチして、使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにデータベースを移動できます。 この方法では、権限がデータベースに保持されます。 SQL Server データベースを使用している場合は、SQL Server の別のインスタンスにそのデータベースを移動する必要があります。 データを移動した後、レポート サーバーがそのレポート サーバー データベースに接続されるように再構成する必要があります。 スケールアウト配置を実行している場合は、各レポート サーバーについて、レポート サーバー データベースの接続を再構成する必要があります。  
  
 次の手順に従ってデータベースを移動します。  
  
1.  移動するレポート サーバー データベースの暗号化キーをバックアップします。 キーは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してバックアップできます。  
  
2.  レポート サーバー サービスを停止します。 サービスは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して停止できます。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を起動し、レポート サーバー データベースをホストしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続を開きます。  
  
4.  レポート サーバー データベースを右クリックし、[タスク] をポイントして **[デタッチ]** をクリックします。 レポート サーバーの一時データベースに対しても、この手順を行います。  
  
5.  使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのデータ フォルダーに .mdf ファイルおよび .ldf ファイルをコピーまたは移動します。 2 つのデータベースを移動するので、4 つのファイルがすべて移動またはコピーされていることを確認してください。  
  
6.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、レポート サーバー データベースを新しくホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続を開きます。  
  
7.  [データベース] ノードを右クリックし、 **[アタッチ]** をクリックします。  
  
8.  **[追加]** をクリックして、アタッチするレポート サーバー データベースの .mdf ファイルおよび .ldf ファイルを選択します。 レポート サーバーの一時データベースに対しても、この手順を行います。  
  
9. データベースをアタッチした後、レポート サーバー データベースおよび一時データベースのデータベース ロールが **RSExecRole** であることを確認します。 **RSExecRole** には、レポート サーバー データベースのテーブルの選択、挿入、更新、削除、および参照を行う権限とストアド プロシージャの実行権限が必要です。 詳細については、「 [RSExecRole の作成](../../reporting-services/security/create-the-rsexecrole.md)」をご覧ください。  
  
10. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバー インスタンスへの接続を開きます。  
  
11. [データベース] ページで新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを選択し、 **[接続]** をクリックします。  
  
12. 移動したレポート サーバー データベースを選択し、 **[適用]** をクリックします。  
  
13. [暗号化キー] ページで、[復元] をクリックします。 キーのバックアップ コピーが格納されているファイルとそのパスワードを指定し、ファイルのロックを解除します。  
  
14. レポート サーバー サービスを再開します。  
  
## <a name="backing-up-and-restoring-the-report-server-databases"></a>レポート サーバー データベースのバックアップと復元  
 レポート サーバーをオフラインにできない場合は、バックアップと復元を使用して、レポート サーバー データベースを再配置できます。 バックアップと復元を実行するには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用する必要があります。 データベースを復元した後、新しいサーバー インスタンスのデータベースを使用できるように、レポート サーバーを構成する必要があります。 詳細については、このトピックの最後にある手順を参照してください。  
  
### <a name="using-backup-and-copyonly-to-backup-the-report-server-databases"></a>レポート サーバー データベースをバックアップする BACKUP および COPY_ONLY の使用  
 データベースをバックアップする場合、COPY_ONLY 引数を設定します。 データベースとログ ファイルの両方を必ずバックアップしてください。  
  
```  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServer  
   SET RECOVERY FULL  
  
-- If the ReportServerData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\ReportServerData.bak'  
  
-- Create a logical backup device, ReportServerLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\ReportServerLog.bak'  
  
-- Back up the full ReportServer database.  
BACKUP DATABASE ReportServer  
   TO ReportServerData  
   WITH COPY_ONLY  
  
-- Back up the ReportServer log.  
BACKUP LOG ReportServer  
   TO ReportServerLog  
   WITH COPY_ONLY  
  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServerTempdb  
   SET RECOVERY FULL  
  
-- If the ReportServerTempDBData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBData',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBData.bak'  
  
-- Create a logical backup device, ReportServerTempDBLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBLog.bak'  
  
-- Back up the full ReportServerTempDB database.  
BACKUP DATABASE ReportServerTempDB  
   TO ReportServerTempDBData  
   WITH COPY_ONLY  
  
-- Back up the ReportServerTempDB log.  
BACKUP LOG ReportServerTempDB  
   TO ReportServerTempDBLog  
   WITH COPY_ONLY  
```  
  
### <a name="using-restore-and-move-to-relocate-the-report-server-databases"></a>レポート サーバー データベースを再配置する RESTORE および MOVE の使用  
 データベースを復元する際には、パスを指定できるように MOVE 引数を使用してください。 NORECOVERY 引数を使用して最初の復元を行うと、データベースが RESTORING 状態で保たれ、ログのバックアップを確認してどのデータベースを復元するかを決定する時間ができます。 最後の手順では、RECOVERY 引数を使用して RESTORE 操作を繰り返します。  
  
 MOVE 引数では、データ ファイルの論理名を使用します。 論理名を検索するには、 ステートメントを実行してください。 `RESTORE FILELISTONLY FROM DISK='C:\ReportServerData.bak';`  
  
 復元するログ ファイルの位置を指定できるように、次の例では FILE 引数を使用しています。 ファイルの位置を検索するには、 ステートメントを実行してください。 `RESTORE HEADERONLY FROM DISK='C:\ReportServerData.bak';`  
  
 データベースとログ ファイルを復元する場合、RESTORE 操作は個別に実行する必要があります。  
  
```  
-- Restore the report server database and move to new instance folder   
RESTORE DATABASE ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore the report server log file to new instance folder   
RESTORE LOG ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore and move the report server temporary database  
RESTORE DATABASE ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Restore the temporary database log file to new instance folder   
RESTORE LOG ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServer  
   WITH RECOVERY  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServerTempDB  
   WITH RECOVERY  
GO  
```  
  
### <a name="how-to-configure-the-report-server-database-connection"></a>レポート サーバー データベースの接続を構成する方法  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバー インスタンスへの接続を開きます。  
  
2.  [データベース] ページの **[データベースの変更]** をクリックします。 **[次へ]** をクリックします。  
  
3.  **[既存のレポート サーバー データベースを選択する]** をクリックします。 **[次へ]** をクリックします。  
  
4.  現在レポート サーバー データベースをホストしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を選択し、 **[接続テスト]** をクリックします。 **[次へ]** をクリックします。  
  
5.  [データベース名] で、使用するレポート サーバー データベースを選択します。 **[次へ]** をクリックします。  
  
6.  レポート サーバーがレポート サーバー データベースに接続するときに使用する資格情報を [資格情報] に指定します。 **[次へ]** をクリックします。  
  
7.  **[次へ]** 、 **[完了]** の順にクリックします。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールでは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] インスタンスに **RSExecRole** ロールが含まれている必要があります。 ロールの作成、ログインの登録、およびロールの割り当ては、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでレポート サーバー データベースの接続を設定する際に行います。 別の方法 (特に、rsconfig.exe コマンド プロンプト ユーティリティを使用する場合) で接続を構成する場合は、レポート サーバーが非動作状態になります。 場合によっては、レポート サーバーを利用可能な状態にするための WMI コードを作成する必要があります。 詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  

## <a name="next-steps"></a>次の手順

[RSExecRole の作成](../../reporting-services/security/create-the-rsexecrole.md)   
[Start and Stop the Report Server Service](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
[レポート サーバー データベース接続の構成](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[自動実行アカウントの構成](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
[Reporting Services 構成マネージャー](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[rsconfig ユーティリティ](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
[暗号化キーの構成と管理](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
[レポート サーバー データベース](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
