---
title: CREATE CELL CALCULATION ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7ba563c848179e8cf3dc12f64d2b3c4233955159
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892165"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>MDX データ操作 - CREATE CELL CALCULATION


  キューブ内の指定された組のセットに対して多次元式 (MDX) 式を評価する計算を作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列です。  
  
 *Calculation_Name*  
 セルの計算名を提供する有効な文字列です。  
  
 *Set_Expression*  
 セットを返す有効な MDX 式です。  
  
 *String*  
 有効な文字列値。  
  
 *MDX_Expression*  
 有効な MDX 式です。  
  
 *Logical_Expression*  
 有効な MDX 論理式です。  
  
 *Integer*  
 有効な整数値。  
  
 *Calculation_Name*  
 セル計算プロパティの名前を提供する有効な文字列です。  
  
 *Scalar_Expression*  
 有効な MDX スカラー式です。  
  
## <a name="remarks"></a>コメント  
 クライアントアプリケーションでは、計算されるセルを使用することによって、カスタムロールアップ式や計算されるメンバーの場合と同様に、セルのセット全体ではなく、特定のセルのセットに対してロールアップ値を指定できます。 たとえば、`{[Canada],[Time].[2000]}` によって定義されるセット内のセルに、特定の式によって定義される値を入れる、といった指定が可能です。 このセット内に含まれていないその他のセルは、通常どおりに計算されます。  
  
> [!NOTE]  
>  の`{*(<comment> | <whitespace> | <newline>)}`バッカスナウア記法-backus-naur Form (BNF) は、下位互換性の`{*}`ためにとして解析されます。  
  
## <a name="see-also"></a>関連項目  
 [セッションスコープの計算されるセルの作成](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [クエリ スコープのセル計算の作成 (MDX)](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [MDX &#40;mdx でのセル計算の作成&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [セル プロパティの使用 &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [FORMAT_STRING の内容 (MDX)](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [FORE_COLOR と BACK_COLOR の&#40;内容 MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
