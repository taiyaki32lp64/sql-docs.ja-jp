---
title: "計算されるセルのセッション スコープの作成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0953df9aa142ce6826e96a3715970d51ec15158
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>セッション スコープの計算されるセルの MDX セル計算
    
> [!IMPORTANT]  
>  この構文は推奨されません。 代わりに、MDX 割り当てを使用してください。 割り当ての詳細については、「[基本的な MDX スクリプト &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)」を参照してください。  
  
 同じセッション内のすべてのクエリで使用可能な計算されるセルを作成するには、[CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) ステートメントまたは [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) ステートメントを使用できます。 どちらのステートメントを使用しても結果は同じになります。  
  
## <a name="create-cell-calculation-syntax"></a>CREATE CELL CALCULATION の構文  
  
> [!IMPORTANT]  
>  この構文は推奨されません。 代わりに、MDX 割り当てを使用してください。 割り当ての詳細については、「[基本的な MDX スクリプト &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)」を参照してください。  
  
 セッション スコープの計算されるセルを定義するために CREATE CELL CALCULATION ステートメントを使用するには、次の構文を使用します。  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>ALTER CUBE の構文  
  
> [!IMPORTANT]  
>  この構文は推奨されません。 代わりに、MDX 割り当てを使用してください。 割り当ての詳細については、「[基本的な MDX スクリプト &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)」を参照してください。  
  
 セッション スコープの計算されるセルを定義するために ALTER CUBE ステートメントを使用するには、次の構文を使用します。  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 `String_Expression` 値には、直交する 1 次元の MDX セット式のリストを指定します。それぞれの式は、次の表のいずれかのセット カテゴリに解決される必要があります。  
  
|カテゴリ|Description|  
|--------------|-----------------|  
|空セット|空セットに解決される MDX セット式。 この場合、計算されるセルのスコープはキューブ全体です。|  
|単一メンバー セット|1 つのメンバーに解決される MDX セット式。|  
|レベル メンバーのセット|単一レベルのメンバーに解決される MDX セット式。 この例として、 *Level_Expression*.**Members** MDX 関数があります。 計算されるメンバーを含めるには、*Level_Expression*.**AllMembers** MDX 関数を使用します。<br /><br /> 詳細については、「[AllMembers (MDX)](../../../mdx/allmembers-mdx.md)」を参照してください。|  
|子孫のセット|指定したメンバーの子孫に解決される MDX セット式。 この例として、**Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*) MDX 関数があります。<br /><br /> 詳細については、「[Descendants (MDX)](../../../mdx/descendants-mdx.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [MDX でのセル計算の作成 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  