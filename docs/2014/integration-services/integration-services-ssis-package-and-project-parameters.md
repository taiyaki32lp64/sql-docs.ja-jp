---
title: Integration Services (SSIS) パラメーター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cfd6a65e1561f252574ff919c8b63b0bbd57876f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892247"
---
# <a name="integration-services-ssis-parameters"></a>Integration Services (SSIS) パラメーター
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) パラメーターを使用すると、パッケージの実行時にパッケージ内のプロパティに値を割り当てることができます。 " *プロジェクト パラメーター* " はプロジェクト レベル、" *パッケージ パラメーター* " はパッケージ レベルで作成できます。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で、 **[Project.params]** ウィンドウを使用して、プロジェクト パラメーターを作成、変更、または削除します。 **デザイナーの** [パラメーター] [!INCLUDE[ssIS](../includes/ssis-md.md)] タブを使用して、パッケージ パラメーターを作成、変更、および削除します。 **[パラメーター化]** ダイアログ ボックスを使用して、新規または既存のパラメーターをタスクのプロパティと関連付けます。 **[Project.params]** ウィンドウと **[パラメーター]** タブの使用の詳細については「 [Create Parameters](create-parameters.md)」を参照してください。 **[パラメーター化]** ダイアログ ボックスの詳細については、「 [Parameterize Dialog Box](parameterize-dialog-box.md)」を参照してください。  
  
## <a name="parameters-and-package-deployment-model"></a>パラメーターとパッケージ配置モデル  
 通常、パッケージ配置モデルを使用してパッケージを配置する場合、パラメーターではなく構成を使用する必要があります。  
  
 パッケージ配置モデルを使用してパラメーターを含むパッケージを配置し、パッケージを実行した場合、実行時にパラメーターは呼び出されません。 パッケージにパッケージ パラメーターが含まれ、パッケージ内の式でパラメーターが使用されている場合、実行時に結果の値が適用されます。 パッケージにプロジェクト パラメーターが含まれている場合、パッケージの実行は失敗する可能性があります。  
  
## <a name="parameters-and-project-deployment-model"></a>パラメーターとプロジェクト配置モデル  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置する場合は、ビュー、ストアド プロシージャ、および [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の UI を使用してプロジェクト パラメーターおよびパッケージ パラメーターを管理します。 詳細については、次の各トピックを参照してください。  
  
