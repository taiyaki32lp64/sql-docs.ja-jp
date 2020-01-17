---
title: Integration Services (SSIS) プロジェクトとパッケージの配置 | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.bids.converttolegacydeployment.f1
- sql13.ssis.deploymentwizard.f1
- sql13.ssis.ssms.isenvprop.permissions.f1
- sql13.ssis.ssms.isenvprop.general.f1
- sql13.ssis.ssms.iscreateenv.f1
- sql13.ssis.ssms.isenvprop.variables.f1
- sql13.ssis.migrationwizard.f1
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0c755208a5443e4606bdb41a0cbdfdf26a1fa1c
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680963"
---
# <a name="deploy-integration-services-ssis-projects-and-packages"></a>Integration Services (SSIS) プロジェクトとパッケージの配置

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、プロジェクト配置モデルと従来のパッケージ配置モデルの 2 つの配置モデルがサポートされています。 プロジェクト配置モデルを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置できます。  
  
従来のパッケージ配置モデルの詳細については、「[レガシー パッケージの配置 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)」を参照してください。  
  
> [!NOTE]  
>  プロジェクト配置モデルは、 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]で導入されました。 このデプロイ モデルを使用した場合、プロジェクト全体をデプロイすることなく 1 つまたは複数のパッケージをデプロイすることができませんでした。 [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] で導入された増分パッケージ配置機能によって、プロジェクト全体を配置することなく、プロジェクトに 1 つ以上のパッケージを配置できます。

