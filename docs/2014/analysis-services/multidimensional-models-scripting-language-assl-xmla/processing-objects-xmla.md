---
title: オブジェクトの処理 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab38ea9b58e891d813a3ca73f43d20a364275da0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727598"
---
# <a name="processing-objects-xmla"></a>オブジェクトの処理 (XMLA)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]処理は、手順、または、ビジネス分析のための情報に手順を有効にするデータを一連の。 処理内容はオブジェクトの種類によって異なりますが、データを情報に変換する処理の一部として必ず実行されます。  
  
 プロセスに、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクトを使用することができます、[プロセス](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)コマンド。 `Process` コマンドでは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの以下のオブジェクトを処理できます。  
  
-   キューブ  
  
-   データベース  
  
-   ディメンション  
  
-   メジャー グループ  
  
-   [マイニング モデル]  
  
-   マイニング構造  
  
-   [メジャー グループ]  
  
 `Process` コマンドには、オブジェクトの処理を制御するために設定できるさまざまなプロパティが用意されています。 `Process` コマンドには、行う処理の程度、処理対象のオブジェクト、不一致バインドを使用するかどうか、エラー処理の方法、および書き戻しテーブルの管理方法を制御するプロパティがあります。  
  
## <a name="specifying-processing-options"></a>処理オプションの指定  
 [型](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)のプロパティ、`Process`コマンド オブジェクトの処理時に使用する処理オプションを指定します。 処理オプションの詳細については、「[処理オプションと設定 &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md)」を参照してください。  
  
 次の表は、`Type` プロパティの定数と、各定数を使用して処理できるさまざまなオブジェクトの一覧を示しています。  
  
