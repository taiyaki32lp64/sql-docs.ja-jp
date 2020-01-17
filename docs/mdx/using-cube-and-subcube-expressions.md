---
title: Cube 式およびサブキューブ式の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7c656bdaa0de108ade568a22bbcc734f38d43bfd
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893537"
---
# <a name="using-cube-and-subcube-expressions"></a>キューブ式とサブキューブ式の使用


  多次元式 (MDX) ステートメントでは、キューブまたはサブキューブのデータを定義、操作、または取得するために、キューブ式やサブキューブ式を使用します。  
  
## <a name="cube-expressions"></a>キューブ式  
 キューブ式には、キューブ識別子または CURRENTCUBE キーワードが含まれているので、単純式のみを指定できます。 多くの MDX ステートメントでは、キューブ識別子を要求する代わりに、CURRENTCUBE キーワードを使用して現在のキューブコンテキストを識別します。  
  
 キューブ識別子は、MDX ステートメントの BNF 表記の説明に*Cube_Name*として表示されます。  
  
 キューブ式は複数の場所に表示される場合があります。 MDX の SELECT ステートメントでは、キューブ式は、データの取得元のキューブを指定します。 次のクエリの例では、[Adventure Works] という式は、その名前のキューブを参照しています。  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 CREATE MEMBER ステートメントでは、キューブ式は、作成中の計算されるメンバーが表示されるキューブを指定します。 次の例では、ステートメントは、Adventure Works キューブの Measures ディメンションに対して計算されるメジャーを作成します。  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 MDX スクリプト内で CREATE MEMBER ステートメントを使用すると、キューブの名前を CURRENTCUBE キーワードに置き換えることができます。これは、計算されるメンバーが作成されるキューブが、MDX スクリプトが属しているキューブと同じである必要があるためです (followingexamp を参照)。&  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 これにより、キューブの名前がハードコーディングされなくなったため、あるキューブから別のキューブに計算されるメンバーの定義を簡単にコピーして貼り付けることができます。  
  
## <a name="subcube-expressions"></a>サブキューブ式  
 サブキューブ式には、サブキューブ識別子、またはサブキューブを返す MDX ステートメントを含めることができます。 サブキューブ式にサブキューブ識別子が含まれている場合は、単純式になります。 サブキューブを返す MDX ステートメントが含まれている場合は、複雑なステートメントです。 たとえば、次の例に示すように、MDX の SELECT ステートメントは、サブキューブを返すので、サブキューブ式が許可されている場所で使用できます。  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 FROM 句での SELECT ステートメントの使用は、サブセレクトとも呼ばれます。  
  
 サブキューブ式が発生するもう1つの一般的なシナリオは、MDX スクリプトでスコープ付き割り当てを行う場合です。 次の例では、SCOPE ステートメントを使用して、[Measures] で構成されるサブキューブに割り当てを制限しています。[Internet Sales Amount]:  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 サブキューブ識別子は*Subcube_Name*として表示されます。 MDX ステートメントの BNF 表記について説明します。  
  
## <a name="see-also"></a>関連項目  
 [MDX の基本的なクエリ &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query)   
 [MDX &#40;mdx でのサブキューブの作成&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)   
 [CREATE サブキューブ&#40;ステートメント MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [MDX &#40;の式&#41;](../mdx/expressions-mdx.md)   
 [SCOPE ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)  
  
  
