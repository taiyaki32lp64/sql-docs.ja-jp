---
title: マネージド バックアップ - 詳細設定オプションの構成
titleSuffix: to Microsoft Azure
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4bd21bac561a34e6dab779f1db0656dcc8e3175e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242572"
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure への SQL Server マネージド バックアップの詳細設定オプションの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  次のチュートリアルでは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の詳細設定オプションを設定する方法について説明します。 この手順は、その機能が必要な場合のみ必要です。 それ以外の場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にし、既定の動作に依存します。  
  
 各シナリオで、バックアップは `database_name` パラメーターを使用して指定します。 `database_name` が NULL または * の場合、変更はインスタンス レベルで既定の設定に影響します。 インスタンス レベルの設定は、変更後に作成された新しいデータベースにも影響します。  
  
 これらの設定を指定したら、データベースまたはインスタンスで、システム ストアド プロシージャ [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) を使用してマネージド バックアップを有効にできます。 詳細については、「[Microsoft Azure への SQL Server マネージド バックアップを有効にする](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
> [!WARNING]  
>  [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) で [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にする前に、常に高度なオプションとカスタム スケジュール オプションを設定する必要があります。 しない場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にしてこれらの設定を行っている間に、望ましくないバックアップ操作が実行される可能性あります。  
  
## <a name="configure-encryption"></a>暗号化の構成  
 次の手順では、ストアド プロシージャ [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) を使用して暗号化設定を指定する方法を示します。  

1.  **暗号化アルゴリズムを決定する:** 最初に、使用する暗号化アルゴリズムの名前を決定します。 次のアルゴリズムから 1 つ選択します。  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **データベースのマスター キーを作成する:** データベースに格納するマスター キーのコピーを暗号化するためのパスワードを指定します。  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **証明書または非対称キーを作成する:** 暗号化には、証明書または非対称キーのいずれかを使用できます。 次の例では、暗号化に使用するバックアップ証明書を作成します。  
  
    ```sql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **マネージド バックアップ暗号化を設定する:** 対応する値を使用して **managed_backup.sp_backup_config_advanced** ストアド プロシージャを呼び出します。 たとえば、次の例では暗号化に、 `MyDB` という証明書と `MyTestDBBackupEncryptCert` の暗号化アルゴリズムを使用し、 `AES_128` データベースを構成します。  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  前の例で `@database_name` が NULL の場合、設定は SQL Server インスタンスに適用されます。  
  
## <a name="configure-a-custom-backup-schedule"></a>カスタム バックアップ スケジュールの構成  
 次の手順では、ストアド プロシージャ [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) を使用して、カスタム スケジュールを設定する方法を示します。  
  
1.  **完全バックアップの頻度を決定する:** :データベースの完全バックアップを実行する頻度を決定します。 完全バックアップを '毎日' または '毎週' 実行するか選択できます。  
  
2.  **ログ バックアップの頻度を決定する:** ログ バックアップを実行する頻度を決定します。 この値は、分または時間単位です。  
  
3.  **毎週のバックアップの曜日を決定する:** バックアップを毎週実行する場合は、完全バックアップを実行する曜日を選択します。  
  
4.  **バックアップの開始時刻を決定する:** 24 時間表記を使用して、バックアップの開始時刻を選択します。  
  
5.  **バックアップで許可される時間の長さを決定する:** これは、その時間中にバックアップを完了する必要がある時間を指定します。  
  
6.  **カスタム バックアップ スケジュールを構成する:** 次のストアド プロシージャで、`MyDB` データベースのカスタム スケジュールを定義します。 完全バックアップは、毎週 `Monday` に `17:30`に実行されます。 ログ バックアップは `5` 分ごとに実行されます。 バックアップの完了には 2 時間かかります。  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>次の手順  
 高度なオプションとカスタム スケジュールを構成したら、ターゲット データベースまたは SQL Server インスタンスで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にする必要があります。 詳細については、「 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
