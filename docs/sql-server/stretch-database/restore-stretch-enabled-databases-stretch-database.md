---
title: Stretch 対応データベースの復元
ms.date: 07/06/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 4b53e333802af9bd70e51ad320300c6f868dea43
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843769"
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>Stretch 対応データベースの復元 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  さまざまな種類の失敗、エラー、障害から修復する必要が生じたときに、バックアップされたデータベースを復元します。
  
  バックアップの詳細については、「 [Stretch 対応データベースのバックアップ](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)」をご覧ください。

> [!TIP]
> バックアップは、完全な高可用性とビジネス継続性ソリューションの一部にすぎません。 高可用性の詳細については、「 [高可用性ソリューション](../../database-engine/sql-server-business-continuity-dr.md)」をご覧ください。

## <a name="restore-your-sql-server-data"></a>SQL Server データの復元
ハードウェアの障害または破損から復元するには、Stretch 対応 SQL Server データベースをバックアップから復元します。 現在使用中の SQL Server の復元方法を引き続き使用できます。 詳細については、「 [復元と復旧の概要](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)」をご覧ください。

SQL Server データベースを復元した後に、ストアド プロシージャ **sys.sp_rda_reauthorize_db** を実行して、Stretch 対応の SQL Server データベースとリモートの Azure データベース間の接続を再確立する必要があります。 詳細については、「 [SQL Server データベースと Azure リモート データベース間の接続を復元する](#reconnect)」をご覧ください。

## <a name="restore-your-remote-azure-data"></a>リモートの Azure データの復元

### <a name="recover-a-live-azure-database"></a>Azure ライブ データベースの復旧
Azure の SQL Server Stretch Database サービスでは、Azure Storage スナップショットを使用して、少なくとも 8 時間ごとにすべてのライブ データのスナップショットを撮ります。 これらのスナップショットは 7 日間保存されます。 これにより、過去 7 日間から最後にスナップショットが撮られた時点までの少なくとも 21 の時点のいずれかの状態にデータを復元できます。

Azure ポータルを使用して、Azure ライブ データベースを過去の状態に復元するには、次の手順を実行します。

1. [Azure ポータル][]にログインします。
2. 画面左側の **[参照]** を選択し、 **[SQL デーベース]** を選択します。
3. 使用中のデータベースに移動して選択します。
4. データベース ブレードの上部にある **[復元]** をクリックします。
5. 新しい **データベース名**を指定し、 **[復元ポイント]** を選択してから **[作成]** をクリックします。
6. データベースの復元処理が開始され、 **[通知]** を使用して監視できます。

### <a name="recover-a-deleted-azure-database"></a>削除された Azure データベースの復旧
Azure の SQL Server Stretch Database サービスでは、データベースが削除される前にデータベースのスナップショットが撮られ、7 日間保持されます。 それ以降、ライブ データベースからのスナップショットは保持されなくなります。 これにより、削除された時点にデータベースを復元できます。

Azure ポータルを使用して、削除された Azure データベースをその時点の状態に復元するには、次の手順を実行します。

1. [Azure ポータル][]にログインします。
2. 画面左側の **[参照]** を選択し、 **[SQL Servers]** を選択します。
3. 使用中のサーバーに移動して選択します。
4. サーバーのブレードで [操作] まで下へスクロールし、 **[削除されたデータベース]** タイルをクリックします。
5. 復元する削除されたデータベースを選択します。
5. 新しい **データベース名** を指定し、 **[作成]** をクリックします。
6. データベースの復元処理が開始され、 **[通知]** を使用して監視できます。

## <a name="reconnect"></a>SQL Server データベースと Azure リモート データベース間の接続を復元する

1.  異なる名前または異なるリージョンの復元された Azure データベースに接続するには、ストアド プロシージャ [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) を実行して、以前の Azure データベースから切断します。  
  
2.  ストアド プロシージャ [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) を実行してローカルの Stretch 対応データベースを Azure データベースに再接続します。  
  
    -   既存のデータベース スコープ資格情報を sysname または varchar(128) 値として指定します。 (varchar(max) は使用しないでください)。資格情報の名前はビュー **sys.database_scoped_credentials** で参照できます。  
  
    -   リモート データのコピーを作成するかどうかを指定し、コピーに接続します (推奨)。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>参照  
 [Stretch 対応データベースのバックアップ](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Azure ポータル]: https://portal.azure.com/
 
