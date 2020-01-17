---
title: クイック スタート:Azure Blob Storage サービスへのバックアップと復元
ms.custom: seo-dt-2019
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: quickstart
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: 24847d7b14341e9a1d5a4d874eb0046f53261fea
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165526"
---
# <a name="quickstart-sql-backup-and-restore-to-azure-blob-storage-service"></a>クイック スタート:Azure Blob Storage サービスへの SQL のバックアップと復元
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
このクイックスタートでは、Azure Blob Storage サービスへのバックアップの書き込みと、Azure Blob Storage サービスからの復元を実行する方法について学習できます。  この記事では、Azure BLOB コンテナーを作成し、Blob service にバックアップを書き込んだ後、復元を実行する方法について説明します。
  
## <a name="prerequisites"></a>前提条件  
このクイックスタートを完了するには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバックアップと復元の概念および T-SQL 構文についての知識が必要です。  Azure ストレージ アカウント、SQL Server Management Studio (SSMS)、および SQL Server または Azure SQL Database マネージド インスタンスが実行されているサーバーへのアクセスが必要です。 また、BACKUP コマンドと RESTORE コマンドの実行に使用するアカウントは、**alter any credential** 権限を持つ **db_backup operator** データベース ロールに属している必要があります。 

- 無料の [Azure アカウント](https://azure.microsoft.com/offers/ms-azr-0044p/)を取得する。
- [Azure ストレージ アカウント](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)を作成します。
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールするか、[Azure SQL 仮想マシン](/azure/sql-database/sql-database-managed-instance-configure-vm)または[ポイント対サイト](/azure/sql-database/sql-database-managed-instance-configure-p2s)[によって確立された接続を使用して](/azure/sql-database/sql-database-managed-instance-get-started)マネージド インスタンスをデプロイします。
- ユーザー アカウントを [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) のロールに割り当て、[alter any credential](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 権限を付与する。 

## <a name="create-azure-blob-container"></a>Azure BLOB コンテナーを作成する
コンテナーには、一連の BLOB をグループ化するコンテナーが用意されています。 すべての BLOB は 1 つのコンテナーに存在する必要があります。 ストレージ アカウントには、コンテナーを無制限に含めることができますが、少なくとも 1 つのコンテナーが必要です。 コンテナーには、BLOB を無制限に格納できます。 

コンテナーを作成するには、次の手順を実行します。

1. Azure portal を開きます。 
1. ストレージ アカウントに移動します。 
1. ストレージ アカウントを選択し、 **[Blob Services]\(Blob services\)** までスクロールします。
1. **[BLOB]** を選択し、 **[+ Container]\(+ コンテナー\)** を選択して新しいコンテナーを追加します。 
1. コンテナーの名前を入力し、指定したコンテナー名をメモしておきます。 この情報は、後でこのクイックスタートの T-SQL ステートメントの URL (バックアップ ファイルのパス) 内で使用されます。 
1. **[OK]** を選択します。 
    
    ![新しいコンテナー](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)

  > [!NOTE]
  > ストレージ アカウントへの認証は、パブリック コンテナーの作成を選択した場合でも、SQL Server のバックアップと復元に必要です。 コンテナーは、REST API を使用してプログラムで作成することもできます。 詳しくは、「[Create Container](https://docs.microsoft.com/rest/api/storageservices/Create-Container)」をご覧ください

## <a name="create-a-test-database"></a>テスト データベースを作成する 
このステップでは、SQL Server Management Studio (SSMS) を使用してテスト データベースを作成します。 

1. [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) を起動し、SQL Server インスタンスに接続します。
1. **[新しいクエリ]** ウィンドウを開きます。 
1. 次の Transact-SQL (T-SQL) コードを実行して、テスト データベースを作成します。 新しいデータベースを表示するには、**オブジェクト エクスプローラー**の **[データベース]** ノードを最新の情報に更新します。 Azure SQL Database マネージド インスタンス上に新しく作成されたデータベースでは自動的に TDE が有効になっているので、続行するにはそれを無効にする必要があります。 

```sql
USE [master]
GO

-- Create database
CREATE DATABASE [SQLTestDB]
GO

-- Create table in database
USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO

-- Populate table 
USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO

-- Disable TDE for newly-created databases on a managed instance 
USE [SQLTestDB];
GO
ALTER DATABASE [SQLTestDB] SET ENCRYPTION OFF;
GO
```

## <a name="create-credential"></a>資格情報の作成

次の手順に従って、SQL Server Management Studio の GUI を使用して資格情報を作成します。 または、[プログラムで](tutorial-use-azure-blob-storage-service-with-sql-server-2016.md#2---create-a-sql-server-credential-using-a-shared-access-signature)資格情報を作成することもできます。 

1. [SQL Server Management Studio(SSMS)](../ssms/download-sql-server-management-studio-ssms.md) の**オブジェクト エクスプローラー**で、 **[データベース]** ノードを展開します。
1. 新しい `SQLTestDB` データベースを右クリックして、 **[タスク]** をポイントし、 **[バックアップ...]** を選択して、**データベースのバックアップ** ウィザードを起動します。 
1. **[バックアップ先]** ドロップダウンから **[URL]** を選択し、 **[追加]** を選択して、 **[バックアップ先の選択]** ダイアログ ボックスを開きます。 

   ![URL にバックアップする](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. **[バックアップ先の選択]** ダイアログ ボックスで **[新しいコンテナー]** を選択して、 **[Microsoft サブスクリプションへの接続]** ウィンドウを開きます。 

   ![バックアップ先](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-backup-destination.png)

1. **[サインイン]** を選択して Azure portal にサインインし、サインイン プロセスを続けます。 
1. ドロップダウンからお使いの**サブスクリプション**を選択します。 
1. ドロップダウンからお使いの**ストレージ アカウント**を選択します。 
1. ドロップダウンから、前に作成したコンテナーを選択します。 
1. **[資格情報の作成]** を選択して、*Shared Access Signature (SAS)* を生成します。  **この値は、復元に必要なため、保存しておいてください。**

   ![資格情報の作成](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/create-credential.png)

1. **[OK]** を選択して、 **[Microsoft サブスクリプションへの接続]** ウィンドウを閉じます。 これにより、 **[バックアップ先の選択] *ダイアログ ボックスに "* Azure ストレージ コンテナー**" の値が設定されます。 **[OK]** を選択して、選択したストレージ コンテナーを選択し、ダイアログ ボックスを閉じます。 
1. この時点で、次のセクションのステップ 4 に進んでデータベースのバックアップを作成するか、または Transact-SQL を使用してデータベースをバックアップする場合は**データベースのバックアップ** ウィザードを閉じることができます。 


## <a name="back-up-database"></a>データベースをバックアップする
このステップでは、SQL Server Management Studio の GUI または Transact-SQL (T-SQL) を使用して、データベース `SQLTestDB` を Azure Blob ストレージ アカウントにバックアップします。 

# <a name="ssmstabssms"></a>[SSMS](#tab/SSMS)

1. **データベースのバックアップ** ウィザードを閉じた場合は、[SQL Server Management Studio(SSMS)](../ssms/download-sql-server-management-studio-ssms.md) の**オブジェクト エクスプローラー**で、 **[データベース]** ノードを展開します。
1. 新しい `SQLTestDB` データベースを右クリックして、 **[タスク]** をポイントし、 **[バックアップ...]** を選択して、**データベースのバックアップ** ウィザードを起動します。 
1. **[バックアップ先]** ドロップダウンから **[URL]** を選択し、 **[追加]** を選択して、 **[バックアップ先の選択]** ダイアログ ボックスを開きます。 

   ![URL にバックアップする](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. 前のステップで作成したコンテナーを **[Azure ストレージ コンテナー]** ドロップダウンで選択します。 

   ![[Azure ストレージ コンテナー]](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/azure-storage-container.png)

1. **データベースのバックアップ** ウィザードで **[OK]** を選択して、データベースをバックアップします。 
1. データベースが正常にバックアップされたら **[OK]** を選択し、バックアップ関連のウィンドウをすべて閉じます。 

   > [!TIP]
   > **データベースのバックアップ** ウィザードの上部にある **[スクリプト]** を選択して、このコマンドの背後にある Transact-SQL をスクリプト化できます。![[スクリプト] コマンド](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/script-backup-command.png)


# <a name="transact-sqltabtsql"></a>[Transact-SQL](#tab/tsql)

Transact-SQL を使用し、次のコマンドを実行して、データベースをバックアップします。 


```sql
USE [master]

BACKUP DATABASE [SQLTestDB] 
TO  URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak' 
WITH  COPY_ONLY, CHECKSUM
GO
```

---

## <a name="delete-database"></a>データベースの削除
このステップでは、復元を実行する前にデータベースを削除します。 このステップは、このチュートリアルの目的でのみ必要であり、通常のデータベース管理手順では使用されない可能性があります。 このステップは省略できますが、その場合、オンプレミスのデータベースを正常に復元するには、マネージド インスタンスでの復元中にデータベースの名前を変更するか、復元コマンド `WITH REPLACE` を実行する必要があります。 

# <a name="ssmstabssms"></a>[SSMS](#tab/SSMS)

1. **オブジェクト エクスプローラー**で **[データベース]** ノードを展開し、`SQLTestDB` データベースを右クリックして [削除] を選択し、**オブジェクトの削除**ウィザードを起動します。 
1. マネージド インスタンスで **[OK]** を選択して、データベースを削除します。 オンプレミスの場合は、 **[既存の接続を閉じる]** の横のチェック ボックスをオンにしてから **[OK]** を選択して、データベースを削除します。 

# <a name="transact-sqltabtsql"></a>[Transact-SQL](#tab/tsql)

次の Transact-SQL コマンドを実行して、データベースを削除します。

```sql
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO

-- If connections currently exist on-premises, you'll need to set the database into single user mode first
USE [master]
GO
ALTER DATABASE [SQLTestDB] SET  SINGLE_USER WITH ROLLBACK IMMEDIATE
GO
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO
```

---


## <a name="restore-database"></a>ダイアログ ボックスの 
このステップでは、SQL Server Management Studio の GUI または Transact-SQL を使用して、データベースを復元します。 

# <a name="ssmstabssms"></a>[SSMS](#tab/SSMS)

1. SQL Server Management Studio の**オブジェクト エクスプローラー**で **[データベース]** ノードを右クリックし、 **[データベースの復元]** を選択します。 
1. **[デバイス]** を選択し、省略記号 [...] を選択してデバイスを選択します。 

   ![デバイスの復元の選択](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-device.png)

1. **[バックアップ メディアの種類]** ドロップダウンから **[URL]** を選択し、 **[追加]** を選択してデバイスを追加します。 

   ![バックアップ デバイスの追加](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/add-backup-device.png)

1. ドロップダウンからコンテナーを選択し、資格情報を作成するときに保存した Shared Access Signature (SAS) を貼り付けます。 

   ![バックアップ先](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/restore-from-container.png)

1. **[OK]** を選択して、バックアップ ファイルの場所を選択します。 
1. **[コンテナー]** を展開し、バックアップ ファイルが存在するコンテナーを選択します。 
1. 復元するバックアップ ファイルを選択し、 **[OK]** を選択します。 ファイルが表示されない場合は、間違った SAS キーを使用している可能性があります。 前と同じ手順に従ってコンテナーを追加することで、SAS キーを再生成することができます。 

   ![ファイルの復元の選択](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-file.png)

1. **[OK]** を選択すると **[バックアップ デバイスの選択]** ダイアログ ボックスが閉じます。 
1. **[OK]** を選択してデータベースを復元します。 

# <a name="transact-sqltabtsql"></a>[Transact-SQL](#tab/tsql)

Azure Blob Storage からオンプレミスのデータベースを復元するには、独自のストレージ アカウントを使用するように次の Transact-SQL コマンドを変更した後、新しいクエリ ウィンドウで実行します。 

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] FROM 
URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak'
```

---


## <a name="see-also"></a>参照 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] バックアップに Azure Blob Storage サービスを使用する場合の概念やベスト プラクティスについて、次の推奨トピックで説明しています。  
  
-   [Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
