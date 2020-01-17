---
title: ADO.NET 接続マネージャー | Microsoft Docs
description: ADO.NET 接続マネージャーを使用すると、パッケージは .NET プロバイダーを使用してデータ ソースにアクセスできます。
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3cf4e302df6e28d898a2790d928cf40085f7915
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687273"
---
# <a name="adonet-connection-manager"></a>ADO.NET 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用すると、パッケージは .NET プロバイダーを使用してデータ ソースにアクセスできます。 通常、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのデータ ソースにアクセスするには、この接続マネージャーを使用します。 また、C# などの言語を使用してマネージド コードに記述されたカスタム タスク内で、OLE DB や XML を介して公開されているデータ ソースにもアクセスできます。  
  
[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーをパッケージに追加すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって、実行時に [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続として解決される接続マネージャーが作成されます。 接続マネージャーのプロパティが設定され、接続マネージャーがパッケージの **Connections** コレクションに追加されます。  
  
接続マネージャーの `ConnectionManagerType` プロパティは、`ADO.NET` に設定されます。 `ConnectionManagerType` の値には、接続マネージャーが使用する .NET プロバイダーの名前を含めることができます。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 接続マネージャーのトラブルシューティング  
[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーによる外部データ プロバイダーの呼び出しをログに記録できます。 その後、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーによる外部データ ソースへの接続に関するトラブルシューティングを行うことができます。 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択する必要があります。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーに読み込まれるとき、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定の日付データ型のデータでは、次の表に示す結果が生成されます。  
  
|SQL Server のデータ型|結果|  
|--------------------------|------------|  
|**time**、 **datetimeoffset**|パッケージがパラメーター化 SQL コマンドを使用していない場合、パッケージは失敗します。 パラメーター化 SQL コマンドを使用するには、パッケージで SQL 実行タスクを使用します。 詳細については、「 [SQL 実行タスク](../../integration-services/control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)」を参照してください。|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーは、ミリ秒の値を切り捨てます。|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の詳細とそれを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型にマッピングする方法については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」と「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="adonet-connection-manager-configuration"></a>ADO.NET 接続マネージャーの構成  
  
プロパティの設定は、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーまたはプログラムで行います。  
  
-   選択した .NET プロバイダーの要件を満たすように構成された、特定の接続文字列を指定します。  
  
-   プロパイダによっては、接続先のデータ ソースの名前を指定します。  
  
-   選択したプロバイダーに適したセキュリティ資格情報を指定します。  
  
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。  
  
[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーの多くの構成オプションは、接続マネージャーが使用する .NET プロバイダーによって異なります。  
  
[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「[ADO.NET 接続マネージャーの構成](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
### <a name="configure-adonet-connection-manager"></a>ADO.NET 接続マネージャーを構成する
.NET Framework データ プロバイダーを使用してアクセスできるデータ ソースへの接続を追加するには、 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを使用します。 たとえば、そのようなプロバイダーの 1 つは SqlClient プロバイダーです。 接続マネージャーでは、既存の接続を使用することも、新しく接続を作成することもできます。  
  
 ADO.NET 接続マネージャーの詳細については、「 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)」を参照してください。  
  
#### <a name="options"></a>オプション  
**[データ接続]**  
一覧から既存の ADO.NET データ接続を選択します。  
  
**[データ接続のプロパティ]**  
選択した ADO.NET データ接続のプロパティとその値を表示します。  
  
**[新規作成]**  
**[接続マネージャー]** ダイアログ ボックスを使用して、ADO.NET データ接続を作成します。  
  
**削除**  
接続を選択し、 **[削除]** を選択して削除します。  
  
#### <a name="managed-identities-for-azure-resources-authentication"></a>Azure リソース認証用のマネージド ID
[Azure Data Factory 内の Azure-SSIS 統合ランタイム](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上で SSIS パッケージを実行しているときは、お使いのデータ ファクトリに関連付けられている[マネージド ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) を Azure SQL Database (またはマネージド インスタンス) 認証に使用できます。 この ID を使用して指定したファクトリからデータベースにアクセスし、データベースに、またはデータベースからデータをコピーできます。

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

最後に、ADO.NET 接続マネージャーに対するマネージド ID 認証を構成します。 これを行うには次のオプションがあります。
    
- **設計時に構成します。** SSIS デザイナーで、ADO.NET 接続マネージャーを右クリックして、 **[プロパティ]** を選択します。 プロパティ `ConnectUsingManagedIdentity` を `True` に更新します。
    > [!NOTE]
    >  現在、SSIS パッケージを SSIS デザイナーまたは [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server で実行しているときは、接続マネージャーのプロパティ `ConnectUsingManagedIdentity` は有効になりません (マネージド ID 認証が機能しないことを示します)。
    
- **実行時に構成します。** パッケージを [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) または [Azure Data Factory の SSIS パッケージの実行アクティビティ](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)で実行するときは、ADO.NET 接続マネージャーを探します。 そのプロパティ `ConnectUsingManagedIdentity` を `True` に更新します。
    > [!NOTE]
    >  Azure-SSIS 統合ランタイムでは、データベース接続を確立するためにマネージド ID 認証を使用すると、ADO.NET 接続マネージャーで事前構成済みの他のすべての認証方法 (統合認証、パスワードなど) はオーバーライドされます。

> [!NOTE]
>  既存のパッケージでマネージド ID 認証を構成するための推奨される方法は、[最新の SSIS デザイナー](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)を使用して SSIS プロジェクトを少なくとも 1 回リビルドすることです。 SSIS プロジェクトのすべての ADO.NET 接続マネージャーに新しい接続マネージャー プロパティ `ConnectUsingManagedIdentity` が自動的に追加されるように、SSIS プロジェクトを Azure-SSIS 統合ランタイムに再配置します。 または、実行時にプロパティ パス **\Package.Connections[<接続マネージャーの名前>].Properties[ConnectUsingManagedIdentity]** を指定して、プロパティのオーバーライドを直接使用します。

## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
