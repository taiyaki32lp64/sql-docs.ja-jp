---
title: 条件分割変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.conditionalsplittrans.f1
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d1e4cddbdad631a5602096f92915a4fe78b23d67
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298004"
---
# <a name="conditional-split-transformation"></a>条件分割変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  条件分割変換では、データ行をデータの内容に応じた別の出力にルートできます。 条件分割変換の実装は、プログラミング言語の CASE 決定構造と同様です。 この変換は式を評価し、その結果に基づいて、データ行を指定された出力に送信します。 この変換には既定の出力も用意されているため、行が式に一致しない場合は既定の出力に送信されます。  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>条件分割変換の構成  
 条件分割変換は、次の方法で構成できます。  
  
-   変換をテストする各条件に対して、ブール型に評価される式を指定します。  
  
-   条件を評価する順序を指定します。 行は、TRUE に評価される最初の条件に対応した出力へ送信されるため、順序の指定は重要です。  
  
-   変換に対する既定の出力を指定します。 この変換では、既定の出力を指定する必要があります。  
  
 各入力行は、1 つの出力にのみ送信できます。この出力は、TRUE に評価される最初の条件に対する出力です。 たとえば、次の条件は、 **FirstName** 列にある文字 *A* で始まる行を 1 つの出力に、文字 *B* で始まる行を別の 1 つの出力に、その他のすべての行を既定の出力に送信します。  
  
 出力 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 出力 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、入力データを評価して出力データを出力する式を作成するために使用できる、関数と演算子が含まれます。 詳細については、「 [Integration Services (SSIS) 式](../../../integration-services/expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
 条件分割変換には、**FriendlyExpression** カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「 [パッケージでプロパティ式を使用する](../../../integration-services/expressions/use-property-expressions-in-packages.md) 」および「 [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つ以上の出力、および 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [条件分割変換を使用してデータセットを分割する](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [条件分割変換を使用してデータセットを分割する](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## <a name="conditional-split-transformation-editor"></a>条件分割変換エディター
  **[条件分割変換エディター]** を使用すると、式の作成、式が評価される順序の設定、条件分割の出力の名前付けを行うことができます。 このダイアログ ボックスには、式の作成に使用する、数学関数、文字列関数、日付/時刻関数や演算子が含まれています。 True として評価される最初の条件は、行が送信される出力を決定します。  
  
> [!NOTE]  
>  条件分割変換は、1 つの出力に対してのみ各入力行を送信します。 複数の条件を入力した場合、変換によって、条件が True である最初の出力に各行が送信され、その行に対して後続する条件は無視されます。 複数の条件を継続して評価する必要がある場合、データ フローで複数の条件分割変換の連結が必要となることがあります。  
  
### <a name="options"></a>オプション  
 **書**  
 行を選択し、右側の矢印キーを使用して、式を評価する順序を変更します。  
  
 **[出力名]**  
 出力名を指定します。 既定は数字の付いた場合の一覧ですが、一意のわかりやすい名前を選択することもできます。  
  
 **条件**  
 式を入力するか、使用可能な列、変数、関数、および演算子の一覧からドラッグして式を作成します。  
  
 このプロパティの値は、プロパティ式を使用して指定することができます。  
  
 **関連項目:** [Integration Services &#40;SSIS&#41; 式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[演算子 &#40;SSIS 式&#41;](../../../integration-services/expressions/operators-ssis-expression.md)、[関数 &#40;SSIS 式&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **[既定の出力名]**  
 既定の出力の名前を入力するか、既定を使用します。  
  
 **[エラー出力の構成]**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスを使用して、エラーの処理方法を指定します。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
