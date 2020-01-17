---
title: 可用性グループに対するセカンダリ データベースの準備
description: Always On 可用性グループに参加させるセカンダリ データベースを手動で準備する方法に関する説明。
ms.custom: seodec18
ms.date: 07/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.preparedbs.f1
- sql13.swb.availabilitygroup.configsecondarydbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 9f2feb3c-ea9b-4992-8202-2aeed4f9a6dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19d9171278bac69eb8b092d6bc7ec69dcbcb71ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023711"
---
# <a name="prepare-a-secondary-database-for-an-always-on-availability-group"></a>Always On 可用性グループに対するセカンダリ データベースの準備
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)]、または PowerShell を使用して、[!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] で AlwaysOn 可用性グループのデータベースを準備する方法について説明します。 データベースの準備には、2 つの手順が必要です。 

1. RESTORE WITH NORECOVERY を使用して、セカンダリ レプリカをホストする各サーバー インスタンスに、プライマリ データベースの最新のデータベース バックアップと以降のログ バックアップを復元します。
2. 復元したデータベースを可用性グループに参加させます。  
  
> [!TIP]  
>  既存のログ配布構成がある場合は、ログ配布プライマリ データベースとその 1 つ以上のセカンダリ データベースを、可用性グループ プライマリ レプリカと 1 つ以上のセカンダリ レプリカに変換できる場合があります。 詳細については、「[Always On 可用性グループにログ配布を移行する前提条件](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)」を参照してください。  

##  <a name="Prerequisites"></a> 前提条件と制限  
  
-   データベースを配置するシステムのディスク ドライブに、セカンダリ データベース用に十分な空き領域があることを確認します。  
  
-   セカンダリ データベースの名前は、プライマリ データベースの名前と同じである必要があります。  
  
-   すべて復元操作に RESTORE WITH NORECOVERY を使用します。  
  
-   セカンダリ データベースをプライマリ データベースとは異なるファイル パス (ドライブ文字を含む) に配置する必要がある場合は、復元コマンドでデータベース ファイルごとに WITH MOVE オプションも使用して、それらのファイルをセカンダリ データベースのパスに指定する必要があります。  
  
-   データベースのファイル グループをファイル グループごとに復元する場合は、必ずデータベース全体を復元してください。  
  
-   データベースの復元後、復元された最後のデータ バックアップの後に作成されたすべてのログ バックアップを復元する必要があります (WITH NORECOVERY)。  
  
##  <a name="Recommendations"></a> 推奨事項  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のスタンドアロン インスタンスでは、可能であれば、特定のセカンダリ データベースのファイル パス (ドライブ文字を含む) は、対応するプライマリ データベースのパスと一致させることをお勧めします。 セカンダリ データベースの作成時にデータベース ファイルを移動し、その後でセカンダリ データベースにファイルを追加しようとした場合、ファイルの追加操作が失敗し、セカンダリ データベースが中断される可能性があるためです。  
  
-   セカンダリ データベースを準備する場合は、セカンダリ レプリカの初期化が完了するまでの間、可用性グループ内のデータベースでスケジュールされているログ パックアップを一時停止することを強くお勧めします。  
  
###  <a name="Security"></a> セキュリティ  
 データベースをバックアップするときに、 [TRUSTWORTHY データベース プロパティ](../../../relational-databases/security/trustworthy-database-property.md) は OFF に設定されます。 したがって、新たに復元されたデータベースでは TRUSTWORTHY は常に OFF です。  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。 詳細については、「 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)」を参照してください。  
  
 復元するデータベースがサーバー インスタンスに存在しない場合、RESTORE ステートメントに CREATE DATABASE 権限が必要です。 詳細については、「 [RESTORE &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md)で復元することはできません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
> [!NOTE]  
>  バックアップ ファイルと復元ファイルのパスが、プライマリ レプリカをホストするサーバー インスタンスとセカンダリ レプリカをホストする各インスタンスとで同じ場合は、[新しい可用性グループ ウィザード](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)、[可用性グループへのレプリカ追加ウィザード](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)、または[可用性グループへのデータベース追加ウィザード](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)を使用して、セカンダリ レプリカ データベースを作成できます。  
  
 **セカンダリ データベースを準備するには**  
  
1.  プライマリ データベースの最新のバックアップがない場合は、データベースの新しい完全バックアップか差分バックアップを作成してください。 このバックアップとそれ以降のすべてのログ バックアップは、推奨されるネットワーク共有に配置することをお勧めします。  
  
2.  プライマリ データベースの新しいログ バックアップを 1 つ以上作成します。

   >[!NOTE]
   >プライマリ レプリカのデータベースでトランザクション ログ バックアップがまだキャプチャされていない場合は、トランザクション ログ バックアップが不要な可能性があります。 Microsoft では、可用性グループに新しいデータベースを追加するたびにトランザクション ログ バックアップを実行することをお勧めします。 
  
