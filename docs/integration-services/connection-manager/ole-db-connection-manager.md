---
title: OLE DB 接続マネージャー | Microsoft Docs
description: OLE DB 接続マネージャーを使用すると、パッケージは OLE DB プロバイダーを使用してデータ ソースに接続できます。
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa5d978126807e1fb83c08a1d1b8d9d7b74d8368
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687173"
---
# <a name="ole-db-connection-manager"></a>OLE DB 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


OLE DB 接続マネージャーを使用すると、パッケージは OLE DB プロバイダーを使用してデータ ソースに接続できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する OLE DB 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用できます。    
    
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB プロバイダーでは、マルチサブネット フェールオーバー クラスタリングの新しい接続文字列キーワード (MultiSubnetFailover=True) はサポートされません。 詳細については、[SQL Server のリリース ノート](https://go.microsoft.com/fwlink/?LinkId=247824)をご覧ください。    
> 
> [!NOTE]
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007 である場合、Excel または Access の以前のバージョンとは異なるデータ プロバイダーが必要になります。 詳細については、「 [Excel ブックに接続する](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) 」および「 [Access データベースに接続する](../../integration-services/connection-manager/connect-to-an-access-database.md)」を参照してください。    
    
いくつかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] タスクとデータ フロー コンポーネントでは、OLE DB 接続マネージャーを使用します。 たとえば、OLE DB の接続元と OLE DB の接続先では、この接続マネージャーを使用してデータの抽出と読み込みが行われます。 SQL 実行タスクでは、この接続マネージャーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続し、クエリを実行できます。    
    
また、OLE DB 接続マネージャーを使用して、C++ などの言語を使用するアンマネージ コードで記述されたカスタム タスク内で、OLE DB データ ソースにアクセスすることもできます。    
    
OLE DB 接続マネージャーをパッケージに追加すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、実行時に OLE DB 接続を解決する接続マネージャーが作成され、接続マネージャーのプロパティが設定されて、接続マネージャーがパッケージの **Connections** コレクションに追加されます。    
    
接続マネージャーの `ConnectionManagerType` プロパティは、`OLEDB` に設定されます。    
    
OLE DB 接続マネージャーは、次のようにして構成します。    
    
-   選択したプロバイダーの要件を満たすように構成された、特定の接続文字列を指定します。    
    
-   プロパイダによっては、接続先のデータ ソースの名前を指定します。    
    
-   選択したプロバイダーに適したセキュリティ資格情報を指定します。    
    
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。    
    
## <a name="log-calls-and-troubleshoot-connections"></a>呼び出しのログ記録と接続のトラブルシューティング    
 OLE DB 接続マネージャーによる外部データ プロバイダーの呼び出しをログに記録できます。 その後、OLE DB 接続マネージャーによる外部データ ソースへの接続に関するトラブルシューティングを行うことができます。 OLE DB 接続マネージャーによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択する必要があります。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。    
    
## <a name="configure-the-ole-db-connection-manager"></a>OLE DB 接続マネージャーを構成する    
 プロパティの設定は、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーまたはプログラムで行います。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [OLE DB 接続マネージャーの構成](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)」を参照してください。 プログラムによって接続マネージャーを構成する方法の詳細については、開発者ガイドの **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** クラスのドキュメントを参照してください。    
    
### <a name="configure-ole-db-connection-manager"></a>OLE DB 接続マネージャーを構成する

接続をデータ ソースに追加するには、 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用します。 この接続は、新しいものでも、既存の接続のコピーでもかまいません。  
  
> [!NOTE]  
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 である場合、Excel の以前のバージョンとは異なる接続マネージャーが必要になります。 詳細については、「 [Excel ブックに接続する](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)」を参照してください。  
>   
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007 である場合、Access の以前のバージョンとは異なる OLE DB プロバイダーが必要になります。 詳細については、「 [Access データベースに接続する](../../integration-services/connection-manager/connect-to-an-access-database.md)」を参照してください。  
  
 OLE DB 接続マネージャーの詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
#### <a name="options"></a>オプション  
 **[データ接続]**  
 一覧から既存の OLE DB データ接続を選択します。  
  
 **[データ接続のプロパティ]**  
 選択した OLE DB データ接続のプロパティとその値を表示します。  
  
 **[新規作成]**  
 **[接続マネージャー]** ダイアログ ボックスを使用して、OLE DB データ接続を作成します。  
  
 **削除**  
 データ接続を選択し、 **[削除]** を選択して削除します。  
  
