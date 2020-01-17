---
title: Stretch Database を無効にして、リモート データを戻す
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 80974811f45a88b740aa8d84ea9ac67c2c2c1c07
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843820"
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>Stretch Database を無効にして、リモート データを戻す
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  テーブルに対する Stretch Database を無効にするには、SQL Server Management Studio のテーブルで **[拡張する]** を選択します。 以下のオプションの 1 つを選択します。  
  
-   **無効化 | Azure からデータを戻します**。 Azure から SQL Server にテーブルのリモート データをコピーして戻し、テーブルに対する Stretch Database を無効にします。 この操作によりデータ転送コストが発生し、取り消すことはできません。  
  
-   **無効化 | Azure にデータを残します**。 テーブルに対する Stretch Database を無効にします。  Azure のテーブルのリモート データを破棄します。  
  
 Transact-SQL を使用してテーブルまたはデータベースで Stretch Database を無効にすることもできます。  
  
 テーブルに対する Stretch Database を無効にすると、データの移行が停止し、クエリの結果にリモート テーブルからの結果が含まれなくなります。  
  
 単にデータの移行を一時停止する場合は、「 [データ移行の一時停止と再開 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
> [!NOTE]
> テーブルまたはデータベースで Stretch Database を無効にしても、リモート オブジェクトは削除されません。 リモート テーブルまたはリモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート オブジェクトを削除するまで、引き続き Azure ストレージのコストが発生します。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」をご覧ください。  
  
## <a name="disable-stretch-database-for-a-table"></a>テーブルに対する Stretch Database を無効にする  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>SQL Server Management Studio を使用して、テーブルに対する Stretch Database を無効にする  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、Stretch Database を無効にするテーブルを選択します。  
  
2.  右クリックして **[拡張する]** を選択し、次のオプションのいずれかを選択します。  
  
    -   **無効化 | Azure からデータを戻します**。 Azure から SQL Server にテーブルのリモート データをコピーして戻し、テーブルに対する Stretch Database を無効にします。 このコマンドは取り消すことができません。  
  
        > [!NOTE]
        > テーブルのリモート データを Azure から SQL Server にコピーして戻すと、データ転送コストが発生します。 詳細については、「 [Data Transfers (データ転送) の料金詳細](https://azure.microsoft.com/pricing/details/data-transfers/)」を参照してください。  
  
         すべてのリモート データが Azure から SQL Server にコピーして戻されると、テーブルに対する Stretch は無効になります。  
  
    -   **無効化 | Azure にデータを残します**。 テーブルに対する Stretch Database を無効にします。  Azure のテーブルのリモート データを破棄します。  
  
    > [!NOTE]
    > テーブルで Stretch Database を無効にしても、リモート データまたはリモート テーブルは削除されません。 リモート テーブルを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート テーブルを削除するまで、引き続き Azure のコストが発生します。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」をご覧ください。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>Transact-SQL を使用してテーブルに対する Stretch Database を無効にする  
  
-   テーブルに対する Stretch を無効にして、テーブルのリモート データを Azure から SQL Server にコピーして戻すには、次のコマンドを実行します。すべてのリモート データが Azure から SQL Server にコピーして戻されると、テーブルに対する Stretch は無効になります。

    このコマンドは取り消すことができません。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > テーブルのリモート データを Azure から SQL Server にコピーして戻すと、データ転送コストが発生します。 詳細については、「 [Data Transfers (データ転送) の料金詳細](https://azure.microsoft.com/pricing/details/data-transfers/)」を参照してください。    
  
-   テーブルに対する Stretch を無効にして、リモート データを破棄するには、次のコマンドを実行します。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> テーブルで Stretch Database を無効にしても、リモート データまたはリモート テーブルは削除されません。 リモート テーブルを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート テーブルを削除するまで、引き続き Azure のコストが発生します。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」をご覧ください。  
  
## <a name="disable-stretch-database-for-a-database"></a>データベースに対する Stretch Database を無効にする  
 データベースに対する Stretch Database を無効にする前に、データベース内で Stretch が有効な個々のテーブルに対する Stretch Database を無効にする必要があります。  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>SQL Server Management Studio を使用して、データベースに対する Stretch Database を無効にする  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、Stretch Database を無効にするデータベースを選択します。  
  
2.  右クリックして **[タスク]** を選択し、 **[拡張する]** を選択してから **[無効にする]** を選択します。  
  
> [!NOTE]
> データベースで Stretch Database を無効にしても、リモート データベースは削除されません。 リモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート データベースを削除するまで、引き続き Azure のコストが発生します。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」をご覧ください。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>Transact-SQL を使用してデータベースに対する Stretch Database を無効にする  
 次のコマンドを実行します。  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> データベースで Stretch Database を無効にしても、リモート データベースは削除されません。 リモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート データベースを削除するまで、引き続き Azure のコストが発生します。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [データ移行の一時停止と再開 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
