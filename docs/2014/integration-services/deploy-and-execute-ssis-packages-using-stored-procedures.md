---
title: ストアドプロシージャを使用した SSIS パッケージの配置と実行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8cc6c9a2961696512c69f9c3e9de6d229eabb509
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251315"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>ストアド プロシージャを使用した SSIS パッケージの配置と実行
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを、プロジェクト配置モデルを使用するように構成すると、 [!INCLUDE[ssIS](../includes/ssis-md.md)] カタログのストアド プロシージャを使用して、プロジェクトの配置とパッケージの実行を行うことができます。 プロジェクト配置モデルの詳細については、「 [プロジェクトとパッケージの展開](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 また、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] または [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して、プロジェクトの配置とパッケージの実行を行うこともできます。 詳細については、「 **関連項目** 」セクションのトピックを参照してください。  
  
> [!TIP]
>  次の手順を実行することにより、catalog.deploy_project を除き、次の手順に示されるストアド プロシージャの Transact-SQL ステートメントを簡単に生成できます。  
> 
>  1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]で、オブジェクト エクスプローラーの **[Integration Services カタログ]** ノードを展開し、実行するパッケージに移動します。  
> 2.  パッケージを右クリックし、 **[実行]** をクリックします。  
> 3.  必要に応じて、パラメーター値、接続マネージャー プロパティ、 **[詳細設定]** タブのオプション (ログ記録レベルなど) を設定します。  
> 
>      詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)」を参照してください。  
> 4.  **[OK]** をクリックしてパッケージを実行する前に、 **[スクリプト]** をクリックします。 Transact-SQL が [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウに表示されます。  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>ストアド プロシージャを使用してパッケージの配置と実行を行うには  
  
1.  [catalog.deploy_project (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) を呼び出して、パッケージを含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置します。  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクト配置ファイルのバイナリコンテンツを取得するには、 *\@project_stream*パラメーターに対して、OPENROWSET 関数と一括行セットプロバイダーで SELECT ステートメントを使用します。 BULK 行セット プロバイダーを使用すると、ファイルからデータを読み取ることができます。 BULK 行セット プロバイダーの SINGLE_BLOB 引数は、データ ファイルの内容を、varbinary(max) 型の単一行、単一列の行セットとして返します。 詳細については、「[OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
     次の例では、SSISPackages_ProjectDeployment プロジェクトを、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーの SSIS パッケージ フォルダーに配置します。 バイナリデータは、プロジェクトファイル (SSISPackage_ProjectDeployment ispac) から読み取られ、varbinary (max) 型の *\@ProjectBinary*パラメーターに格納されます。 *\@ProjectBinary* パラメーター値は、 *\@project_stream* パラメーターに割り当てられます。  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  [catalog.create_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) を呼び出してパッケージ実行のインスタンスを作成し、必要に応じて、[catalog.set_execution_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) を呼び出してランタイム パラメーター値を設定します。  
  
     次の例では、catalog.create_execution は、SSISPackage_ProjectDeployment プロジェクトに含まれる package.dtsx の実行のインスタンスを作成します。 このプロジェクトは SSIS パッケージ フォルダーに配置されます。 ストアド プロシージャから返される execution_id は、catalog.set_execution_parameter_value の呼び出しに使用されます。 この 2 番目のストアド プロシージャは、LOGGING_LEVEL パラメーターを 3 (詳細ログ) に、Parameter1 という名前のパッケージ パラメーターを 1 に設定します。  
  
     LOGGING_LEVEL などのパラメーターの場合、object_type 値は 50 です。 パッケージ パラメーターの場合、object_type 値は 30 になります。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  [catalog.start_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) を呼び出してパッケージを実行します。  
  
     次の例では、catalog.start_execution の呼び出しを Transact-SQL に追加して、パッケージの実行を開始します。 catalog.create_execution ストアド プロシージャによって返される execution_id が使用されます。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>ストアド プロシージャを使用してサーバー間でプロジェクトを配置するには  
 [catalog.get_project (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) と [catalog.deploy_project (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) ストアド プロシージャを使用して、サーバー間でプロジェクトを配置できます。  
  
 ストアド プロシージャを実行する前に次の操作を行う必要があります。  
  
-   リンク サーバー オブジェクトを作成します。 詳細については、「[リンク サーバーの作成 (SQL Server データベース エンジン)](../database-engine/sql-server-database-engine-overview.md)」を参照してください。  
  
     **[リンク サーバーのプロパティ]** ダイアログ ボックスの **[サーバー オプション]** ページで、 **[RPC]** および **[RPC 出力]** を **[True]** に設定します。 そして、 **[分散トランザクションのプロモーションを RPC に対して有効化]** を **[False]** に設定します。  
  
-   オブジェクト エクスプローラーの **[リンク サーバー]** にある **[プロバイダー]** ノードを展開し、プロバイダーを右クリックして **[プロパティ]** をクリックすることで、リンク サーバーに対して選択したプロバイダーの動的パラメーターを有効にします。 **[動的パラメーター]** の横にある **[有効化]** を選択します。  
  
-   分散トランザクション コーディネーター (DTC) が両方のサーバーで起動していることを確認します。  
  
 プロジェクトのバイナリを返す catalog.get_project を呼び出したら、catalog.deploy_project を呼び出します。 catalog.get_project によって返される値は、varbinary(max) 型のテーブル変数に挿入されます。 リンク サーバーは varbinary(max) 型の結果を返すことができません。  
  
 次の例では、catalog.get_project は、リンク サーバーで SSISPackages プロジェクトのバイナリを返します。 catalog.deploy_project は、ローカル サーバーの DestFolder という名前のフォルダーにプロジェクトを配置します。  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [SQL Server Data Tools でのパッケージの実行](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [SQL Server Management Studio を使用した SSIS サーバーでのパッケージの実行](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
