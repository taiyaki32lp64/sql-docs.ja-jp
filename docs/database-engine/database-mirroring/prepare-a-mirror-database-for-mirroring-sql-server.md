---
title: ミラーリングのためのデータベースの準備
description: データベース ミラーリングのための SQL Server データベースを準備する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 11/10/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], preparing for mirroring
- logins [SQL Server], database mirroring
- mirror database [SQL Server]
ms.assetid: 8676f9d8-c451-419b-b934-786997d46c2b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f93ea5a9b37abcfac0310619b971e3ec5f1e625f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255978"
---
# <a name="prepare-a-mirror-database-for-mirroring-sql-server"></a>ミラーリングのためのミラー データベースの準備 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベース ミラーリング セッションを開始する前に、データベース所有者またはシステム管理者は、ミラー データベースを作成し、ミラーリング用に準備しておく必要があります。 新しいミラー データベースを作成するには、少なくとも、プリンシパル データベースの完全バックアップとそれ以降のログ バックアップを作成し、その両方をミラー サーバーのインスタンスに (WITH NORECOVERY を使用して) 復元する必要があります。  
  
 このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でミラー データベースを準備する方法について説明します。  
  
-   **作業を開始する準備:**  
  
     [必要条件](#Requirements)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   [ミラーリングを再開するために既存のミラー データベースを準備するには](#PrepareToRestartMirroring)  
  
-   [新しいミラー データベースを準備するには](#CombinedProcedure)  
  
-   **補足情報:** [ミラー データベースを準備した後](#FollowUp)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Requirements"></a> 必要条件  
  
-   プリンシパル サーバー インスタンスとミラー サーバー インスタンスは、同じバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行されている必要があります。 ミラー サーバーで SQL Server の新しいバージョンを実行することはできますが、この構成は慎重に計画されたアップグレード プロセスにおいてのみ推奨されます。 そのような構成では、自動フェールオーバーが発生したときに SQL Server の古いバージョンにデータを移動できず、データの移動が自動的に保留される可能性があります。 詳細については、「 [ミラー化されたインスタンスのアップグレード](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)」を参照してください。  
  
-   プリンシパル サーバー インスタンスとミラー サーバー インスタンスは、同じエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行されている必要があります。 データベース ミラーリングの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のサポートについては、「[SQL Server 2017 の各エディションとサポートされている機能](~/sql-server/editions-and-components-of-sql-server-2017.md)」を参照してください。  
  
-   このデータベースは、完全復旧モデルを使用する必要があります。  
  
     詳細については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」または「[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」と「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
-   ミラー データベースの名前は、プリンシパル データベースと同じ名前にする必要があります。  
  
-   ミラーリングが機能するには、ミラー データベースは RESTORING 状態である必要があります。 ミラー データベースを準備する際には、すべての復元操作で RESTORE WITH NORECOVERY を使用する必要があります。 少なくとも、WITH NORECOVERY を指定して、プリンシパル データベースの完全バックアップと、以降のすべてのログ バックアップを復元する必要があります。  
  
-   ミラー データベースを作成するシステムのディスク ドライブに、ミラー データベースを保持するのに十分な空き領域を確保する必要があります。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   **master**、 **msdb**、 **temp**、および **model** の各システム データベースはミラー化できません。  
  
-   [Always On 可用性グループ](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)に属しているデータベースはミラー化できません。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   プリンシパル データベースの最新の完全データベース バックアップまたは差分データベース バックアップを使用します。  
  
-   ログ バックアップ ジョブをプリンシパル データベースで非常に頻繁に実行するようにスケジュールすると、ミラーリングが開始されるまでバックアップ ジョブを無効にする必要が生じる場合があります。  
  
-   可能であれば、ミラー データベースのパス (ドライブ文字を含む) を、プリンシパル データベースと同一のパスにします。  
  
     ファイルのパスが異なる場合、たとえば、プリンシパル データベースが "F:" ドライブに存在する一方で、ミラー システムに "F:" ドライブがない場合には、RESTORE ステートメントに MOVE オプションを含める必要があります。  
  
    > [!IMPORTANT]  
    >  ミラーリング セッション中に、セッションに影響を与えずにファイルを追加するには、追加するファイルのパスが両方のサーバーに存在する必要があります。 したがって、ミラー データベースの作成時にデータベース ファイルを移動し、その後でミラー データベースにファイルを追加しようとした場合、ファイルの追加操作が失敗し、ミラーリングが中断されることがあります。 ファイル作成操作の失敗に対処する方法については、「[データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)」を参照してください。  
  
-   プリンシパル データベースにフルテキスト カタログが含まれている場合は、「[データベース ミラーリングとフルテキスト カタログ &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)」を参照することをお勧めします。  
  
-   運用データベースを使用する場合は、必ず別のデバイスにバックアップしてください。  
  
###  <a name="Security"></a> セキュリティ  
 データベースがバックアップされている場合、TRUSTWORTHY は OFF に設定されます。 したがって、新しいミラー データベースでは TRUSTWORTHY は常に OFF です。 フェールオーバー後にデータベースを信頼可能にする必要がある場合は、追加の設定作業が必要です。 詳細については、「 [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)でミラー データベースを準備する方法について説明します。  
  
 データベース マスター キーの自動暗号化解除を有効にする方法については、「 [暗号化されたミラー データベースの設定](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)」を参照してください。  
  
####  <a name="Permissions"></a> Permissions  
 データベース所有者またはシステム管理者。  
  
##  <a name="PrepareToRestartMirroring"></a> ミラーリングを再開するために既存のミラー データベースを準備するには  
 ミラーリングを削除してもミラー データベースが RECOVERING 状態のままである場合、ミラーリングを再開することができます。  
  
1.  プリンシパル データベースで 1 つ以上のログ バックアップを作成します。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」を参照してください。  
  
2.  ミラー データベースで、RESTORE WITH NORECOVERY を使用して、ミラーリングの削除後にプリンシパル データベースで作成されたすべてのログ バックアップを復元します。 詳細については、「 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)でミラー データベースを準備する方法について説明します。  
  
##  <a name="CombinedProcedure"></a> 新しいミラー データベースを準備するには  
 **ミラー データベースを準備するには**  
  
> [!NOTE]  
>  この手順の [!INCLUDE[tsql](../../includes/tsql-md.md)] の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  プリンシパル サーバー インスタンスに接続します。  
  
2.  プリンシパル データベースの完全バックアップまたは差分バックアップのいずれかを作成します。  
  
    -   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
    -   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
3.  通常、プリンシパル データベースで 1 つ以上のログ バックアップを作成する必要があります。 ただし、データベースを作成したばかりでログ バックアップがまだ作成されていない場合や、復旧モデルを SIMPLE から FULL に変更したばかりの場合など、ログ バックアップが不要な場合もあります。  
  
    -   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
4.  両方のシステムからアクセスできるネットワーク ドライブにバックアップがある場合を除いて、データベース バックアップとログ バックアップは、ミラー サーバー インスタンスをホストするシステムにコピーします。  
  
5.  ミラー サーバー インスタンスに接続します。  
  
6.  RESTORE WITH NORECOVERY を使用する場合、ミラー サーバー インスタンスにデータベースの完全バックアップと、必要に応じて、データベースの最新の差分バックアップを復元することで、ミラー データベースを作成します。  
  
    > [!NOTE]  
    >  データベースのファイル グループをファイル グループごとに復元する場合は、必ずデータベース全体を復元してください。  
  
    -   [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
    -   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 」と「 [RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)でミラー データベースを準備する方法について説明します。  
  
7.  RESTORE WITH NORECOVERY を使用して、未処理のログ バックアップをミラー データベースに適用します。  
  
    -   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 データベース ミラーリング セッションを開始する前に、ミラー データベースを作成する必要があります。 ミラー データベースは、ミラーリング セッションを開始する直前に作成してください。  
  
 この例では、既定で単純復旧モデルを使用する [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを使用します。  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースでデータベース ミラーリングを使用するには、完全復旧モデルが使用されるように変更します。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  データベースの復旧モデルを SIMPLE から FULL へ変更した後は、完全バックアップを作成します。作成した完全バックアップはミラー データベースの作成に使用できます。 復旧モデルを変更した直後なので、新しいメディア セットを作成するには WITH FORMAT オプションを指定します。 これにより、完全復旧モデルのバックアップを、単純復旧モデルで作成された以前のバックアップと分離できます。 この例では、バックアップ ファイル (`C:\AdventureWorks.bak`) をデータベースと同じドライブに作成します。  
  
    > [!NOTE]  
    >  運用データベースを使用する場合は、必ず別のデバイスにバックアップしてください。  
  
     プリンシパル サーバー インスタンス ( `PARTNERHOST1`) で、次のようにプリンシパル データベースの完全バックアップを作成します。  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  完全バックアップをミラー サーバーにコピーします。  
  
4.  RESTORE WITH NORECOVERY を使用して、ミラー サーバー インスタンスに完全バックアップを復元します。 復元コマンドは、プリンシパル データベースとミラー データベースのパスが同じかどうかによって変わります。  
  
    -   **パスが同じ場合は、次のようにします。**  
  
         ミラー サーバー インスタンス ( `PARTNERHOST5`) で、次のように完全バックアップを復元します。  
  
        ```  
        RESTORE DATABASE AdventureWorks   
            FROM DISK = 'C:\AdventureWorks.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **パスが異なる場合は、次のようにします。**  
  
         ミラー データベースのパスがプリンシパル データベースのパスと異なる (たとえば、ドライブ文字が異なる) 場合、ミラー データベースを作成するには、復元操作に MOVE 句が必要です。  
  
        > [!IMPORTANT]  
        >  プリンシパル データベースとミラー データベースのパス名が異なる場合は、ファイルを追加することはできません。 これは、ミラーリング サーバー インスタンスでファイル追加操作のログが受信されると、プリンシパル データベースで使用される場所に新しいファイルの追加が試行されるためです。  
  
         たとえば次のコマンドは、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\ にあるプリンシパル データベースのバックアップを、D:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Dat`a\`という別の場所 (ミラー データベースが配置される場所) に復元します。  
  
        ```  
        RESTORE DATABASE AdventureWorks  
           FROM DISK='C:\AdventureWorks.bak'  
           WITH NORECOVERY,   
              MOVE 'AdventureWorks_Data' TO   
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Data.mdf',   
              MOVE 'AdventureWorks_Log' TO  
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Log.ldf';  
        GO  
        ```  
  
5.  完全バックアップを作成した後、プリンシパル データベースでログ バックアップを作成する必要があります。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、前回の完全バックアップで使用したものと同じファイルにログをバックアップします。  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  ミラーリングを開始する前に、必要なログ バックアップ (および、それ以降のログ バックアップ) を適用する必要があります。  
  
     たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、最初のログを `C:\AdventureWorks.bak`から復元します。  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  ミラーリングを開始する前に追加のログ バックアップが作成された場合は、それらのログ バックアップもすべて復元する必要があります。すべてのログ バックアップを順番に、WITH NORECOVERY を使用して、ミラー サーバーに復元します。  
  
     たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、2 つの追加のログを `C:\AdventureWorks.bak`から復元します。  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
 データベース ミラーリングの設定、セキュリティの設定、ミラー データベースの準備、パートナーの設定、およびミラーリング監視サーバーの追加をすべて含む例については、「 [データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)でミラー データベースを準備する方法について説明します。  
  
##  <a name="FollowUp"></a>補足情報: ミラー データベースを準備した後  
  
1.  最新の RESTORE LOG 操作の後、ログ バックアップを採取している場合は、ミラーリングを開始する前に、採取したすべてのログ バックアップを手動で適用する必要があります (WITH NORECOVERY を使用します。  
  
2.  ミラーリング セッションを再開します。 詳細については、「 [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md) を使用して、 [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)でミラー データベースを準備する方法について説明します。  
  
3.  プリンシパル データベースのバックアップ ジョブを無効にする場合は、ジョブを再度有効にします。  
  
4.  フェールオーバー後にデータベースを信頼可能にする必要がある場合は、ミラーリングを開始した後で追加の設定が必要です。 詳細については、「 [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)でミラー データベースを準備する方法について説明します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [暗号化されたミラー データベースの設定](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [データベース ミラーリングと Always On 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [データベース ミラーリングとフルテキスト カタログ &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)   
 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)  
  
  