-   [ビュー &#40;Integration Services カタログ&#41;](/sql/integration-services/system-views/views-integration-services-catalog)  
  
-   [ストアド プロシージャ &#40;Integration Services カタログ&#41;](/sql/integration-services/system-stored-procedures/stored-procedures-integration-services-catalog)  
  
-   [[構成] ダイアログ ボックス](catalog/configure-dialog-box.md)  
  
-   [[パッケージの実行] ダイアログ ボックス](../../2014/integration-services/execute-package-dialog-box.md)  
  
### <a name="parameter-values"></a>パラメーター値  
 パラメーターに最大 3 つの型の値を割り当てることができます。 パッケージ実行が開始されると、パラメーターに 1 つの値が使用され、パラメーターはその最終的なリテラル値に解決されます。  
  
 次の表に、値の型の一覧を示します。  
  
|値の名前|説明|値の型|  
|----------------|-----------------|-------------------|  
|実行値|パッケージ実行の特定のインスタンスに割り当てられる値です。 この割り当ては他のすべての値をオーバーライドしますが、適用されるのは、パッケージ実行の 1 つのインスタンスのみです。|リテラル|  
|サーバーの値|プロジェクトが [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置された後にプロジェクトのスコープ内にあるパラメーターに割り当てられる値です。 この値は、設計上の既定値をオーバーライドします。|リテラルまたは環境変数の参照|  
|設計上の値|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]でプロジェクトを作成または編集するときにパラメーターに割り当てられる値です。 この値はプロジェクトと共に保持されます。|リテラル|  
  
 1 つのパラメーターを使用して、複数のパッケージのプロパティに値を割り当てることができます。 1 つのパッケージのプロパティには、1 つのパラメーターの値のみを割り当てることができます。  
  
###  <a name="executions"></a> 実行とパラメーター値  
 *実行* とは、パッケージ実行の 1 つのインスタンスを表すオブジェクトです。 実行を作成するときに、実行パラメーター値など、パッケージの実行に必要なすべての詳細情報を指定します。 既存の実行のパラメーター値を変更することもできます。  
  
 実行パラメーター値を明示的に設定すると、その値はその特定の実行インスタンスにのみ適用できます。 実行値は、サーバーの値または設計上の値の代わりに使用されます。 実行値を明示的に設定せず、サーバーの値が指定されている場合は、サーバーの値が使用されます。  
  
 パラメーターが必須とマークされている場合、サーバーの値または実行値をそのパラメーターに指定する必要があります。 それ以外の場合、対応するパッケージは実行されません。 デザイン時にパラメーターに既定値が設定されていても、プロジェクトが配置されると使用されることはありません。  
  
#### <a name="environment-variables"></a>環境変数  
 パラメーターが環境変数を参照する場合、その変数のリテラル値は、指定した環境参照を通じて解決され、パラメーターに適用されます。 パッケージ実行に使用される最終的なリテラル パラメーター値は、実行パラメーター値と呼ばれます。 **[実行]** ダイアログ ボックスを使用して、実行の環境参照を指定します。  
  
 プロジェクト パラメーターで環境変数を参照していて、変数のリテラル値を実行時に解決できない場合、設計上の値が使用されます。 サーバーの値は使用されません。  
  
 パラメーター値に割り当てられている環境変数を表示するには、catalog.object_parameters ビューに対してクエリを実行します。 詳細については、「[catalog.object_parameters &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)」を参照してください。  
  
#### <a name="determining-execution-parameter-values"></a>実行パラメーター値の決定  
 次の Transact-SQL ビューとストアド プロシージャを使用して、パラメーター値を表示および設定できます。  
  
 [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database) (ビュー)  
 特定の実行で使用される実際のパラメーター値を示します。  
  
 [catalog.get_parameter_values &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database) (ストアド プロシージャ)  
 指定されたパッケージと環境参照の実際の値を解決して示します。  
  
 [catalog.object_parameters &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) (ビュー)  
 設計上の既定値とサーバーの既定値を含め、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログのすべてのパッケージおよびプロジェクトのパラメーターとプロパティを表示します。  
  
 [catalog.set_execution_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにパラメーターの値を設定します。  
  
 **の** [パッケージの実行] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ダイアログ ボックスを使用してパラメーター値を変更することもできます。 詳細については、「 [Execute Package Dialog Box](../../2014/integration-services/execute-package-dialog-box.md)」を参照してください。  
  
 dtexec の `/Parameter` オプションを使用してパラメーター値を変更することもできます。 詳しくは、「 [dtexec Utility](packages/dtexec-utility.md)」をご覧ください。  
  
### <a name="parameter-validation"></a>パラメーターの検証  
 パラメーター値を解決できない場合、対応するパッケージ実行は失敗します。 失敗を回避するために、 **の** [検証] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ダイアログ ボックスを使用してプロジェクトとパッケージを検証できます。 検証を使用すると、すべてのパラメーター値に必要な値が設定されているか、または特定の環境参照で必要な値を解決できるかを確認できます。 検証では、その他の一般的なパッケージの問題も確認されます。  
  
 詳細については、「 [Validate Dialog Box](catalog/validate-dialog-box.md)」を参照してください。  
  
### <a name="parameter-example"></a>パラメーターの例  
 この例では、 **pkgOptions** という名前のパラメーターについて説明します。これは、このパラメーターが存在するパッケージのオプションを指定するために使用されます。  
  
 設計時に、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で作成されたパラメーターには、既定値 1 が割り当てられます。 この既定値は、設計上の既定値と呼ばれます。 プロジェクトが SSISDB カタログに配置され、このパラメーターに他の値が割り当てられなかった場合は、パッケージの実行中に、 **pkgOptions** パラメーターに対応するパッケージ プロパティに値 1 が割り当てられます。 設計上の既定値は、プロジェクトと共にライフ サイクル全体で保持されます。  
  
 特定のパッケージ実行インスタンスの準備中には、 **pkgOptions** パラメーターに値 5 が割り当てられます。 この値は実行値と呼ばれます。これは、その特定の実行インスタンスのパラメーターにのみ適用されるためです。 実行が開始されると、 **pkgOptions** パラメーターに対応するパッケージ プロパティに値 5 が割り当てられます。  
  
## <a name="related-tasks"></a>Related Tasks  
 [パラメーターの作成](create-parameters.md)  
  
 [プロジェクトを配置した後にパラメーターの値を設定する](../../2014/integration-services/set-parameter-values-after-the-project-is-deployed.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 mattmasson.com のブログ記事、「[SSIS 簡単なヒント: 必要なパラメーター](https://go.microsoft.com/fwlink/?LinkId=239781)」  
  
  
