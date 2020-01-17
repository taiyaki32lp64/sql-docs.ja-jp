---
title: This (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 12455c82fe7a885a3530b6c0db216b9996a5eda6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893558"
---
# <a name="this-mdx"></a>This (MDX)


  多次元式 (MDX) 計算スクリプトで、割り当てに使用する現在のサブキューブを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
This   
```  
  
## <a name="remarks"></a>コメント  
 **この**関数は、MDX 計算スクリプト内の現在のスコープ内で現在のサブキューブを指定するために、任意のサブキューブ式の代わりに使用できます。 **この**関数は、代入の左側で使用する必要があります。  
  
## <a name="examples"></a>使用例  
 次の MDX スクリプトでは、This キーワードを SCOPE ステートメントと共に使用してサブキューブに代入する方法を示します。  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [計算](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
  