#### <a name="managed-identities-for-azure-resources-authentication"></a>Azure リソース認証用のマネージド ID
[Azure Data Factory 内の Azure-SSIS 統合ランタイム](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上で SSIS パッケージを実行しているときは、お使いのデータ ファクトリに関連付けられている[マネージド ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) を Azure SQL Database (またはマネージド インスタンス) 認証に使用します。 この ID を使用して指定したファクトリからデータベースにアクセスし、データベースに、またはデータベースからデータをコピーできます。

> [!NOTE]
>  Azure Active Directory (Azure AD) 認証 (マネージド ID 認証を含む) を使用して Azure SQL Database (またはマネージド インスタンス) に接続するときに、パッケージの実行エラーや予期しない動作の変更に関連する問題が発生することがあります。 詳しくは、「[Azure AD の機能と制限事項](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations)」をご覧ください。

Azure SQL Database にマネージド ID 認証を使用するには、以下の手順でデータベースを構成します。

1. まだ行っていない場合は、Azure portal で Azure SQL サーバーの [Azure Active Directory 管理者をプロビジョニング](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)します。 Azure AD 管理者は、Azure AD ユーザーでも Azure AD グループでもかまいません。 マネージド ID を持つグループに管理者ロールを付与する場合は、ステップ 2 と 3 をスキップします。 管理者は、データベースへのフル アクセスを持ちます。

1. データ ファクトリのマネージド ID 用に[包含データベース ユーザーを作成](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)します。 少なくとも ALTER ANY USER アクセス許可を持つ Azure AD ID で、SSMS のようなツールを使用してデータをコピーするデータベースに接続します。 次の T-SQL を実行します。 
    
    ```sql
    CREATE USER [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. SQL ユーザーや他のユーザーに対する通常の方法と同様に、データ ファクトリのマネージド ID に必要なアクセス許可を付与します。 適切なロールについては、「[データベース レベルのロール](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles)」をご覧ください。 次のコードを実行します。 詳細については、[こちらのドキュメント](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)を参照してください。

    ```sql
    EXEC sp_addrolemember [role name], [your data factory name];
    ```

Azure SQL Database マネージド インスタンスにマネージド ID 認証を使用するには、以下の手順でデータベースを構成します。
    
1. まだ行っていない場合は、Azure portal でお使いのマネージド インスタンスの [Azure Active Directory 管理者をプロビジョニング](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)します。 Azure AD 管理者は、Azure AD ユーザーでも Azure AD グループでもかまいません。 マネージド ID を持つグループに管理者ロールを付与する場合は、ステップ 2 から 4 をスキップします。 管理者は、データベースへのフル アクセスを持ちます。

1. データ ファクトリのマネージド ID 用に[ログインを作成](https://docs.microsoft.com/sql/t-sql/statements/create-login-transact-sql?view=azuresqldb-mi-current)します。 SQL Server Management Studio (SSMS) で、**sysadmin** である SQL Server アカウントを使用して Managed Instance に接続します。 **マスター** データベースで、次の T-SQL を実行します。

    ```sql
    CREATE LOGIN [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. データ ファクトリのマネージド ID 用に[包含データベース ユーザーを作成](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)します。 データのコピー元またはコピー先のデータベースに接続し、次の T-SQL を実行します。 
  
    ```sql
    CREATE USER [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. SQL ユーザーや他のユーザーに対する通常の方法と同様に、データ ファクトリのマネージド ID に必要なアクセス許可を付与します。 次のコードを実行します。 詳細については、[こちらのドキュメント](https://docs.microsoft.com/sql/t-sql/statements/alter-role-transact-sql?view=azuresqldb-mi-current)を参照してください。

    ```sql
    ALTER ROLE [role name e.g., db_owner] ADD MEMBER [your data factory name];
    ```

次に、OLE DB 接続マネージャーに対して OLE DB プロバイダーを構成します。 これを行うには次のオプションがあります。
    
- **設計時に構成します。** SSIS デザイナーで、OLE DB 接続マネージャーをダブルクリックして、 **[接続マネージャー]** ウィンドウを開きます。 **[プロバイダー]** ドロップダウン リストで、[ **[Microsoft OLE DB Driver for SQL Server]** ](https://go.microsoft.com/fwlink/?linkid=871294) を選択します。
    > [!NOTE]
    >  ドロップダウン リストの他のプロバイダーでは、マネージド ID 認証がサポートされていない場合があります。
    
- **実行時に構成します。** パッケージを [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) または [Azure Data Factory の SSIS パッケージの実行アクティビティ](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)で実行するときは、OLE DB 接続マネージャーに対する接続マネージャーのプロパティ **ConnectionString** を探します。 接続プロパティ `Provider` を `MSOLEDBSQL` に更新します (つまり、Microsoft OLE DB Driver for SQL Server)。
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

最後に、OLE DB 接続マネージャーに対するマネージド ID 認証を構成します。 これを行うには次のオプションがあります。
    
- **設計時に構成します。** SSIS デザイナーで、OLE DB 接続マネージャーを右クリックして、 **[プロパティ]** を選択します。 プロパティ `ConnectUsingManagedIdentity` を `True` に更新します。
    > [!NOTE]
    >  現在、SSIS パッケージを SSIS デザイナーまたは [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server で実行しているときは、接続マネージャーのプロパティ `ConnectUsingManagedIdentity` は有効になりません (マネージド ID 認証が機能しないことを示します)。

- **実行時に構成します。** パッケージを SSMS または **SQL パッケージの実行**アクティビティで実行するときは、OLE DB 接続マネージャーを見つけて、そのプロパティ `ConnectUsingManagedIdentity` を `True` に更新します。
    > [!NOTE]
    >  Azure-SSIS 統合ランタイムでは、データベース接続を確立するためにマネージド ID 認証を使用すると、OLE DB 接続マネージャーで事前構成済みの他のすべての認証方法 (統合セキュリティ、パスワードなど) はオーバーライドされます。

> [!NOTE]
>  既存のパッケージでマネージド ID 認証を構成するための推奨される方法は、[最新の SSIS デザイナー](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)を使用して SSIS プロジェクトを少なくとも 1 回リビルドすることです。 SSIS プロジェクトのすべての OLE DB 接続マネージャーに新しい接続マネージャー プロパティ `ConnectUsingManagedIdentity` が自動的に追加されるように、SSIS プロジェクトを Azure-SSIS 統合ランタイムに再配置します。 または、実行時にプロパティ パス **\Package.Connections[<接続マネージャーの名前>].Properties[ConnectUsingManagedIdentity]** を指定して、プロパティのオーバーライドを直接使用します。

## <a name="see-also"></a>参照    
 [OLE DB ソース](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)     
 [SQL 実行タスク](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
