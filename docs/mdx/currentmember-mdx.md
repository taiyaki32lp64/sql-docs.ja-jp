---
title: CurrentMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 374a38d07c3174e799d01199e20e822f85deed13
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892923"
---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)


  反復処理の実行中に、指定された階層の現在のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 階層メンバーのセットに対する反復処理の間、反復の各ステップにおいては、処理対象のメンバーが現在のメンバーになります。 **Currentmember**関数は、そのメンバーを返します。  
  
> [!IMPORTANT]  
>  表示可能な階層がディメンション内に 1 つしかない場合は、ディメンション名がその 1 つしかない階層に解決されるため、その階層はディメンション名でも階層名でも参照できます。 たとえば、は`Measures.CurrentMember` 、Measures ディメンション内の唯一の階層に解決されるため、有効な MDX 式です。  
  
## <a name="examples"></a>使用例  
 次のクエリでは、 **Currentmember**を使用して、列、行、およびスライス軸の階層から現在のメンバーを検索する方法を示しています。  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 現在のメンバーは、クエリの軸で使用される階層で変更されます。 そのため、軸で使用されていない、同じディメンションの他の階層の現在のメンバーも変更される可能性があります。この動作は "自動存在" と呼ばれます。詳細については、「 [MDX &#40;Analysis Services&#41;の主要な概念](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)」を参照してください。 たとえば、次のクエリでは、Date ディメンションの Calendar Year 階層の現在のメンバーが Calendar 階層の現在のメンバーとどのように変化するかを示しています。これは、後者が Rows 軸に表示されるときです。  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **Currentmember**は、使用されているクエリのコンテキストを計算に認識させるために非常に重要です。 次の例では、 **Adventure works**キューブから、各製品の注文数量と、カテゴリおよびモデル別の注文数量の割合を返します。 **Currentmember**関数は、計算時に使用される注文数量を含む製品を識別します。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
