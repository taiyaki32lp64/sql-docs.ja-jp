---
title: 条件分割変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcfbbac9eacc96384a723088cf8f20cc939bdc48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900826"
---
# <a name="conditional-split-transformation"></a>条件分割変換
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
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、入力データを評価して出力データを出力する式を作成するために使用できる、関数と演算子が含まれます。 詳細については、「 [Integration Services (SSIS) 式](../../expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
 条件分割変換には、`FriendlyExpression` カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「 [パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md) 」および「 [変換のカスタム プロパティ](transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つ以上の出力、および 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[条件分割変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [[条件分割変換エディター]](../../conditional-split-transformation-editor.md)」を参照してください。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [条件分割変換を使用してデータセットを分割する](conditional-split-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [条件分割変換を使用してデータセットを分割する](conditional-split-transformation.md)  
  
## <a name="see-also"></a>参照  
 [データ フロー](../data-flow.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