|`Type` 値|適用されるオブジェクト|  
|--------------------|------------------------|  
|*ProcessFull*|キューブ、データベース、ディメンション、メジャー グループ、マイニング モデル、マイニング構造、パーティション|  
|*ProcessAdd*|ディメンション、パーティション|  
|*ProcessUpdate*|[ディメンション]|  
|*ProcessIndexes*|ディメンション、キューブ、メジャー グループ、パーティション|  
|*ProcessData*|ディメンション、キューブ、メジャー グループ、パーティション|  
|*ProcessDefault*|キューブ、データベース、ディメンション、メジャー グループ、マイニング モデル、マイニング構造、パーティション|  
|*ProcessClear*|キューブ、データベース、ディメンション、メジャー グループ、マイニング モデル、マイニング構造、パーティション|  
|*ProcessStructure*|キューブ、マイニング構造|  
|*ProcessClearStructureOnly*|マイニング構造|  
|*ProcessScriptCache*|Cube|  
  
 処理の詳細については[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、オブジェクトを参照してください[多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)します。  
  
## <a name="specifying-objects-to-be-processed"></a>処理対象のオブジェクトの指定  
 [オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`Process`コマンドには、処理するオブジェクトのオブジェクト識別子が含まれています。 `Process` コマンドで指定できるオブジェクトは 1 つだけですが、1 つのオブジェクトを処理すると、その子オブジェクトも処理されます。 たとえば、キューブ内のメジャー グループを処理すると、そのメジャー グループのすべてのパーティションが処理されます。また、データベースを処理すると、キューブ、ディメンション、およびマイニング構造など、そのデータベースに含まれるすべてのオブジェクトが処理されます。  
  
 `ProcessAffectedObjects` コマンドの `Process` 属性を true に設定すると、指定されたオブジェクトを処理することによって影響を受ける関連オブジェクトもすべて処理されます。 たとえばを使用して、ディメンションの増分更新、 *ProcessUpdate*処理オプション、`Process`コマンドを任意のパーティションの集計はメンバーの追加、削除によって無効になるもによって処理される[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]場合`ProcessAffectedObjects`設定が true にします。 この場合、1 つの `Process` コマンドで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの複数のオブジェクトを処理することができますが、`Process` コマンドで指定された単一のオブジェクトの他に処理する必要があるオブジェクトは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって決定されます。  
  
 しかし、`Process` コマンドの中で複数の `Batch` コマンドを使用することによって、ディメンションなどの複数のオブジェクトを同時に処理することもできます。 バッチ操作では、`ProcessAffectedObjects` 属性を使用する場合よりも詳細なレベルで、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのオブジェクトの直列または並列処理を制御することができ、大規模な [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの処理方法をチューニングすることができます。 バッチ操作の実行の詳細については、次を参照してください。[バッチ操作の実行&#40;XMLA&#41;](performing-batch-operations-xmla.md)します。  
  
## <a name="specifying-out-of-line-bindings"></a>不一致バインドの指定  
 場合、`Process`コマンドが含まれていない、`Batch`コマンド、アウトオブ ライン バインドで必要に応じて指定できます、[バインド](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)、 [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)、および[DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)のプロパティ、`Process`コマンドを処理するオブジェクト。 不一致バインドは、バインドが `Process` コマンドの実行時のみに存在する、データ ソース、データ ソース ビュー、および他のオブジェクトへの参照であり、処理中のオブジェクトに関連付けられている既存のバインドをオーバーライドします。 不一致バインドが指定されていない場合、処理対象のオブジェクトに現在関連付けられているバインドが使用されます。  
  
 不一致バインドは以下の状況で使用されます。  
  
-   パーティションの増分更新を行う。行が 2 回カウントされないように、代替のファクト テーブルか、既存のファクト テーブルに対するフィルターを指定する必要があります。  
  
-   データ フロー タスクを使用して[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]ディメンション、マイニング モデル、またはパーティションの処理中にデータを提供します。  
  
 不一致バインドは、Analysis Services Scripting Language (ASSL) の一部として記述されます。 ASSL でのアウトオブ ライン バインドの詳細については、次を参照してください。[データ ソースとバインド&#40;SSAS 多次元&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)します。  
  
### <a name="incrementally-updating-partitions"></a>パーティションの増分更新  
 通常、既に処理されているパーティションを増分更新する場合は、不一致バインドが必要です。これは、パーティションに対して指定されているバインドが、既にパーティション内で集計されているファクト テーブル データを参照するためです。 既に処理されているパーティションを `Process` コマンドを使用して増分更新する場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は以下のアクションを実行します。  
  
-   増分更新を行うパーティションと同じ構造の一時パーティションを作成します。  
  
-   `Process` コマンドで指定された不一致バインドを使用して、一時パーティションを処理します。  
  
-   一時パーティションを、選択された既存のパーティションにマージします。  
  
 XML for Analysis (XMLA) を使用してパーティションのマージの詳細については、次を参照してください。[パーティションのマージ&#40;XMLA&#41;](merging-partitions-xmla.md)します。  
  
## <a name="handling-processing-errors"></a>処理エラーの処理  
 [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)のプロパティ、`Process`コマンドを使用して、オブジェクトの処理中に発生したエラーを処理する方法を指定できます。 たとえば、ディメンションの処理時に、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] がキー属性のキー列で重複した値を検出したとします。 属性キーは一意である必要があるため、重複するレコードは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって破棄されます。 に基づいて、 [KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl)プロパティの`ErrorConfiguration`、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でした。  
  
-   エラーを無視し、ディメンションの処理を続行する。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が重複したキーを検出したことを示すメッセージを返し、処理を続行する。  
  
 `ErrorConfiguration` によって `Process` コマンドの実行時のオプションが指定される同様の状況は、他にも多くあります。  
  
## <a name="managing-writeback-tables"></a>書き戻しテーブルの管理  
 `Process` コマンドで、まだ完全に処理されていない書き込み許可パーティション、または完全に処理されていない書き込み許可パーティションに対するキューブやメジャー グループが見つかった場合、そのパーティションには書き戻しテーブルがまだ存在していない可能性があります。 [WritebackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla)のプロパティ、`Process`コマンドを決定するかどうか[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]書き戻しテーブルを作成する必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="description"></a>説明  
 次の例は、[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サンプル データベースを完全に処理します。  
  
### <a name="code"></a>コード  
  
```  
<Process xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>説明  
 次の例では、増分処理、 **Internet_Sales_2004**でパーティション分割、 **Internet Sales**のメジャー グループ、 **Adventure Works DW** 内のキューブ[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]サンプル[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース。 `Process`コマンドは、パーティションに追加する注文の集計、2006 年 12 月 31 日より後の日付でクエリのアウトオブ ライン バインドを使用して、`Bindings`のプロパティ、`Process`生成元となるファクト テーブルの行を取得するコマンドパーティションに追加する集計。  
  
### <a name="code"></a>コード  
  
```  
<Process ProcessAffectedObjects="true" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
