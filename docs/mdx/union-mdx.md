---
title: Union (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 170e3764795e1bb6db3fc9589ecf1fe486078633
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097298"
---
# <a name="union--mdx"></a>Union (MDX)


  重複するメンバーを残すこともできます 2 つのセットの和集合によって生成されるセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>引数  
 *セット式 1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *セット式 2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 この関数は、2 つの和集合を返します。 または、複数の指定されたセット。 標準の構文および代替構文 1、重複が既定で除外されます。 標準の構文を使用して、**すべて**フラグは、結合されたセットに重複部分を保持します。 重複部分は、セットの末尾から削除されます。 代替構文 2 では、重複部分が常に保持されます。  
  
## <a name="examples"></a>使用例  
 次の例では、動作、**共用体**各構文を使用して機能します。  
  
### <a name="standard-syntax-duplicates-eliminated"></a>標準構文、重複部分の除去  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>標準構文、重複部分の保持  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>代替構文 1、重複部分の除去  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>代替構文 2、重複の保持  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [+&#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