> [!NOTE]
> この記事では、SSIS パッケージをデプロイする方法 (全般) と、オンプレミスでパッケージをデプロイする方法について説明します。 次のプラットフォームで SSIS パッケージをデプロイすることもできます。
> - **Microsoft Azure クラウド**。 詳細については、「[Lift and shift SQL Server Integration Services workloads to the cloud](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」 (SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする) を参照してください。
> - **Linux**。 詳しくは、「[SSIS で Linux 上のデータの抽出、変換、読み込みを行う](../../linux/sql-server-linux-migrate-ssis.md)」 をご覧ください。

## <a name="compare-project-deployment-model-and-legacy-package-deployment-model"></a>プロジェクト配置モデルと従来のパッケージ配置モデルの比較

 プロジェクトに対して選択する配置モデルの種類によって、そのプロジェクトに使用できる開発オプションと管理オプションが決まります。 次の表に、プロジェクト配置モデルを使用した場合とパッケージ配置モデルを使用した場合の相違点と共通点を示します。  
  
|プロジェクト配置モデルを使用した場合|従来のパッケージ配置モデルを使用した場合|  
|---------------------------------------------|----------------------------------------------------|  
|配置の単位はプロジェクトです。|パッケージは配置の 1 単位です。|  
|パラメーターを使用して、値をパッケージ プロパティに割り当てます。|構成を使用して、値をパッケージ プロパティに割り当てます。|  
|プロジェクト (パッケージとパラメーターを含む) はプロジェクト配置ファイル (.ispac 拡張子) にビルドされます。|パッケージ (.dtsx 拡張子) と構成 (.dtsConfig 拡張子) は、個別にファイル システムに保存されます。|  
|パッケージとパラメーターを含むプロジェクトは、SQL Server のインスタンス上の SSISDB カタログに配置されます。|パッケージと構成は、別のコンピューター上のファイル システムにコピーされます。 パッケージは、SQL Server のインスタンス上の MSDB データベースに保存することもできます。|  
|データベース エンジンでは CLR 統合が必要です。|データベース エンジンでは CLR 統合は不要です。|  
|環境固有のパラメーター値は、環境変数に格納されます。|環境固有の構成値は、構成ファイルに格納されます。|  
|カタログ内のプロジェクトとパッケージは、実行前にサーバー上で検証できます。 SQL Server Management Studio、ストアド プロシージャ、またはマネージド コードを使用して検証を実行できます。|パッケージは実行の直前に検証されます。 dtExec またはマネージド コードを使用してパッケージを検証することもできます。|  
|パッケージは、データベース エンジンで実行を開始することで実行されます。 プロジェクト識別子、明示的なパラメーター値 (オプション)、および環境参照 (オプション) は、開始前に実行に割り当てられます。<br /><br /> **dtExec**を使用してパッケージを実行することもできます。|パッケージは、 **dtExec** および **DTExecUI** 実行ユーティリティを使用して実行されます。 適切な構成が、コマンド プロンプトの引数で指定されます (オプション)。|  
|実行時に、パッケージによって生成されたイベントが自動的にキャプチャされ、カタログに保存されます。 Transact-SQL ビューを使用して、これらのイベントに対してクエリを実行できます。|実行時に、パッケージによって生成されたイベントは自動的にキャプチャされません。 イベントをキャプチャするには、パッケージにログ プロバイダーを追加する必要があります。|  
|パッケージは、個別の Windows プロセスで実行されます。|パッケージは、個別の Windows プロセスで実行されます。|  
|SQL Server エージェントを使用してパッケージ実行がスケジュールされます。|SQL Server エージェントを使用してパッケージ実行がスケジュールされます。|  


## <a name="features-of-project-deployment-model"></a>プロジェクト配置モデルの機能  
 次の表に、プロジェクト配置モデル専用に開発されたプロジェクトで使用できる機能を示します。  
  
|機能|[説明]|  
|-------------|-----------------|  
|パラメーター|パラメーターは、パッケージで使用されるデータを指定します。 パラメーターは、パッケージ パラメーターとプロジェクト パラメーターを使用して、パッケージ レベルとプロジェクト レベルそれぞれにスコープを設定できます。 パラメーターは、式またはタスクで使用できます。 プロジェクトをカタログに配置すると、パラメーターごとにリテラル値を割り当てることも、設計時に割り当てられた既定値を使用することもできます。 リテラル値の代わりに、環境変数を参照することもできます。 環境変数値は、パッケージ実行時に解決されます。|  
|環境|環境とは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトが参照できる変数のコンテナーです。 各プロジェクトには複数の環境参照を含めることができますが、1 回のパッケージ実行で参照できるのは、1 つの環境の変数のみです。 環境を使用すると、パッケージに割り当てる値をまとめることができます。 たとえば、"Dev"、"test"、"Production" という名前の環境を使用できます。|  
|環境変数|環境変数は、パッケージの実行時にパラメーターに割り当てることができるリテラル値を定義します。 環境変数を使用するには、(パラメーターを持つ環境に対応するプロジェクト内に) 環境参照を作成し、環境変数の名前にパラメーター値を割り当て、個々の実行を構成するときに対応する環境参照を指定します。|  
|SSISDB カタログ|すべての [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトは、SQL Server のインスタンス上で、SSISDB カタログと呼ばれるデータベースに格納され、管理されます。 カタログでは、フォルダーを使用してプロジェクトや環境を整理することができます。 SQL Server の各インスタンスに 1 つのカタログを含めることができます。 各カタログには 0 個以上のフォルダーを含めることができます。 各フォルダーには、0 個以上のプロジェクトと 0 個以上の環境を含めることができます。 カタログ内のフォルダーは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトに対する権限の境界として使用することもできます。|  
|カタログのストアド プロシージャとビュー|カタログ内の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトは、多数のストアド プロシージャとビューを使用して管理できます。 たとえば、パラメーターおよび環境変数の値を指定し、実行を作成および開始して、カタログ操作を監視できます。 実行が開始される前にパッケージで使用される値を確認することもできます。|  
  
## <a name="project-deployment"></a>プロジェクト配置  
 プロジェクト配置モデルの中心にあるのは、プロジェクト配置ファイル (.ispac 拡張子) です。 プロジェクト配置ファイルは、プロジェクト内のパッケージおよびパラメーターに関する重要な情報のみを含む、自己完結型の配置単位です。 プロジェクト配置ファイルは、Integration Services プロジェクト ファイル (.dtproj 拡張子) に含まれるすべての情報を取得するわけではありません。 たとえば、メモの作成に使用する追加のテキスト ファイルは、プロジェクト配置ファイルには保存されないため、カタログには配置されません。  

## <a name="permissions-required-to-deploy-ssis-projects-and-packages"></a>SSIS プロジェクトとパッケージを展開するのに必要なアクセス許可

SSIS サービス アカウントを既定値から変更した場合は、パッケージを正常に展開するために、既定以外のサービス アカウントに追加のアクセス許可を付与することが必要な場合があります。 既定以外のサービス アカウントに必要なアクセス許可が割り当てられていない場合、次のエラー メッセージが表示される可能性があります。

`A .NET Framework error occurred during execution of user-defined routine or aggregate "deploy_project_internal":
System.ComponentModel.Win32Exception: A required privilege is not held by the client.`

このエラーは、通常、DCOM アクセス許可が不足している場合に発生します。 このエラーを解決するには、次の操作を行います。

1.  **[コンポーネント サービス]** コンソールを開きます (または Dcomcnfg.exe を実行します)。
2.  **[コンポーネント サービス]** コンソールで、 **[コンポーネント サービス]**  >  **[コンピューター]**  >  **[マイ コンピューター]**  >  **[DCOM の構成]** を展開します。
3.  一覧で、使用している SQL Server のバージョンに対応する **Microsoft SQL Server Integration Services xx.0** を探します。 たとえば、SQL Server 2016 がバージョン 13 であるとします。
4.  右クリックし、 **[プロパティ]** を選択します。
5.  **[Microsoft SQL Server Integration Services 13.0 のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックします。
6.  3 つのアクセス許可 ("起動とアクティブ化"、"アクセス"、"構成") のそれぞれに対して、 **[カスタマイズ]** を選択してから、 **[編集]** を選択して **[権限]** ダイアログ ボックスを開きます。
7.  **[権限]** ダイアログ ボックスで、既定以外のサービス アカウントを追加し、必要に応じて **[許可]** を付与します。 通常、アカウントには **[ローカルからの起動]** と **[ローカルからのアクティブ化]** のアクセス許可が割り当てられています。
8.  **[OK]** を 2 回クリックし、 **[コンポーネント サービス]** コンソールを閉じます。

このセクションで示したエラーと SSIS サービス アカウントで求められるアクセス許可の詳細については、次のブログ記事を参照してください。
 
- [System.ComponentModel.Win32Exception: Deploying SSIS プロジェクトの配置中にクライアントが要求された特権を保有していません](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2013/08/20/system-componentmodel-win32exception-a-required-privilege-is-not-held-by-the-client-while-deploying-ssis-project/)

## <a name="deploy-projects-to-integration-services-server"></a>Integration Services サーバーへのプロジェクトの配置
  現在のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーを使用すると、さまざまな環境を利用して、パッケージの管理、パッケージの実行、およびパッケージに合わせたランタイム値の構成を行うことができます。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]と同様に、現在のリリースでも、パッケージを SQL Server のインスタンスに配置し、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを使用してパッケージを実行および管理できます。 パッケージ配置モデルを使用できます。 詳細については、「[レガシー パッケージの配置 (SSIS)](../../integration-services/packages/legacy-package-deployment-ssis.md)」を参照してください。  
  
 プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置するには、次の作業を実行します。  
  
1.  SSISDB カタログをまだ作成していない場合は、作成します。 詳細については、「[SSIS カタログ](../../integration-services/catalog/ssis-catalog.md)」を参照してください。  
  
2.  **Integration Services プロジェクト変換ウィザード** を実行して、プロジェクトをプロジェクト配置モデルに変換します。 詳細については、次の指示を参照してください。[プロジェクトをプロジェクトの配置モデルに変換するには](#convert)  
  
    -   [!INCLUDE[ssISversion12](../../includes/ssisversion12-md.md)] 以降でプロジェクトを作成した場合、既定では、プロジェクトでプロジェクト配置モデルが使用されます。  
  
    -   以前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]でプロジェクトを作成した場合、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]でプロジェクト ファイルを開いた後に、プロジェクトをプロジェクト配置モデルに変換します。  
  
        > [!NOTE]  
        >  プロジェクトに含まれている 1 つ以上のデータ ソースは、プロジェクトの変換が完了すると削除されます。 プロジェクト内のパッケージで共有できるデータ ソースへの接続を作成するには、プロジェクト レベルで接続マネージャーを追加します。 詳細については、「 [パッケージでの接続マネージャーの追加、削除、または共有](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)」 を参照してください。  
  
         **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のいずれから実行するかによって、ウィザードが実行する変換タスクは異なります。  
  
        -   ウィザードを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]から実行した場合、プロジェクトに含まれるパッケージは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005、2008、または 2008 R2 から現在のバージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]で使用されている形式に変換されます。 元のプロジェクト (.dtproj) ファイルおよびパッケージ (.dtsx) ファイルはアップグレードされます。  
  
        -   ウィザードを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から実行した場合、プロジェクトに含まれるパッケージおよび構成からプロジェクト配置ファイル (.ispac) が生成されます。 元のパッケージ (.dtsx) ファイルはアップグレードされません。  
  
             ウィザードの **[変換先の選択]** ページで、既存のファイルを選択するか、新規ファイルを作成することができます。  
  
             プロジェクトの変換時にパッケージ ファイルをアップグレードするには、 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]から実行します。 プロジェクトの変換とは別にパッケージ ファイルをアップグレードするには、 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から実行してから、 **SSIS パッケージ アップグレード ウィザード**を実行します。 パッケージ ファイルを個別にアップグレードする場合は、必ず変更を保存します。 保存しないと、プロジェクトをプロジェクトの配置モデルに変換するときに、パッケージに対する未保存の変更が変換されません。  
  
     パッケージのアップグレードの詳細については、「 [Integration Services パッケージのアップグレード](../../integration-services/install-windows/upgrade-integration-services-packages.md) 」および「 [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)」を参照してください。  
  
