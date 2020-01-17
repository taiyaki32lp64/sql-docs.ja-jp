---
title: Integration Services (SSIS) パッケージおよびプロジェクト パラメーター | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.parameterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b595c8e2c09260e6874fc3cbaab8cc06d2a0c9df
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296169"
---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Integration Services (SSIS) パッケージおよびプロジェクト パラメーター

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) パラメーターを使用すると、パッケージの実行時にパッケージ内のプロパティに値を割り当てることができます。 " *プロジェクト パラメーター* " はプロジェクト レベル、" *パッケージ パラメーター* " はパッケージ レベルで作成できます。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で、 **[Project.params]** ウィンドウを使用して、プロジェクト パラメーターを作成、変更、または削除します。 **デザイナーの** [パラメーター] [!INCLUDE[ssIS](../includes/ssis-md.md)] タブを使用して、パッケージ パラメーターを作成、変更、および削除します。 **[パラメーター化]** ダイアログ ボックスを使用して、新規または既存のパラメーターをタスクのプロパティと関連付けます。 **[Project.params]** ウィンドウと **[パラメーター]** タブの使用の詳細については「 [Create Parameters](https://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99)」を参照してください。 **[パラメーター化]** ダイアログ ボックスの詳細については、「 [Parameterize Dialog Box](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350)」を参照してください。  
  
## <a name="parameters-and-package-deployment-model"></a>パラメーターとパッケージ配置モデル  
 通常、パッケージ配置モデルを使用してパッケージを配置する場合、パラメーターではなく構成を使用する必要があります。  
  
 パッケージ配置モデルを使用してパラメーターを含むパッケージを配置し、パッケージを実行した場合、実行時にパラメーターは呼び出されません。 パッケージにパッケージ パラメーターが含まれ、パッケージ内の式でパラメーターが使用されている場合、実行時に結果の値が適用されます。 パッケージにプロジェクト パラメーターが含まれている場合、パッケージの実行は失敗する可能性があります。  
  
## <a name="parameters-and-project-deployment-model"></a>パラメーターとプロジェクト配置モデル  
 Integration Services (SSIS) サーバーにプロジェクトを配置する場合は、ビュー、ストアド プロシージャ、および [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の UI を使用してプロジェクト パラメーターおよびパッケージ パラメーターを管理します。 詳細については、次の各トピックを参照してください。  
  
-   [ビュー &#40;Integration Services カタログ&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [ストアド プロシージャ &#40;Integration Services カタログ&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [[構成] ダイアログ ボックス](../integration-services/service/configure-dialog-box.md)  
  
-   [[パッケージの実行] ダイアログ ボックス](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>パラメーター値  
 パラメーターに最大 3 つの型の値を割り当てることができます。 パッケージ実行が開始されると、パラメーターに 1 つの値が使用され、パラメーターはその最終的なリテラル値に解決されます。  
  
 次の表に、値の型の一覧を示します。  
  
|値の名前|[説明]|値の型|  
|----------------|-----------------|-------------------|  
|実行値|パッケージ実行の特定のインスタンスに割り当てられる値です。 この割り当ては他のすべての値をオーバーライドしますが、適用されるのは、パッケージ実行の 1 つのインスタンスのみです。|リテラル|  
|サーバーの値|プロジェクトが Integration Services サーバーに配置された後にプロジェクトのスコープ内にあるパラメーターに割り当てられる値です。 この値は、設計上の既定値をオーバーライドします。|リテラルまたは環境変数の参照|  
|設計上の値|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]でプロジェクトを作成または編集するときにパラメーターに割り当てられる値です。 この値はプロジェクトと共に保持されます。|リテラル|  
  
 1 つのパラメーターを使用して、複数のパッケージのプロパティに値を割り当てることができます。 1 つのパッケージのプロパティには、1 つのパラメーターの値のみを割り当てることができます。  
  
###  <a name="executions"></a> 実行とパラメーター値  
 *実行* とは、パッケージ実行の 1 つのインスタンスを表すオブジェクトです。 実行を作成するときに、実行パラメーター値など、パッケージの実行に必要なすべての詳細情報を指定します。 既存の実行のパラメーター値を変更することもできます。  
  
 実行パラメーター値を明示的に設定すると、その値はその特定の実行インスタンスにのみ適用できます。 実行値は、サーバーの値または設計上の値の代わりに使用されます。 実行値を明示的に設定せず、サーバーの値が指定されている場合は、サーバーの値が使用されます。  
  
 パラメーターが必須とマークされている場合、サーバーの値または実行値をそのパラメーターに指定する必要があります。 それ以外の場合、対応するパッケージは実行されません。 デザイン時にパラメーターに既定値が設定されていても、プロジェクトが配置されると使用されることはありません。  
  
#### <a name="environment-variables"></a>環境変数  
 パラメーターが環境変数を参照する場合、その変数のリテラル値は、指定した環境参照を通じて解決され、パラメーターに適用されます。 パッケージ実行に使用される最終的なリテラル パラメーター値は、実行パラメーター値と呼ばれます。 **[実行]** ダイアログ ボックスを使用して、実行の環境参照を指定します。  
  
 プロジェクト パラメーターで環境変数を参照していて、変数のリテラル値を実行時に解決できない場合、設計上の値が使用されます。 サーバーの値は使用されません。  
  
 パラメーター値に割り当てられている環境変数を表示するには、catalog.object_parameters ビューに対してクエリを実行します。 詳細については、「[catalog.object_parameters &#40;SSISDB データベース&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)」を参照してください。  
  
#### <a name="determining-execution-parameter-values"></a>実行パラメーター値の決定  
 次の Transact-SQL ビューとストアド プロシージャを使用して、パラメーター値を表示および設定できます。  
  
 [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) (ビュー)  
 特定の実行で使用される実際のパラメーター値を示します。  
  
 [catalog.get_parameter_values &#40;SSISDB データベース&#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (ストアド プロシージャ)  
 指定されたパッケージと環境参照の実際の値を解決して示します。  
  
 [catalog.object_parameters &#40;SSISDB データベース&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (ビュー)  
 設計上の既定値とサーバーの既定値を含め、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログのすべてのパッケージおよびプロジェクトのパラメーターとプロパティを表示します。  
  
 [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにパラメーターの値を設定します。  
  
 **の** [パッケージの実行] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ダイアログ ボックスを使用してパラメーター値を変更することもできます。 詳細については、「 [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)」を参照してください。  
  
 dtexec の **/Parameter** オプションを使用してパラメーター値を変更することもできます。 詳細については、「 [dtexec Utility](../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
### <a name="parameter-validation"></a>パラメーターの検証  
 パラメーター値を解決できない場合、対応するパッケージ実行は失敗します。 失敗を回避するために、 **の** [検証] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ダイアログ ボックスを使用してプロジェクトとパッケージを検証できます。 検証を使用すると、すべてのパラメーター値に必要な値が設定されているか、または特定の環境参照で必要な値を解決できるかを確認できます。 検証では、その他の一般的なパッケージの問題も確認されます。  
  
 詳細については、「 [Validate Dialog Box](../integration-services/service/validate-dialog-box.md)」を参照してください。  
  
### <a name="parameter-example"></a>パラメーターの例  
 この例では、 **pkgOptions** という名前のパラメーターについて説明します。これは、このパラメーターが存在するパッケージのオプションを指定するために使用されます。  
  
 設計時に、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で作成されたパラメーターには、既定値 1 が割り当てられます。 この既定値は、設計上の既定値と呼ばれます。 プロジェクトが SSISDB カタログに配置され、このパラメーターに他の値が割り当てられなかった場合は、パッケージの実行中に、 **pkgOptions** パラメーターに対応するパッケージ プロパティに値 1 が割り当てられます。 設計上の既定値は、プロジェクトと共にライフ サイクル全体で保持されます。  
  
 特定のパッケージ実行インスタンスの準備中には、 **pkgOptions** パラメーターに値 5 が割り当てられます。 この値は実行値と呼ばれます。これは、その特定の実行インスタンスのパラメーターにのみ適用されるためです。 実行が開始されると、 **pkgOptions** パラメーターに対応するパッケージ プロパティに値 5 が割り当てられます。  
  
## <a name="create-parameters"></a>Create Parameters
プロジェクト パラメーターおよびパッケージ パラメーターを作成するには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用します。 以下の手順では、パッケージ/プロジェクト パラメーターを作成する方法を詳細に説明します。  
  
> **注:** 以前のバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を使用して作成したプロジェクトをプロジェクトの配置モデルに変換する場合は、**Integration Services プロジェクト変換ウィザード**を使用して、構成に基づいたパラメーターを作成できます。 詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
### <a name="create-package-parameters"></a>パッケージ パラメーターを作成する  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを開き、SSIS デザイナーの **[パラメーター]** タブをクリックします。  
  
     ![パッケージの [パラメーター] タブ](../integration-services/media/denali-package-parameters.gif "パッケージの [パラメーター] タブ")  
  
2.  ツール バーの **[パラメーターの追加]** ボタンをクリックします。  
  
     ![ツール バーの [追加] ボタン](../integration-services/media/denali-parameter-add.gif "ツール バーの [追加] ボタン")  
  
3.  一覧で直接、または **[プロパティ]** ウィンドウを使用して、 **[名前]** 、 **[データ型]** 、 **[値]** 、 **[区別する]** 、 **[必須]** の各プロパティに値を入力します。 次の表では、これらのプロパティについて説明します。  
  
    |プロパティ|[説明]|  
    |--------------|-----------------|  
    |[オブジェクト名]|パラメーターの名前。|  
    |データ型|パラメーターのデータ型です。|  
    |既定値|設計時に割り当てられたパラメーターの既定値。 これは設計時の既定値とも呼ばれます。|  
    |区別する|機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。|  
    |Required|パッケージを実行する前に、設計上の既定値以外の値を指定する必要があります。|  
    |[説明]|管理しやすさを考慮した、パラメーターの説明。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、該当するパラメーター ウィンドウでパラメーターを選択したときに、Visual Studio プロパティ ウィンドウでパラメーターの説明を設定します。|  
  
    > **注:** プロジェクトをカタログに配置すると、いくつかのプロパティがプロジェクトに関連付けられます。 カタログ内のすべてのパラメーターのすべてのプロパティを表示するには、[catalog.object_parameters &#40;SSISDB Database&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) ビューを使用します。  
  
4.  プロジェクトを保存して、変更をパラメーターに保存します。 パラメーターの値はプロジェクト ファイルに格納されます。  
  
    > **警告!!** リストで直接編集することも、 **[プロパティ]** ウィンドウを使用してパラメーターのプロパティの値を変更することもできます。 **[削除] \(X)** ツール バー ボタンを使用して、パラメーターを削除できます。 ツール バーの最後のボタンを使用すると、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを実行するときにのみ使用されるパラメーターの値を指定できます。  
  
    > **注:** プロジェクトを [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で開かずにパッケージ ファイルを再度開くと、 **[パラメーター]** タブは空になり、無効になります。  
  
### <a name="create-project-parameters"></a>プロジェクト パラメーターを作成する  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でプロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで **[Project.params]** を右クリックして **[開く]** をクリックするか、または **[Project.params]** をダブルクリックして開きます。  
  
     ![プロジェクト パラメーター ウィンドウ](../integration-services/media/denali-project-parameters.gif "プロジェクト パラメーター ウィンドウ")  
  
3.  ツール バーの **[パラメーターの追加]** ボタンをクリックします。  
  
     ![ツール バーの [追加] ボタン](../integration-services/media/denali-parameter-add.gif "ツール バーの [追加] ボタン")  
  
4.  **[名前]** 、 **[データ型]** 、 **[値]** 、 **[区別する]** 、 **[必須]** の各プロパティに値を入力します。  
  
    |プロパティ|[説明]|  
    |--------------|-----------------|  
    |[オブジェクト名]|パラメーターの名前。|  
    |データ型|パラメーターのデータ型です。|  
    |既定値|設計時に割り当てられたパラメーターの既定値。 これは設計時の既定値とも呼ばれます。|  
    |区別する|機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。|  
    |Required|パッケージを実行する前に、設計上の既定値以外の値を指定する必要があります。|  
    |[説明]|管理しやすさを考慮した、パラメーターの説明。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] では、該当するパラメーター ウィンドウでパラメーターを選択したときに、Visual Studio プロパティ ウィンドウでパラメーターの説明を設定します。|  
  
5.  プロジェクトを保存して、変更をパラメーターに保存します。 パラメーター値はプロジェクト ファイルの構成に格納されます。 プロジェクト ファイルを保存して、パラメーター値の変更をディスクにコミットしてください。  
  
    > **警告!!!** リストで直接編集することも、 **[プロパティ]** ウィンドウを使用してパラメーターのプロパティの値を変更することもできます。 **[削除] \(X)** ツール バー ボタンを使用して、パラメーターを削除できます。 ツール バーの最後のボタンを使用すると、 **[パラメーター値の管理]** ダイアログ ボックスを開いて、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを実行するときにのみ使用されるパラメーターの値を指定できます。  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
**[パラメーター化]** ダイアログ ボックスでは、新規または既存のパラメーターをタスクのプロパティと関連付けることができます。 このダイアログ ボックスを開くには、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでタスクまたは [制御フロー] タブを右クリックし、 **[パラメーター化]** をクリックします。 次の一覧では、このダイアログ ボックスの UI 要素について説明します。 パラメーターの詳細については、「 [Integration Services (SSIS) パラメーター](https://msdn.microsoft.com/library/hh213214.aspx)」を参照してください。
  
### <a name="options"></a>オプション  
 **プロパティ**  
 パラメーターと関連付けるタスクのプロパティを選択します。 この一覧には、パラメーター化できるすべてのプロパティが表示されます。  
  
 **既存のパラメーターを使用する**  
 タスクのプロパティを既存のパラメーターと関連付けるには、このオプションを選択し、ドロップダウン リストからパラメーターを選択します。  
  
 **パラメーターを使用しない**  
 パラメーターへの参照を削除するには、このオプションを選択します。 パラメーターは削除されません。  
  
 **新しいパラメーターを作成する**  
 タスクのプロパティと関連付ける新しいパラメーターを作成するには、このオプションを選択します。  
  
 **[名前]**  
 作成するパラメーターの名前を指定します。  
  
 **[説明]**  
 パラメーターの説明を指定します。  
  
 **Value**  
 パラメーターの既定値を指定します。 これは設計上の既定値とも呼ばれ、後で配置時にオーバーライドできます。  
  
 **スコープ**  
 パラメーターのスコープとして、 **[プロジェクト]** または **[パッケージ]** オプションを指定します。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。  
  
 **機密**  
 チェック ボックスをオンまたはオフにして、パラメーターが機密かどうかを指定します。 機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。  
  
 **必須**  
 パッケージを実行する前に、設計上の既定値以外の値をパラメーターに設定する必要があるかどうかを指定します。  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>プロジェクトを配置した後にパラメーターの値を設定する
配置ウィザードを使用すると、プロジェクトをカタログに配置するときにサーバーの既定のパラメーター値を設定できます。 プロジェクトをカタログに配置した後、SQL Server Management Studio (SSMS) オブジェクト エクスプローラーまたは Transact-SQL を使用して、サーバーの既定値を設定できます。  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>SSMS オブジェクト エクスプ ローラーを使用してサーバーの既定値を設定する  
  
1.  **[Integration Services]** ノードでオブジェクトを選択して右クリックします。  
  
2.  **[プロパティ]** をクリックして、 **[プロジェクトのプロパティ]** ダイアログ ウィンドウを開きます。  
  
3.  **[ページの選択]** の **[パラメーター]** をクリックして、パラメーター ページを開きます。  
  
4.  **[パラメーター]** の一覧で目的のパラメーターを選択します。 注: **[コンテナー]** 列を使用すると、プロジェクト パラメーターとパッケージパラメーターを区別できます。  
  
5.  **[値]** 列で、目的のサーバーの既定のパラメーター値を指定します。  

### <a name="set-server-defaults-with-transact-sql"></a>Transact-SQL を使用してサーバーの既定値を設定する  
 Transact-SQL を使用してサーバーの既定値を設定するには、[catalog.set_object_parameter_value &#40;SSISDB Database&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) ストアド プロシージャを使用します。 現在のサーバーの既定値を表示するには、[catalog.object_parameters &#40;SSISDB Database&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) ビューをクエリします。 サーバーの既定値をクリアするには、[catalog.clear_object_parameter_value &#40;SSISDB Database&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md) ストアド プロシージャを使用します。  
  
## <a name="related-content"></a>関連コンテンツ  
 mattmasson.com のブログ記事、「[SSIS 簡単なヒント: 必要なパラメーター](https://go.microsoft.com/fwlink/?LinkId=239781)」  
  
  