3.  セカンダリ レプリカをホストするサーバー インスタンスで、プライマリ データベースの完全バックアップ (および必要に応じて差分バックアップ)、それ以降のすべてのログ バックアップの順で復元します。  
  
     **[データベースの復元] の [オプション]** ページで、 **[データベースは操作不可状態のままで、コミットされていないトランザクションはロールバックしない。別のトランザクション ログは復元できます] (RESTORE WITH NORECOVERY)** を選択します。  
  
     プライマリ データベースとセカンダリ データベースのファイル パスが異なる場合、たとえばプライマリ データベースはドライブ "F:" にあり、セカンダリ レプリカをホストするサーバー インスタンスに F: ドライブがない場合は、WITH 句に MOVE オプションを含めてください。  
  
4.  セカンダリ データベースの構成を完了するには、セカンダリ データベースを可用性グループに参加させる必要があります。 詳細については、「[可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  これらのバックアップ操作および復元操作の実行方法については、このセクションの「 [関連するバックアップおよび復元のタスク](#RelatedTasks)」を参照してください。  
  
###  <a name="RelatedTasks"></a> 関連するバックアップおよび復元のタスク  
 **データベースのバックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 **ログ バックアップを作成するには**  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **バックアップを復元するには**  
  
-   [SSMS を使用してデータベース バックアップを復元する](../../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [データベースの差分バックアップの復元 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [データベースを新しい場所に復元する &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **セカンダリ データベースを準備するには**  
  
> [!NOTE]  
>  この手順の例については、このトピックの「 [例 (Transact-SQL)](#ExampleTsql)」を参照してください。  
  
1.  プライマリ データベースの最新の完全バックアップがない場合は、プライマリ レプリカをホストするサーバー インスタンスに接続し、データベースの完全バックアップを作成してください。 このバックアップとそれ以降のすべてのログ バックアップは、推奨されるネットワーク共有に配置することをお勧めします。  
  
2.  セカンダリ レプリカをホストするサーバー インスタンスで、プライマリ データベースの完全バックアップ (および必要に応じて差分バックアップ)、それ以降のすべてのログ バックアップの順で復元します。 すべて復元操作に WITH NORECOVERY を使用します。  
  
     プライマリ データベースとセカンダリ データベースのファイル パスが異なる場合、たとえばプライマリ データベースはドライブ "F:" にあり、セカンダリ レプリカをホストするサーバー インスタンスに F: ドライブがない場合は、WITH 句に MOVE オプションを含めてください。  
  
3.  必要なログ バックアップ以降にプライマリ データベースのログ バックアップを作成した場合は、それらのログ バックアップもセカンダリ レプリカをホストするサーバー インスタンスにコピーして、各ログ バックアップをセカンダリ データベースに適用する必要があります。その際には古いものから順に適用し、毎回 RESTORE WITH NORECOVERY を使用します。  
  
    > [!NOTE]  
    >  プライマリ データベースを作成したばかりでログ バックアップがまだ作成されていない場合や、復旧モデルを単純から完全に変更したばかりの場合には、ログ バックアップが存在しない可能性があります。  
  
4.  セカンダリ データベースの構成を完了するには、セカンダリ データベースを可用性グループに参加させる必要があります。 詳細については、「[可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  これらのバックアップ操作および復元操作の実行方法については、このトピックの「 [関連するバックアップおよび復元のタスク](#RelatedTasks)」を参照してください。  
  
###  <a name="ExampleTsql"></a> Transact-SQL の例  
 次の例では、セカンダリ データベースを準備します。 この例では、既定で単純復旧モデルを使用する [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] サンプル データベースを使用します。  
  
1.  [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースを使用するには、完全復旧モデルが使用されるように変更します。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE MyDB1   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  データベースの復旧モデルを SIMPLE から FULL に変更した後は、完全バックアップを作成します。作成した完全バックアップはセカンダリ データベースの作成に使用できます。 復旧モデルを変更した直後なので、新しいメディア セットを作成するには WITH FORMAT オプションを指定します。 これにより、完全復旧モデルのバックアップを、単純復旧モデルで作成された以前のバックアップと分離できます。 この例では、バックアップ ファイル (C:\\[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].bak) をデータベースと同じドライブに作成します。  
  
    > [!NOTE]  
    >  運用データベースを使用する場合は、必ず別のデバイスにバックアップしてください。  
  
     プライマリ レプリカをホストするサーバー インスタンス (`INSTANCE01`) 上で、次のとおりプライマリ データベースの完全バックアップを作成します。  
  
    ```  
    BACKUP DATABASE MyDB1   
        TO DISK = 'C:\MyDB1.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  セカンダリ レプリカをホストするサーバー インスタンスに完全バックアップをコピーします。  
  
4.  RESTORE WITH NORECOVERY を使用して、セカンダリ レプリカをホストするサーバー インスタンスに完全バックアップを復元します。 復元コマンドは、プライマリ データベースとセカンダリ データベースのパスが同じかどうかによって変わります。  
  
    -   **パスが同じ場合は、次のようにします。**  
  
         セカンダリ レプリカをホストするコンピューターで、次のとおり完全バックアップを復元します。  
  
        ```  
        RESTORE DATABASE MyDB1   
            FROM DISK = 'C:\MyDB1.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **パスが異なる場合は、次のようにします。**  
  
         セカンダリ データベースのパスがプライマリ データベースのパスと異なる (たとえば、ドライブ文字が異なる) 場合、セカンダリ データベースを作成するには、復元操作に MOVE 句が必要です。  
  
        > [!IMPORTANT]  
        >  プライマリ データベースとセカンダリ データベースのパス名が異なる場合は、ファイルを追加することはできません。 ファイル追加操作のログの受信時に、セカンダリ レプリカのサーバー インスタンスがプライマリ データベースで使用されるのと同じパスに新しいファイルを配置しようとするためです。  
  
         たとえば、次のコマンドは、既定の [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]インスタンスのデータ ディレクトリ (C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA) に存在するプライマリ データベースのバックアップを復元します。 データベースの復元操作では、別のクラスター ノードのセカンダリ レプリカをホストする、( [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] AlwaysOn1 *) という*のリモート インスタンスのデータ ディレクトリにデータベースを移動する必要があります。 そこで、データおよびログ ファイルが *C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA* ディレクトリに復元されます。 この復元操作では WITH NORECOVERY を使用してセカンダリ データベースを復元するデータベースに残します。  
  
        ```  
        RESTORE DATABASE MyDB1  
          FROM DISK='C:\MyDB1.bak'  
         WITH NORECOVERY,   
            MOVE 'MyDB1_Data' TO   
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.mdf',   
            MOVE 'MyDB1_Log' TO  
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.ldf';  
        GO  
        ```  
  
5.  完全バックアップを復元した後、プライマリ データベースでログ バックアップを作成する必要があります。 たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、ログを *E:\MyDB1_log.trn* というバックアップ ファイルにバックアップします。  
  
    ```  
    BACKUP LOG MyDB1   
      TO DISK = 'E:\MyDB1_log.trn'   
    GO  
    ```  
  
6.  データベースをセカンダリ レプリカに参加させるには、必要なログ バックアップ (およびそれ以降のすべてのログ バックアップ) を事前に適用する必要があります。  
  
     たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、最初のログを *C:\MyDB1.trn* から復元します。  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  データベースをセカンダリ レプリカに参加させる前に追加のログ バックアップが行われた場合は、RESTORE WITH NORECOVERY を使用して、それらすべてのログ バックアップもセカンダリ レプリカをホストするサーバー インスタンスに順番に復元する必要があります。  
  
     たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、2 つの追加のログを *E:\MyDB1_log.trn* から復元します。  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **セカンダリ データベースを準備するには**  
  
1.  プライマリ データベースの最新のバックアップを作成する必要がある場合は、プライマリ レプリカがホストされているサーバー インスタンスにディレクトリを変更します (**cd**)。  
  
2.  **Backup-SqlDatabase** コマンドレットを使用して各バックアップを作成します。  
  
3.  ディレクトリ変更コマンド (**cd**) を使用して、セカンダリ レプリカがホストされているサーバー インスタンスに移動します。  
  
4.  各プライマリ データベースのデータベースおよびログ バックアップを復元するには、 **restore-SqlDatabase** コマンドレットを使用して、 **NoRecovery** 復元パラメーターを指定します。 プライマリ レプリカをホストするコンピューターとターゲット セカンダリ レプリカをホストするコンピューターとでファイル パスが異なる場合は、 **RelocateFile** 復元パラメーターも使用します。  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
5.  セカンダリ データベースの構成を完了するには、セカンダリ データベースを可用性グループに参加させる必要があります。 詳細については、「[可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="ExamplePSscript"></a> バックアップと復元のスクリプトとコマンドのサンプル  
 次の PowerShell コマンドは、データベースの完全バックアップとトランザクション ログをネットワーク共有にバックアップし、その共有からこれらのバックアップを復元します。 この例では、データベースの復元先のファイル パスとデータベースがバックアップされたファイル パスが同じであると想定しています。  
  
```  
# Create database backup  
Backup-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -ServerInstance "SourceMachine\Instance"  
# Create log backup  
Backup-SqlDatabase -Database "MyDB1" -BackupAction "Log" -BackupFile "\\share\backups\MyDB1.trn" -ServerInstance "SourceMachine\Instance"  
# Restore database backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
# Restore log backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.trn" -RestoreAction "Log" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
  
```  
  
##  <a name="FollowUp"></a> 次の手順  
 セカンダリ データベースの構成を完了するには、新たに復元したデータベースを可用性グループに参加させる必要があります。 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE の引数 &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md)   
 [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
  