3.  プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置します。 詳細については、後の手順を参照してください。[Integration Services サーバーにプロジェクトを配置するには](#deploy)。  
  
4.  (省略可能) 配置されたプロジェクト用の環境を作成します。 
  
###  <a name="convert"></a> プロジェクトをプロジェクトの配置モデルに変換するには  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]でプロジェクトを開き、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロジェクト配置モデルに変換]** をクリックします。  
  
     \- または -  
  
     オブジェクト エクスプローラーの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、 **[プロジェクト]** ノードを右クリックし、 **[パッケージのインポート]** を選択します。  
  
2.  ウィザードを完了します。
  
###  <a name="deploy"></a> Integration Services サーバーにプロジェクトを配置するには  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]でプロジェクトを開き、 **[プロジェクト]** メニューの **[配置]** を選択して、 **Integration Services 配置ウィザード**を起動します。  
  
     内の複数の  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** ノードの順に展開し、配置するプロジェクトの [プロジェクト] フォルダーを探します。 **[プロジェクト]** フォルダーを右クリックして **[プロジェクトの配置]** をクリックします。  
  
     内の複数の  
  
     コマンド プロンプトで、 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** にある **isdeploymentwizard.exe**を実行します。 64 ビット コンピューターの場合、 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**に 32 ビット バージョンのツールもあります。  
  
2.  **[ソースの選択]** ページで、 **[プロジェクト配置ファイル]** をクリックして、プロジェクトの配置ファイルを選択します。  
  
     内の複数の  
  
     **[Integration Services カタログ]** をクリックし、SSISDB カタログに既に配置されているプロジェクトを選択します。  
  
3.  ウィザードを完了します。 

## <a name="deploy-packages-to-integration-services-server"></a>Integration Services サーバーへのパッケージの配置
  [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] で導入された増分パッケージ配置機能を使用すると、プロジェクト全体を配置することなく、既存または新規のプロジェクトに 1 つ以上のパッケージを配置できます。  
  
###  <a name="DeployWizard"></a> Integration Services 配置ウィザードを使用してパッケージを配置する  
  
1.  コマンド プロンプトで、 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** にある **isdeploymentwizard.exe**を実行します。 64 ビット コンピューターの場合、 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**に 32 ビット バージョンのツールもあります。  
  
2.  **[ソースの選択]** ページで、 **[パッケージ配置モデル]** に切り替えます。 次に、配置対象のパッケージが含まれるフォルダーを選択し、パッケージを構成します。  
  
3.  ウィザードを完了します。 [Package Deployment Model](#PackageModel)で説明されている残りの手順を実行します。  
  
###  <a name="SSMS"></a> SQL Server Management Studio を使用してパッケージを配置する  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、 **[Integration Services カタログ]**  >  **[SSISDB]** ノードの順に展開します。  
  
2.  **[プロジェクト]** フォルダーを右クリックして、 **[プロジェクトの配置]** をクリックします。  
  
3.  **[説明]** ページが表示される場合は、 **[次へ]** をクリックして続行します。  
  
4.  **[ソースの選択]** ページで、 **[パッケージ配置モデル]** に切り替えます。 次に、配置対象のパッケージが含まれるフォルダーを選択し、パッケージを構成します。  
  
5.  ウィザードを完了します。 [Package Deployment Model](#PackageModel)で説明されている残りの手順を実行します。  
  
###  <a name="SSDT"></a> SQL Server Data Tools (Visual Studio) を使用してパッケージを配置する  
  
1.  Visual Studio で Integration Services プロジェクトを開き、配置する 1 つ以上のパッケージを選択します。  
  
2.  右クリックして、 **[パッケージの配置]** をクリックします。 選択したパッケージ (配置対象のパッケージとして構成済みのもの) が配置ウィザードによって開かれます。  
  
3.  ウィザードを完了します。 [Package Deployment Model](#PackageModel)で説明されている残りの手順を実行します。  
  
###  <a name="StoredProcedure"></a> deploy_packages ストアド プロシージャを使用してパッケージを配置する  
 **[catalog].[deploy_packages]** ストアド プロシージャを使用して、1 つ以上の SSIS パッケージを SSIS カタログに配置できます。 次のコード例では、このストアド プロシージャを使用して SSIS サーバーにパッケージを配置する方法を示します。 詳細については、「 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)」を参照してください。  
  
```cs
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
###  <a name="MOMApi"></a> 管理オブジェクト モデル API を使用してパッケージを配置する  
 次のコード例では、管理オブジェクト モデル API を使用してパッケージをサーバーに配置する方法を示します。  
  
```cs 
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```

## <a name="convert-to-package-deployment-model-dialog-box"></a>[パッケージ配置モデルに変換] ダイアログ ボックス
  **[パッケージ配置モデルに変換]** コマンドを使用すると、パッケージをパッケージ配置モデルに変換できます。この変換は、プロジェクトおよびプロジェクト内の各パッケージとそのモデルとの互換性を確認した後に行います。 パラメーターなど、プロジェクト配置モデルに固有の機能をパッケージで使用する場合は、パッケージを変換できません。  

 パッケージをパッケージ配置モデルに変換するには、2 つの手順を実行する必要があります。  
  
1.  **[プロジェクト]** メニューの **[パッケージ配置モデルに変換]** をクリックすると、プロジェクトおよび各パッケージとこのモデルとの互換性が確認されます。 結果は **[結果]** テーブルに表示されます。  
  
     互換性テストに失敗したプロジェクトまたはパッケージがある場合は、 **[結果]** 列の **[失敗]** をクリックして詳細を確認します。 この情報のコピーをテキスト ファイルに保存するには、 **[レポートの保存]** をクリックします。  
  
2.  プロジェクトとすべてのパッケージの互換性テストが成功した場合は、 **[OK]** をクリックしてパッケージを変換します。  
  
> [!NOTE]
> プロジェクトをプロジェクト配置モデルに変換するには、**Integration Services プロジェクト変換ウィザード**を使用します。 詳細については、「 [Integration Services プロジェクトの変換ウィザード](deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  

## <a name="integration-services-deployment-wizard"></a>Integration Services 配置ウィザード
  **Integration Services 配置ウィザード** は次の 2 つの配置モデルをサポートしています。
   - プロジェクト配置モデル
   - パッケージ配置モデル 
   
 **プロジェクト配置モデル** では、SSIS カタログに単一ユニットとして SQL Server Integration Services (SSIS) プロジェクトを配置することができます。
 
 **パッケージ配置モデル** では、プロジェクト全体を配置する必要はなく、更新したパッケージを SSIS カタログに配置できます。 
 
 > [!NOTE]
 > ウィザードの既定の配置は、プロジェクト配置モデルです。  
  
### <a name="launch-the-wizard"></a>ウィザードを起動する
ウィザードを起動するには、次のいずれかの方法を使用します。

 - Windows Search に「 **SQL Server 配置ウィザード」** 」と入力します。 

 内の複数の

 - SQL Server のインストール フォルダーで、実行可能ファイル **ISDeploymentWizard.exe** を検索します。たとえば、"C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn" で検索します。 
 
 > **注:** **[説明]** ページが表示された場合は、 **[次へ]** をクリックして、 **[ソースの選択]** ページに切り替えます。 
 
 このページの設定は、配置モデルごとに異なります。 このページで選択したモデルに基づいて、「 [Project Deployment Model](#ProjectModel) 」セクションまたは「 [Package Deployment Model](#PackageModel) 」セクションの手順に従ってください。  
  
###  <a name="ProjectModel"></a> Project Deployment Model  
  
#### <a name="select-source"></a>[ソースの選択]

 作成したプロジェクト配置ファイルを配置するには、 **[プロジェクト配置ファイル]** を選択して .ispac ファイルのパスを入力します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログにあるプロジェクトを配置するには、 **[Integration Services カタログ]** を選択し、サーバー名とカタログ内のプロジェクトのパスを入力します。 **[次へ]** をクリックして、 **[配置先の選択]** ページを表示します。  
  
#### <a name="select-destination"></a>[配置先の選択]

 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログでプロジェクトの配置先フォルダーを選択するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを入力するか、 **[参照]** をクリックしてサーバーの一覧から選択します。 SSISDB でプロジェクトのパスを入力するか、 **[参照]** をクリックしてプロジェクトを選択します。 **[次へ]** をクリックして **[レビュー]** ページを表示します。  
  
#### <a name="review-and-deploy"></a>レビュー (と配置)

 このページでは、選択した設定を確認することができます。 選択内容を変更するには、 **[戻る]** をクリックするか、左ペインでいずれかの手順をクリックします。 **[配置]** をクリックして、配置プロセスを開始します。  
  
#### <a name="results"></a>[結果]

 配置プロセスが完了したら、 **[結果]** ページが表示されます。 このページでは、各アクションが成功したか、失敗したかを表示します。 アクションが失敗した場合は、 **[結果]** 列の **[失敗]** をクリックすると、エラーの説明が表示されます。 **[レポートの保存]** をクリックして結果を XML ファイルに保存するか、 **[閉じる]** をクリックしてウィザードを終了します。
  
###  <a name="PackageModel"></a> Package Deployment Model  
  
#### <a name="select-source"></a>[ソースの選択]

 **Integration Services 配置ウィザード** の **[ソースの選択]** ページには、 **配置モデル** に **[パッケージ配置]** オプションを選択した場合、パッケージ配置モデルに固有の設定が表示されます。  
  
 ソース パッケージを選択するには、 **[参照]** ボタンをクリックして、パッケージを含む**フォルダー**を選択するか、 **[パッケージ フォルダーのパス]** テキストボックスにフォルダー パスを入力して、ページの下部にある **[更新]** ボタンをクリックします。 これで、リスト ボックスに指定したフォルダー内のすべてのパッケージが表示されます。 既定では、すべてのパッケージが選択されます。 サーバーに配置するパッケージを選択するには、最初の列の **チェックボックス** をクリックします。  
  
 **[ステータス]** と **[メッセージ]** 列を参照して、パッケージの状態を確認します。 ステータスが **[準備完了]** または **[警告]** に設定されている場合は、配置ウィザードは配置プロセスをブロックしません。 ステータスが **[エラー]** に設定されている場合は、ウィザードは選択したパッケージの配置には進みません。 詳細な警告メッセージまたはエラー メッセージを表示するには、 **[メッセージ]** 列のリンクをクリックします。  
  
 機微なデータまたはパッケージのデータがパスワードで暗号化されている場合は、 **[パスワード]** 列にパスワードを入力して、 **[更新]** ボタンをクリックし、パスワードが承認されたかどうかを検証します。 パスワードが正しい場合は、ステータスが **[準備完了]** に変更され、警告メッセージは表示されません。 同じパスワードを使用する複数のパッケージがある場合は、同じ暗号化パスワードのパッケージを選択して、 **[パスワード]** テキストボックスにパスワードを入力し、 **[適用]** ボタンを選択します。 パスワードは、選択したパッケージに適用されます。  
  
 選択したすべてのパッケージのステータスが **[エラー]** に設定されていない場合は、パッケージ配置プロセスを続行できるように、 **[次へ]** ボタンが有効になります。  
  
#### <a name="select-destination"></a>[配置先の選択]

 パッケージ ソースを選択した後に、 **[次へ]** ボタンをクリックして、 **[配置先の選択]** ページに切り替えます。 パッケージは、SSIS カタログ (SSISDB) のプロジェクトに配置する必要があります。 パッケージを配置する前に、SSIS カタログに配置先のプロジェクトが既に必ず存在しているようにします。 プロジェクトが存在しない場合は、空のプロジェクトを作成します。 **[配置先の選択]** ページで、 **[サーバー名]** テキストボックスにサーバー名を入力するか、 **[参照]** ボタンをクリックしてサーバー インスタンスを選択します。 次に、 **[パス]** テキストボックスの横にある **[参照]** ボタンをクリックして、配置先のプロジェクトを指定します。 プロジェクトが存在しない場合は、 **[新しいプロジェクト]** ボタンをクリックして、配置先のプロジェクトとして空のプロジェクトを作成します。 プロジェクトは、フォルダーの下に作成する必要があります。  
  
#### <a name="review-and-deploy"></a>レビューと配置

 **[配置先の選択]** ページで **[次へ]** をクリックして、 **Integration Services 配置ウィザード** の **[レビュー]** ページに切り替えます。 [レビュー] ページで、配置アクションに関する概要レポートを確認します。 検証した後に、 **[配置]** ボタンをクリックして、配置アクションを実行します。  
  
#### <a name="results"></a>[結果]

 配置が完了したら、 **[結果]** ページが表示されます。 **[結果]** ページで、配置プロセスの各手順の結果を確認します。 **[レポートの保存]** をクリックして配置レポートを保存するか、 **[閉じる]** をクリックしてウィザードを閉じます。  

## <a name="create-and-map-a-server-environment"></a>サーバー環境の作成とマップ

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置したプロジェクトに含まれるパッケージに合わせたランタイム値を指定するためのサーバー環境を作成します。 特定のパッケージ、エントリ ポイント パッケージ、または特定のプロジェクト内のすべてのパッケージに対して、環境変数をパラメーターにマップできるようになります。 エントリ ポイント パッケージは、通常、子パッケージを実行する親パッケージです。  
  
> [!IMPORTANT]  
>  特定の実行で、パッケージは単一のサーバー環境に含まれている値だけで実行できます。  
  
 サーバー環境、環境参照、および環境変数の一覧のビューに対してクエリを実行できます。 環境、環境参照、および環境変数を追加、削除、変更するストアド プロシージャを呼び出すこともできます。 詳細については、「[SSIS Catalog](../../integration-services/catalog/ssis-catalog.md)」の「**サーバー環境、サーバー変数、およびサーバー環境参照**」を参照してください。  
  
### <a name="to-create-and-use-a-server-environment"></a>サーバー環境を作成して使用するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーで、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ **SSISDB** ノードを展開し、環境を作成するプロジェクトの **[環境]** フォルダーを検索します。  
  
2.  **[環境]** フォルダーを右クリックし、 **[環境の作成]** をクリックします。  
  
3.  環境の名前を入力し、必要に応じて説明を追加します。 **[OK]** をクリックします。  
  
4.  新しい環境を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[変数]** ページで、次の手順を実行して変数を追加します。  
  
    1.  変数の **[型]** を選択します。 変数の名前は、変数にマップするプロジェクト パラメーターの名前と一致している必要はありません。  
  
    2.  必要に応じて、変数の **[説明]** を入力します。  
  
    3.  環境変数の **[値]** を入力します。  
  
         環境変数の名前のルールについては、「 **SSIS Catalog** 」の「 [環境変数](../../integration-services/catalog/ssis-catalog.md)」を参照してください。  
  
    4.  **[機微]** チェック ボックスをオンまたはオフにして、変数に機微な値が含まれているかどうかを示します。  
  
         **[機微]** をオンにすると、変数値が **[値]** のフィールドに表示されません。  
  
         機微な値は、SSISDB カタログで暗号化されます。 暗号化の詳細については、「 [SSIS Catalog](../../integration-services/catalog/ssis-catalog.md)」を参照してください。  
  
6.  **[権限]** ページで、次の手順を実行して、選択したユーザーに対して権限とロールを許可または拒否します。  
  
    1.  **[参照]** をクリックし、 **[すべてのプリンシパルを参照]** ダイアログ ボックスで 1 つ以上のユーザーおよびロールを選択します。  
  
    2.  **[ログインまたはロール]** 領域で、権限を許可または拒否するユーザーまたはロールを選択します。  
  
    3.  **[明示]** 領域で、各権限の横にある **[許可]** または **[拒否]** を選択します。  
  
7.  環境のスクリプトを作成するには、 **[スクリプト]** をクリックします。 既定では、新しいクエリ エディター ウィンドウにスクリプトが表示されます。  
  
    > [!TIP]  
    >  スクリプトを作成した後、または変数を追加するなど環境プロパティを変更した後に **[スクリプト]** をクリックしてから、 **[環境のプロパティ]** ダイアログ ボックスで **[OK]** をクリックする必要があります。 このようにしないと、スクリプトは生成されません。  
  
8.  **[OK]** をクリックして、変更を環境プロパティに保存します。  
  
9. オブジェクト エクスプローラーで **[SSISDB]** ノードの下の **[プロジェクト]** フォルダーを展開し、プロジェクトを右クリックして **[構成]** をクリックします。  
  
10. **[参照]** ページで、 **[追加]** をクリックして環境を追加し、 **[OK]** をクリックして参照を環境に保存します。  
  
11. プロジェクトをもう一度右クリックし、 **[構成]** をクリックします。  
  
12. 環境変数を、デザイン時にパッケージに追加したパラメーターにマップするか、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトをプロジェクト配置モデルに変換したときに生成されたパラメーターにマップするには、次の手順を実行します。
  
    1.  **[パラメーター]** ページの **[パラメーター]** タブで、 **[値]** フィールドの横にある参照ボタンをクリックします。  
  
    2.  **[環境変数を使用する]** をクリックし、作成した環境変数を選択します。  
  
13. 環境変数を接続マネージャーのプロパティにマップするには、次の操作を行います。 パラメーターは、SSIS サーバー上で接続マネージャー プロパティ用に自動的に生成されます。  
  
    1.  **[パラメーター]** ページの **[接続マネージャー]** タブで、 **[値]** フィールドの横にある **[参照]** ボタンをクリックします。  
  
    2.  **[環境変数を使用する]** をクリックし、作成した環境変数を選択します。  
  
14. **[OK]** を 2 回クリックして変更を保存します。  

## <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>ストアド プロシージャを使用した SSIS パッケージの配置と実行

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを、プロジェクト配置モデルを使用するように構成すると、[!INCLUDE[ssIS](../../includes/ssis-md.md)] カタログのストアド プロシージャを使用して、プロジェクトの配置とパッケージの実行を行うことができます。 プロジェクト配置モデルの詳細については、「[プロジェクトとパッケージの展開](deploy-integration-services-ssis-projects-and-packages.md#compare-project-deployment-model-and-legacy-package-deployment-model)」を参照してください。  
  
 また、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用して、プロジェクトの配置とパッケージの実行を行うこともできます。 詳細については、「 **関連項目** 」セクションのトピックを参照してください。  
  
> [!TIP]
>  次の手順を実行することにより、catalog.deploy_project を除き、次の手順に示されるストアド プロシージャの Transact-SQL ステートメントを簡単に生成できます。
> 
>  1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、オブジェクト エクスプローラーの **[Integration Services カタログ]** ノードを展開し、実行するパッケージに移動します。  
> 2.  パッケージを右クリックし、 **[実行]** をクリックします。  
> 3.  必要に応じて、パラメーター値、接続マネージャー プロパティ、 **[詳細設定]** タブのオプション (ログ記録レベルなど) を設定します。  
> 
>      詳細については、「[SSIS サーバーでのパッケージ実行のログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)」を参照してください。  
> 4.  **[OK]** をクリックしてパッケージを実行する前に、 **[スクリプト]** をクリックします。 Transact-SQL が [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウに表示されます。  
  
### <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>ストアド プロシージャを使用してパッケージの配置と実行を行うには  
  
1.  [catalog.deploy_project (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) を呼び出して、パッケージを含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置します。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクト配置ファイルのバイナリ コンテンツを取得するには、 _\@project_stream_ パラメーターの場合、SELECT ステートメントと、OPENROWSET 関数および BULK 行セット プロバイダーを使用します。 BULK 行セット プロバイダーを使用すると、ファイルからデータを読み取ることができます。 BULK 行セット プロバイダーの SINGLE_BLOB 引数は、データ ファイルの内容を、varbinary(max) 型の単一行、単一列の行セットとして返します。 詳細については、「[OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)」を参照してください。  
  
     次の例では、SSISPackages_ProjectDeployment プロジェクトを、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーの SSIS パッケージ フォルダーに配置します。 バイナリ データは、プロジェクト ファイル (SSISPackage_ProjectDeployment.ispac) から読み取られ、varbinary(max) 型の _\@ProjectBinary パラメーターに格納されます。 _\@ProjectBinary_ パラメーター値は、 _\@project_stream_ パラメーターに割り当てられます。  
  
    ```sql
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  [catalog.create_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) を呼び出してパッケージ実行のインスタンスを作成し、必要に応じて、[catalog.set_execution_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) を呼び出してランタイム パラメーター値を設定します。  
  
     次の例では、catalog.create_execution は、SSISPackage_ProjectDeployment プロジェクトに含まれる package.dtsx の実行のインスタンスを作成します。 このプロジェクトは SSIS パッケージ フォルダーに配置されます。 ストアド プロシージャから返される execution_id は、catalog.set_execution_parameter_value の呼び出しに使用されます。 この 2 番目のストアド プロシージャは、LOGGING_LEVEL パラメーターを 3 (詳細ログ) に、Parameter1 という名前のパッケージ パラメーターを 1 に設定します。  
  
     LOGGING_LEVEL などのパラメーターの場合、object_type 値は 50 です。 パッケージ パラメーターの場合、object_type 値は 30 になります。  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  [catalog.start_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) を呼び出してパッケージを実行します。  
  
     次の例では、catalog.start_execution の呼び出しを Transact-SQL に追加して、パッケージの実行を開始します。 catalog.create_execution ストアド プロシージャによって返される execution_id が使用されます。  
  
    ```sql
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
  
### <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>ストアド プロシージャを使用してサーバー間でプロジェクトを配置するには

 [catalog.get_project (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md) と [catalog.deploy_project (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) ストアド プロシージャを使用して、サーバー間でプロジェクトを配置できます。  
  
 ストアド プロシージャを実行する前に次の操作を行う必要があります。  
  
-   リンク サーバー オブジェクトを作成します。 詳細については、「[リンク サーバーの作成 (SQL Server データベース エンジン)](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)」を参照してください。  
  
     **[リンク サーバーのプロパティ]** ダイアログ ボックスの **[サーバー オプション]** ページで、 **[RPC]** および **[RPC 出力]** を **[True]** に設定します。 そして、 **[分散トランザクションのプロモーションを RPC に対して有効化]** を **[False]** に設定します。  
  
-   オブジェクト エクスプローラーの **[リンク サーバー]** にある **[プロバイダー]** ノードを展開し、プロバイダーを右クリックして **[プロパティ]** をクリックすることで、リンク サーバーに対して選択したプロバイダーの動的パラメーターを有効にします。 **[動的パラメーター]** の横にある **[有効化]** を選択します。  
  
-   分散トランザクション コーディネーター (DTC) が両方のサーバーで起動していることを確認します。  
  
 プロジェクトのバイナリを返す catalog.get_project を呼び出したら、catalog.deploy_project を呼び出します。 catalog.get_project によって返される値は、varbinary(max) 型のテーブル変数に挿入されます。 リンク サーバーは varbinary(max) 型の結果を返すことができません。  
  
 次の例では、catalog.get_project は、リンク サーバーで SSISPackages プロジェクトのバイナリを返します。 catalog.deploy_project は、ローカル サーバーの DestFolder という名前のフォルダーにプロジェクトを配置します。  
  
```sql
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  

## <a name="integration-services-project-conversion-wizard"></a>Integration Services プロジェクト変換ウィザード
  **Integration Services プロジェクト変換ウィザード** で、プロジェクトをプロジェクト配置モデルに変換します。  
  
> [!NOTE]  
>  プロジェクトに含まれている 1 つ以上のデータ ソースは、プロジェクトの変換が完了すると削除されます。 プロジェクト内のパッケージで共有可能なデータ ソースへの接続を作成するには、プロジェクト レベルで接続マネージャーを追加します。 詳細については、「 [パッケージの接続マネージャーを追加、削除、または共有する](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)」を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [Integration Services プロジェクト変換ウィザードを開く](#open_dialog)  
  
-   [[パッケージの場所の指定] ページのオプションの設定](#locate)  
  
-   [[パッケージの選択] ページのオプションの設定](#selectPackages)  
  
-   [[配置先の選択] ページのオプションの設定](#destination)  
  
-   [[プロジェクト プロパティの指定] ページのオプションの設定](#projectProperties)  
  
-   [[パッケージ実行タスクの更新] ページのオプションの設定](#executePackage)  
  
-   [[構成の選択] ページのオプションの設定](#configurations)  
  
-   [[パラメーターの作成] ページのオプションの設定](#createParameters)  
  
-   [[パラメーターの構成] ページのオプションの設定](#configureParameters)  
  
-   [[確認] ページのオプションの設定](#review)  
  
-   [[変換の実行] のオプションの設定](#conversion)  
  
###  <a name="open_dialog"></a> Integration Services プロジェクト変換ウィザードを開く  
 **Integration Services プロジェクト変換** ウィザードを開くには、次のいずれかの操作を行います。  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]でプロジェクトを開き、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロジェクト配置モデルに変換]** をクリックします。  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーで、 **[Integration Services カタログ]** の **[プロジェクト]** ノードを右クリックし、 **[パッケージのインポート]** をクリックします。  
  
 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のいずれから実行するかによって、ウィザードが実行する変換タスクは異なります。   
  
###  <a name="locate"></a> [パッケージの場所の指定] ページのオプションの設定  
  
> [!NOTE]  
>  **[パッケージの場所の指定]** ページは、ウィザードを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]から実行した場合にのみ使用可能です。  
  
 **[ソース]** ボックスの一覧の **[ファイル システム]** を選択すると、次のオプションがページに表示されます。 パッケージがファイル システムに存在する場合は、このオプションを選択します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
 **[ソース]** ボックスの一覧の **[SSIS パッケージ ストア]** を選択すると、次のオプションがページに表示されます。 パッケージ ストアの詳細については、「[パッケージの管理 &#40;SSIS サービス&#41;](../../integration-services/service/package-management-ssis-service.md)」を参照してください。  
  
 **[サーバー]**  
 サーバー名を入力するか、またはサーバーを選択します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
 **[ソース]** ボックスの一覧の **[Microsoft SQL Server]** を選択すると、次のオプションがページに表示されます。 パッケージが Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に存在する場合は、このオプションを選択します。  
  
 **[サーバー]**  
 サーバー名を入力するか、またはサーバーを選択します。  
  
 **[Windows 認証を使用する]**  
 Microsoft Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。 Windows 認証を使用すると、ユーザー名とパスワードを入力する必要がなくなります。  
  
 **[SQL Server 認証を使用する]**  
 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで接続の認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。  
  
 **User name**  
 SQL Server 認証を使用する場合に、ユーザー名を指定します。  
  
 **パスワード**  
 SQL Server 認証を使用する場合に、パスワードを指定します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
###  <a name="selectPackages"></a> [パッケージの選択] ページのオプションの設定  
 **[パッケージ名]**  
 パッケージ ファイルを一覧表示します。  
  
 **ステータス**  
 パッケージをパッケージ配置モデルに変換する準備ができているかどうかを示します。  
  
 **メッセージ**  
 パッケージに関連付けられているメッセージが表示されます。  
  
 **パスワード**  
 パッケージに関連付けられているパスワードが表示されます。 パスワードのテキストは表示されません。  
  
 **[選択項目に適用]**  
 クリックすると、 **[パスワード]** ボックスのパスワードが選択したパッケージに適用されます。  
  
 **[更新]**  
 パッケージの一覧を更新します。  
  
###  <a name="destination"></a> [配置先の選択] ページのオプションの設定  
 このページで、新規プロジェクト配置ファイル (.ispac) の名前とパスを指定するか、既存のファイルを選択します。  
  
> [!NOTE]  
>  **[配置先の選択]** ページは、ウィザードを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]から実行した場合にのみ使用可能です。  
  
 **[出力パス]**  
 配置ファイルのパスを入力するか、 **[参照]** をクリックしてファイルに移動します。  
  
 **プロジェクト名**  
 プロジェクト名を入力します。  
  
 **保護レベル**  
 保護レベルを選択します。 詳しくは、「 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
 **[プロジェクトの説明]**  
 プロジェクトの説明を入力します (省略可)。  
  
###  <a name="projectProperties"></a> [プロジェクト プロパティの指定] ページのオプションの設定  
  
> [!NOTE]  
>  **[プロジェクト プロパティの指定]** ページは、ウィザードを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]から実行した場合にのみ使用可能です。  
  
 **プロジェクト名**  
 プロジェクト名を一覧表示します。  
  
 **保護レベル**  
 プロジェクトに含まれるパッケージの保護レベルを選択します。 保護レベルの詳細については、「 [パッケージ内の機微なデータへのアクセス制御](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」を参照してください。  
  
 **[プロジェクトの説明]**  
 プロジェクトの説明 (省略可能) を入力します。  
  
###  <a name="executePackage"></a> [パッケージ実行タスクの更新] ページのオプションの設定  
 プロジェクト ベースの参照を使用するには、パッケージに含まれているパッケージ実行タスクを更新します。 詳細については、「 [パッケージ実行タスク エディター](../../integration-services/control-flow/execute-package-task-editor.md)」を参照してください。  
  
 **[親パッケージ]**  
 パッケージ実行タスクを使用して子パッケージを実行するパッケージの名前を一覧表示します。  
  
 **[タスク名]**  
 パッケージ実行タスクの名前を一覧表示します。  
  
 **[元の参照]**  
 子パッケージの現在のパスを一覧表示します。  
  
 **[参照の割り当て]**  
 プロジェクトに格納されている子パッケージを選択します。  
  
###  <a name="configurations"></a> [構成の選択] ページのオプションの設定  
 パラメーターで置き換えるパッケージ構成を選択します。  
  
 **[パッケージ]**  
 パッケージ ファイルを一覧表示します。  
  
 **Type**  
 XML 構成ファイルなど、構成の種類を一覧表示します。  
  
 **[構成文字列]**  
 構成ファイルのパスを一覧表示します。  
  
 **ステータス**  
 構成の状態メッセージが表示されます。 メッセージ テキスト全体を表示するには、メッセージをクリックします。  
  
 **[構成の追加]**  
 他のプロジェクトに含まれているパッケージ構成を、パラメーターで置き換える (使用可能な) 構成の一覧に追加します。 ファイル システムまたは SQL Server に格納された構成を選択できます。  
  
 **[更新]**  
 構成の一覧を更新する場合にクリックします。  
  
 **[変換後にすべてのパッケージから構成を削除する]**  
 このオプションを選択して、プロジェクトからすべての構成を削除することをお勧めします。  
  
 このオプションを選択しない場合は、パラメーターで置き換えるために選択した構成のみが削除されます。  
  
###  <a name="createParameters"></a> [パラメーターの作成] ページのオプションの設定  
 各構成プロパティのパラメーター名とスコープを選択します。  
  
 **[パッケージ]**  
 パッケージ ファイルを一覧表示します。  
  
 **[パラメーター名]**  
 パラメーター名を一覧表示します。  
  
 **スコープ**  
 パラメーターのスコープ (パッケージまたはプロジェクト) を選択します。  
  
###  <a name="configureParameters"></a> [パラメーターの構成] ページのオプションの設定  
 **[名前]**  
 パラメーター名を一覧表示します。  
  
 **スコープ**  
 パラメーターのスコープを一覧表示します。  
  
 **Value**  
 パラメーター値を一覧表示します。  
  
 パラメーター プロパティを構成するには、値フィールドの横にある参照ボタンをクリックします。  
  
 **[パラメーターの詳細の設定]** ダイアログ ボックスで、パラメーター値を編集できます。 パッケージの実行時にパラメーター値を指定する必要があるかどうかを指定することもできます。  
  
 **の** [構成] **ダイアログ ボックスの** [パラメーター] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ページの値を変更するには、パラメーターの横にある参照ボタンをクリックします。 **[パラメーター値の設定]** ダイアログ ボックスが表示されます。  
  
 また、 **[パラメーターの詳細の設定]** ダイアログ ボックスには、パラメーター値のデータ型や元のパラメーターが一覧表示されます。  
  
###  <a name="review"></a> [確認] ページのオプションの設定  
 プロジェクトの変換に関して選択したオプションを確認するには、 **[確認]** ページを使用します。  
  
 **[戻る]**  
 オプションを変更する場合にクリックします。  
  
 **[変換]**  
 プロジェクトをプロジェクト配置モデルに変換する場合にクリックします。  
  
###  <a name="conversion"></a> [変換の実行] のオプションの設定  
 [変換の実行] ページには、プロジェクトの変換の状態が表示されます。  
  
 **操作**  
 特定の変換手順を一覧表示します。  
  
 **結果**  
 各変換手順の状態を一覧表示します。 状態メッセージをクリックすると、詳細が表示されます。  
  
 プロジェクトの変換は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]でプロジェクトを保存しないと保存されません。  
  
 **[レポートの保存]**  
 プロジェクトの変換の概要を .xml ファイルに保存する場合にクリックします。  
