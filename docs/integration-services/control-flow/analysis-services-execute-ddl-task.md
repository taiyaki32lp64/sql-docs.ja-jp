---
title: Analysis Services DDL 実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a160e61e390f58dc640a5d1da265cdb77d5d9be1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294338"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 実行タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクは、データ定義言語 (DDL) ステートメントを実行します。DDL ステートメントを使用すると、マイニング モデルや多次元オブジェクト (キューブおよびディメンションなど) を作成、削除、または変更できます。 たとえば DDL ステートメントは、 **Adventure Works** キューブ内にパーティションを作成したり、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]に含まれるサンプルの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のディメンションを削除したりできます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに接続します。 詳しくは、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、分析オブジェクトの処理やデータ マイニング予測クエリの実行など、ビジネス インテリジェンス操作を実行する多数のタスクが含まれます。  
  
 関連するビジネス インテリジェンス タスクの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Analysis Services 処理タスク](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL ステートメント  
 DDL ステートメントは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) のステートメントとして表され、XML for Analysis (XMLA) コマンドで構成されます。  
  
-   ASSL は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンス、それに含まれるデータベースやデータベース オブジェクトの定義、および記述に使用されます。 詳細については、「[Analysis Services スクリプト言語 (XMLA 用 ASSL)](/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)」を参照してください。  
  
-   XMLA は、Create、Alter、Process などのアクション コマンドを、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに送信する場合に使用されるコマンド言語です。 詳細については、「[XML for Analysis (XMLA) リファレンス](/bi-reference/xmla/xml-for-analysis-xmla-reference)」を参照してください。  
  
 DDL コードが別のファイルに格納されている場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクはファイル接続マネージャーを使用して、そのファイルのパスを指定します。 詳しくは「 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)」をご覧ください。  
  
 DDL ステートメントには、パスワードおよびその他の機微な情報が含まれる場合があるため、1 つ以上の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクが含まれるパッケージでは、パッケージの保護レベル **EncryptAllWithUserKey** または **EncryptAllWithPassword** を使用する必要があります。 詳細については、「[Integration Services &#40;SSIS&#41; Packages](../../integration-services/integration-services-ssis-packages.md)」を参照してください。  
  
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
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックをクリックしてください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>プログラムによる Analysis Services DDL 実行タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>[Analysis Services DDL 実行タスク エディター] ([全般] ページ)
  **[Analysis Services DDL 実行タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクの名前と説明を入力できます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクの一意な名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクの説明を入力します。  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>[Analysis Services DDL 実行タスク エディター] ([DDL] ページ)
  **[Analysis Services DDL 実行タスク エディター]** ダイアログ ボックスの **[DDL]** ページを使用すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースへの接続を指定でき、データ定義言語 (DDL) ステートメントのソースについての情報を表示できます。  
  
### <a name="static-options"></a>静的オプション  
 **[接続]**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを一覧で選択するか、\< **[新しい接続...]** > をクリックして **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して新しい接続を作成します。  
  
 **関連トピック:** [[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、[Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **[SourceType]**  
 DDL ステートメントのソースの種類を指定します。 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|**[SourceDirect]** テキスト ボックスに格納される DDL ステートメントへのソースを設定します。 この値を選択すると、次に示す動的オプションが表示されます。|  
|**[ファイル接続]**|DDL ステートメントを含むファイルへのソースを設定します。 この値を選択すると、次に示す動的オプションが表示されます。|  
|**変数**|ソースを変数に設定します。 この値を選択すると、次に示す動的オプションが表示されます。|  
  
### <a name="dynamic-options"></a>動的オプション  
  
#### <a name="sourcetype--direct-input"></a>[SourceType] = [直接入力]  
 **ソース**  
 DDL ステートメントを入力するか、参照ボタン ( **[...]** ) をクリックしてから **[DDL ステートメント]** ダイアログ ボックスでステートメントを入力します。  
  
#### <a name="sourcetype--file-connection"></a>[SourceType] = [ファイル接続]  
 **ソース**  
 一覧でファイル接続を選択するか、\< **[新しい接続...]** > をクリックし、 **[ファイル接続マネージャー]** ダイアログ ボックスを使用して新しい接続を作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>[SourceType] = [変数]  
 **ソース**  
 一覧で変数を選択するか、\< **[新しい変数...]** > をクリックし、 **[変数の追加]** ダイアログ ボックスを使用して新しい接続を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)  
  
