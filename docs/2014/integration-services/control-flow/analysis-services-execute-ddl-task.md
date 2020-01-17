---
title: Analysis Services DDL 実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a74ab896e974410e8357a22546cb63ed7365a149
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833157"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 実行タスク
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクは、データ定義言語 (DDL) ステートメントを実行します。DDL ステートメントを使用すると、マイニング モデルや多次元オブジェクト (キューブおよびディメンションなど) を作成、削除、または変更できます。 たとえば DDL ステートメントは、 **Adventure Works** キューブ内にパーティションを作成したり、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]に含まれるサンプルの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のディメンションを削除したりできます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに接続します。 詳しくは、「 [Analysis Services 接続マネージャー](../connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、分析オブジェクトの処理やデータ マイニング予測クエリの実行など、ビジネス インテリジェンス操作を実行する多数のタスクが含まれます。  
  
 関連するビジネス インテリジェンス タスクの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Analysis Services 処理タスク](analysis-services-processing-task.md)  
  
-   [データ マイニング クエリ タスク](data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL ステートメント  
 DDL ステートメントは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) のステートメントとして表され、XML for Analysis (XMLA) コマンドで構成されます。  
  
-   ASSL は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンス、それに含まれるデータベースやデータベース オブジェクトの定義、および記述に使用されます。 詳細については、次を参照してください。 [Analysis Services スクリプト言語&#40;ASSL&#41;参照](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)します。  
  
-   XMLA は、Create、Alter、Process などのアクション コマンドを、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに送信する場合に使用されるコマンド言語です。 詳細については、「[XML for Analysis (XMLA) リファレンス](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)」を参照してください。  
  
 DDL コードが別のファイルに格納されている場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクはファイル接続マネージャーを使用して、そのファイルのパスを指定します。 詳しくは「 [File Connection Manager](../connection-manager/file-connection-manager.md)」をご覧ください。  
  
 DDL ステートメントには、パスワードおよびその他の機微な情報が含まれる場合があるため、1 つ以上の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクが含まれるパッケージでは、パッケージの保護レベル `EncryptAllWithUserKey` または `EncryptAllWithPassword` を使用する必要があります。 詳細については、「[Integration Services &#40;SSIS&#41; Packages](../integration-services-ssis-packages.md)」を参照してください。  
  
### <a name="ddl-examples"></a>DDL の例  
 次の 3 つの DDL ステートメントは、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]に含まれる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースである、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスクリプト オブジェクトによって生成されたものです。  
  
 次の DDL ステートメントは、 **Promotion** ディメンションを削除します。  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 次の DDL ステートメントは、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] キューブを処理します。  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 次の DDL ステートメントは、 **Forecasting** マイニング モデルを作成します。  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 次の 3 つの DDL ステートメントは、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]に含まれる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースである、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスクリプト オブジェクトによって生成されたものです。  
  
 次の DDL ステートメントは、 **Promotion** ディメンションを削除します。  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 次の DDL ステートメントは、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] キューブを処理します。  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 次の DDL ステートメントは、 **Forecasting** マイニング モデルを作成します。  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>Analysis Services DDL 実行タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[Analysis Services DDL 実行タスク エディター] ([全般] ページ)](../general-page-of-integration-services-designers-options.md)  
  
-   [[Analysis Services DDL 実行タスク エディター] ([DDL] ページ)](../analysis-services-execute-ddl-task-editor-ddl-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックをクリックしてください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>プログラムによる Analysis Services DDL 実行タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
  
