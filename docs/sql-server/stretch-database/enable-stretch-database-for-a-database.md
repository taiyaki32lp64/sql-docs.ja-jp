---
title: Enable Stretch Database for a database
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling database
- enabling database for Stretch Database
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: db08d84dd1619d8c9e2e4d8e796abdd0c9d202fc
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844590"
---
# <a name="enable-stretch-database-for-a-database"></a>Enable Stretch Database for a database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database 用にデータベースを構成するには、SQL Server Management Studio でデータベースに対して **[タスク]、[ストレッチ]、[有効にする]** の順に選択し、 **[データベースのストレッチの有効化]** ウィザードを開きます。 Transact-SQL を使用してデータベースの Stretch Database を有効にすることもできます。  
  
 個別のテーブルに対して **[タスク]、[ストレッチ]、[有効にする]** の順に選択した場合、データベースの Stretch Database がまだ有効になっていないと、ウィザードはデータベースの Stretch Database を構成し、ユーザーはプロセスの一部としてテーブルを選択できます。 「[テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」の手順ではなく、この記事の手順に従ってください。  
  
 データベースまたはテーブルで Stretch Database を有効にするには、db_owner アクセス許可が必要です。 データベースで Stretch Database を有効にするには、管理データベースのアクセス許可も必要です。  

> [!NOTE]
> 後で、Stretch Database を無効にする場合は、テーブルまたはデータベースで Stretch Database を無効にしてもリモート オブジェクトは削除されないことに注意してください。 リモート テーブルまたはリモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート オブジェクトを手動で削除するまで、引き続き Azure ストレージのコストが発生します。 
 
## <a name="before-you-get-started"></a>始める前に  
  
-   データベースで Stretch を構成する前に、Stretch Database Advisor を実行して、Stretch を構成できるデータベースとテーブルを識別することをお勧めします。 Stretch Database Advisor はブロックの問題も識別します。 詳細については、「 [Stretch Database Advisor を実行して Stretch Database のデータベースとテーブルを特定する](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)」をご覧ください。  
  
-   [Stretch Database の制限事項](../../sql-server/stretch-database/limitations-for-stretch-database.md)を確認します。  
  
-   Stretch Database はデータを Azure に移行します。 そのため、Azure アカウントとサブスクリプションを請求のために用意する必要があります。 Azure アカウントを取得するには、 [こちらをクリック](https://azure.microsoft.com/pricing/free-trial/)してください。  
  
-   新しい Azure サーバーを作成する、または既存の Azure サーバーを選択するために必要な接続およびログイン情報を入手します。  
  
##  <a name="EnableTSQLServer"></a> 前提条件:サーバーで Stretch Database を有効にする  
 データベースまたはテーブルで Stretch Database を有効にする前に、ローカル サーバーで有効にする必要があります。 この操作には、sysadmin または serveradmin のアクセス許可が必要です。  
  
-   必要な管理アクセス許可がある場合、 **データベースのストレッチの有効化** ウィザードは Stretch 用にサーバーを構成します。  
  
-   必要なアクセス許可がない場合、ユーザーがウィザードを実行する前に管理者が **sp_configure** を実行して手動でオプションを有効にするか、または管理者がウィザードを実行する必要があります。  
  
 手動によってサーバーで Stretch Database を有効にするには、 **sp_configure** を実行して、 **remote data archive** オプションを有効にします。 次の例では、値を 1 に設定することによって **remote data archive** オプションを有効にしています。  
  
```sql
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 詳細については、「[remote data archive サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md)」と「[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」をご覧ください。  
  
##  <a name="Wizard"></a> ウィザードを使用してデータベースで Stretch Database を有効にする  
 入力する必要がある情報や選択など、データベースのストレッチの有効化ウィザードの詳細については、「 [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)」 (データベースのストレッチの有効化ウィザードの実行から開始する) をご覧ください。  
  
##  <a name="EnableTSQLDatabase"></a> Transact-SQL を使用してデータベースで Stretch Database を有効にする  
 個別のテーブルで Stretch Database を有効にする前に、データベースで有効にする必要があります。  
  
 データベースまたはテーブルで Stretch Database を有効にするには、db_owner アクセス許可が必要です。 データベースで Stretch Database を有効にするには、管理データベースのアクセス許可も必要です。  
  
1.  始める前に、Stretch Database で移行するデータ用に既存の Azure サーバーを選択するか、または新しい Azure サーバーを作成します。  
  
2.  Azure サーバーで、SQL Server の IP アドレス範囲に対するファイアウォール規則を作成し、SQL Server がリモート サーバーと通信できるようにします。  

    SQL Server Management Studio (SSMS) のオブジェクト エクスプローラーから Azure サーバーに接続することで、必要とする値を簡単に見つけて、ファイアウォール規則を作成できます。 SSMS で次のダイアログ ボックスが開き、既に必要な IP アドレス値が設定されているので、簡単に規則を作成できます。
    
    ![Stretch 用のファイアウォール規則](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  Stretch Database 用に SQL Server データベースを構成するには、データベースにデータベース マスター キーが必要です。 データベース マスター キーは、Stretch Database がリモート データベースへの接続に使用する資格情報をセキュリティで保護します。 新しいデータベース マスター キーを作成する例を次に示します。  
  
    ```sql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    データベースのマスター キーを作成する方法については、「[CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)」と「[データベース マスター キーの作成](../../relational-databases/security/encryption/create-a-database-master-key.md)」をご覧ください。
    
4.  Stretch Database 用にデータベースを構成するときは、オンプレミスの SQL Server とリモート Azure サーバーの間の通信に使用する資格情報を Stretch Database に提供する必要があります。 この場合、2 つの選択肢があります。  
  
    -   管理者の資格情報を提供できます。  
  
        -   ウィザードを実行して Stretch Database を有効にする場合は、そのときに資格情報を作成できます。  
  
        -   **ALTER DATABASE**を実行して Stretch Database を有効にする場合は、 **ALTER DATABASE** を実行して Stretch Database を有効にする前に、資格情報を手動で作成する必要があります。 
        
        新しい資格情報を作成する例を次に示します。
  
        ```sql  
        CREATE DATABASE SCOPED CREDENTIAL <db_scoped_credential_name>  
            WITH IDENTITY = '<identity>' , SECRET = '<secret>' ;
        GO   
        ```  

         資格情報の詳細については、「[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)」をご覧ください。 資格情報を作成するには、ALTER ANY CREDENTIAL 権限が必要です。  

    -   以下の条件をすべて満たす場合、SQL Server のフェデレーション サービス アカウントを使用して、リモート Azure サーバーと通信できます。  
  
        -   SQL Server のインスタンスを実行しているサービス アカウントがドメイン アカウントである。  
  
        -   Active Directory が Azure Active Directory とフェデレーションされているドメインに、ドメイン アカウントが属している。  
  
        -   Azure Active Directory 認証をサポートするように、リモート Azure サーバーが構成されている。  
  
        -   SQL Server のインスタンスを実行しているサービス アカウントが、リモート Azure サーバー上で dbmanager または sysadmin アカウントとして構成されている。  
  
5.  Stretch Database 用にデータベースを構成するには、ALTER DATABASE コマンドを実行します。  
  
    1.  SERVER 引数では、既存の Azure サーバーの名前を指定します。これには、名前の `.database.windows.net` の部分も含めます (例: `MyStretchDatabaseServer.database.windows.net`)。  
  
    2.  CREDENTIAL 引数で既存の管理者資格情報を指定するか、または FEDERATED_SERVICE_ACCOUNT = ON を指定します。 次の例では既存の資格情報を指定しています。  
  
    ```sql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## <a name="next-steps"></a>次の手順  
-   追加のテーブルを有効にする場合: [テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
-   データ移行の状態を表示する場合: [データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)  
  
-   [データ移行の一時停止と再開 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Stretch 対応データベースのバックアップ](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Stretch 対応データベースの復元](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>参照  
 [Stretch Database Advisor を実行して Stretch Database のデータベースとテーブルを特定する](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
