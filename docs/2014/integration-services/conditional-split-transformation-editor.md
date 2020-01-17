---
title: 条件分割変換エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 920ec41ae30d53853cfb757fb7fc33610953dc86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060893"
---
# <a name="conditional-split-transformation-editor"></a>条件分割変換エディター
  **[条件分割変換エディター]** を使用すると、式の作成、式が評価される順序の設定、条件分割の出力の名前付けを行うことができます。 このダイアログ ボックスには、式の作成に使用する、数学関数、文字列関数、日付/時刻関数や演算子が含まれています。 True として評価される最初の条件は、行が送信される出力を決定します。  
  
> [!NOTE]  
>  条件分割変換は、1 つの出力に対してのみ各入力行を送信します。 複数の条件を入力した場合、変換によって、条件が True である最初の出力に各行が送信され、その行に対して後続する条件は無視されます。 複数の条件を継続して評価する必要がある場合、データ フローで複数の条件分割変換の連結が必要となることがあります。  
  
 条件分割変換の詳細については、「 [条件分割変換](data-flow/transformations/conditional-split-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **書**  
 行を選択し、右側の矢印キーを使用して、式を評価する順序を変更します。  
  
 **[出力名]**  
 出力名を指定します。 既定は数字の付いた場合の一覧ですが、一意のわかりやすい名前を選択することもできます。  
  
 **条件**  
 式を入力するか、使用可能な列、変数、関数、および演算子の一覧からドラッグして式を作成します。  
  
 このプロパティの値は、プロパティ式を使用して指定することができます。  
  
 **関連項目:** [Integration Services &#40;SSIS&#41; 式](expressions/integration-services-ssis-expressions.md)、[演算子 &#40;SSIS 式&#41;](expressions/operators-ssis-expression.md)、[関数 &#40;SSIS 式&#41;](expressions/functions-ssis-expression.md)  
  
 **[既定の出力名]**  
 既定の出力の名前を入力するか、既定を使用します。  
  
 **[エラー出力の構成]**  
 [[エラー出力の構成]](../../2014/integration-services/configure-error-output.md) ダイアログ ボックスを使用して、エラーの処理方法を指定します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [条件分割変換を使用してデータセットを分割する](data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
