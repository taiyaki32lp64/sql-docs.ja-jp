---
title: 式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a1dfcdc52bb52652c204e31c28ccf5ec48ca7a00
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893596"
---
# <a name="expressions-mdx"></a>式 (MDX)


  式は、結果を取得するために評価できる識別子、値、および演算子の組み合わせです。 データは、データにアクセスしたり変更したりするときに、さまざまな場所で使用できます。 たとえば、クエリによって取得されるデータの一部として式を使用したり、一連の条件を満たすデータを探す検索条件として使用したりできます。  
  
## <a name="simple-and-complex-expressions"></a>単純式と複合式  
 MDX では、式は単純または複雑にすることができます。  
  
 単純式とは、次のような式です。  
  
 定数  
 定数は、MDX の単一の特定の値を表す記号です。 文字列、数値、および日付の値は定数として表示できます。 数値定数とは異なり、文字列定数と日付定数は単一引用符 (') で区切る必要があります。  
  
 スカラー関数  
 MDX のスカラー関数は、評価のコンテキスト内で単一の値を返します。 この区別は、MDX がスカラー関数を解決する方法を理解する上で重要です。ほとんどの MDX 式、ステートメント、およびスクリプトは、1つのデータ要素ではなく評価されますが、セルやメンバーなどのデータ要素のグループを反復処理するためです。 ただし、スカラー関数が評価された時点では、通常、この関数は単一のデータ要素を確認します。  
  
 オブジェクト識別子  
 MDX は、多次元データの性質上、オブジェクト指向です。 オブジェクト識別子は、MDX の単純式と見なされます。 識別子の詳細については[、 &#40;「&#41;MDX の識別子](../mdx/identifiers-mdx.md)」を参照してください。  
  
 複合式は、演算子によって結合されたこれらのエンティティの組み合わせから構築できます。  
  
## <a name="expression-results"></a>式の結果  
 1つの定数、変数、スカラー関数、または列名で構成される単純な式の場合、式のデータ型、照合順序、有効桁数、小数点以下桁数、および値は、参照される要素のデータ型、照合順序、有効桁数、小数点以下桁数、および値になります。 MDX が直接サポートするのは OLE VARIANT データ型だけなので、単純式で強制型変換が発生することはありません。  
  
 複雑な式の場合は、異なるデータ型を持つ2つ以上の単純な式を使用すると強制型変換が発生する可能性があります。  
  
## <a name="expression-examples"></a>式の例  
 次のクエリでは、定義が単純式である、計算されるメジャーの例を示します。  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 式は、のように`[Measures].[Discount Amount] * 1.5`計算することもできます。 次の例では、計算を使用して、MDX の SELECT ステートメントでメンバーを定義する方法を示します。  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[キューブ式とサブキューブ式の使用](../mdx/using-cube-and-subcube-expressions.md)|キューブ式とサブキューブ式を定義します。|  
|[ディメンション式の使用](../mdx/using-dimension-expressions.md)|ディメンション式を定義します。|  
|[メンバー式の使用](../mdx/using-member-expressions.md)|メンバー式を定義します。|  
|[組式の使用](../mdx/using-tuple-expressions.md)|組式を定義します。|  
|[セット式の使用](../mdx/using-set-expressions.md)|セット式を定義します。|  
|[スカラー関数の使用](../mdx/using-scalar-expressions.md)|スカラー式を定義します。|  
|[空の値の操作](../mdx/working-with-empty-values.md)|空の値とは何か、そのような値がどのように処理されるかを説明します。|  
  
## <a name="see-also"></a>関連項目  
 [MDX 言語リファレンス &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX クエリの基礎 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)  
  
  
