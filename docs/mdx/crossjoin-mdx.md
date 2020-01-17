---
title: Crossjoin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 63de71ae82e60b8ec7d8a39e18f89e6bd2393f2d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892946"
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)


  1 つ以上のセットのクロス積を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **Crossjoin**関数は、2つ以上の指定されたセットのクロス積を返します。 結果セット内の組の順序は、結合されるセットの順序とメンバーの順序によって異なります。 たとえば、最初のセットが {x1, x2,..., x*n*} で構成され、2番目のセットが {y1, y2,..., y*n*} で構成されている場合、これらのセットのクロス積は次のようになります。  
  
 {(x1, y1)、(x1, y2),..., (x1, y*n*)、(x2, y1)、(x2, y2),...,  
  
 (x2、y*n*),..., (x*n*, y1)、(x*n*、y2),..., (xn, y*n*)}  
  
> [!IMPORTANT]  
>  クロス結合内のセットが同一ディメンションの異なる属性階層の組から構成されている場合、この関数は実際に存在する組のみを返します。 詳細については、「 [MDX &#40;Analysis Services&#41;の主要概念](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次のクエリは、クエリの Columns 軸と Rows 軸で Crossjoin 関数を使用する簡単な例を示しています。  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 次の例は、同じディメンションの異なる階層がクロス結合されている場合に行われる自動フィルター処理を示しています。  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 次の3つの例では、米国内の州の州別の Internet Sales Amount と同じ結果が返されます。 最初の2つは2つのクロス結合構文を使用し、3番目の例では WHERE 句を使用して同じ情報を返す方法を示しています。  
  
### <a name="example-1"></a>例 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>例 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>例 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
