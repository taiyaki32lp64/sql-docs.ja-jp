---
title: パス順序と解決順序について (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7c17bf520f1feaf454d784658c8abc423dbe7a0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75229430"
---
# <a name="understanding-pass-order-and-solve-order-mdx"></a>パス順序と解決順序の概要 (MDX)
  MDX スクリプトの結果としてキューブが計算される場合、計算に関連するさまざまな機能の使われ方によっては、キューブは多数の計算段階をたどることがあります。 それらの各段階は、計算パスと呼ばれます。  
  
 計算パスは、計算パス番号と呼ばれる序数で表すこともできます。 キューブのセルすべてを完全に計算するために必要な計算パスの数を、キューブの計算パスの深さと呼びます。  
  
 パス 0 に影響するのはファクト テーブルと書き戻しデータだけです。 スクリプトがデータを設定するのはパス 0 の後です。ステートメント内に代入や計算ステートメントがある場合、新しいパスが作成されます。 MDX スクリプト以外では、絶対パス 0 への参照がある場合、それはキューブに対するスクリプトによって最後に作成されたパスを意味します。  
  
 計算されるメンバーはすべてのパスで作成されますが、式が適用されるのは現在のパスです。 以前のパスには計算されるメジャーが含まれますが、値は NULL です。  
  
## <a name="solve-order"></a>解決順序  
 解決順序は、競合する式がある場合に計算の優先順位を決定します。 1 つのパスの中では、解決順序によって以下の 2 つの順序が決まります。  
  
-   がディメンション、メンバー [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 、計算されるメンバー、カスタムロールアップ、および計算されるセルを評価する順序。  
  
-   カスタム メンバー、計算されるメンバー、カスタム ロールアップ、および計算されるセルが [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] によって計算される順序。  
  
 最も高い解決順序を持つメンバーが最も優先されます。  
  
> [!NOTE]  
>  この優先順位に関する例外は、Aggregate 関数です。 Aggregate 関数を使用して計算されるメンバーの解決順序は、交差するどの計算されるメジャーの解決順序よりも低くなります。  
  
## <a name="solve-order-values-and-precedence"></a>解決順序の値と優先順位  
 解決順序は、-8,181 ～ 65,535 の値をとります。 この範囲内で、いくつかの解決順序の値は、次の表のように特定の種類の計算に対応しています。  
  
|計算|解決順序|  
|-----------------|-----------------|  
|カスタム メンバー式|-5119|  
|単項演算子|-5119|  
|表示部分の合計計算|-4096|  
|その他のすべての計算 (特に指定されていない場合)|0|  
  
 解決順序の値を設定するときは、正の整数のみを使用することを強くお勧めします。 前の表に示されている解決順序の値よりも低い値を割り当てると、計算パスが予測不能になることがあります。 たとえば、計算されるメンバーの計算に、解決順序の値として既定のカスタム ロールアップ式の値である -5119 より低い値を割り当てるとします。 このように低い解決順序の値を持つ計算されるメンバーはカスタム ロールアップ式より先に計算され、正確な結果が得られないことがあります。  
  
### <a name="creating-and-changing-solve-order"></a>解決順序の作成と変更  
 キューブ デザイナーでは、 **[計算]** ペインで計算の順序を変更することによって、計算されるメンバーと計算されるセルの解決順序を変更できます。  
  
 MDX では、計算されるメンバーや計算されるセルを作成または変更するときに `SOLVE_ORDER` キーワードを使用できます。  
  
## <a name="solve-order-examples"></a>解決順序の例  
 解決順序がどれほど複雑なものになることがあるかを示すために、個別のクエリとしては解決順序を考慮する必要のない 2 つのクエリで始まる一連の MDX クエリを次に示します。 それらの 2 つのクエリを組み合わせると、解決順序を考慮しなければならないクエリになります。  
  
> [!NOTE]  
>  Adventure Works サンプル多次元データベースに対してこれらの MDX クエリを実行できます。 
  [AdventureWorks Multidimensional Models SQL Server 2012](https://msftdbprodsamples.codeplex.com/releases/view/55330) サンプルは、CodePlex サイトからダウンロードできます。  
  
### <a name="query-1-differences-in-income-and-expenses"></a>クエリ 1-収益と経費の違い  
 1 番目の MDX クエリとして、年ごとの売上とコストの差を計算するために、次の例のような単純な MDX クエリを作成します。  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 このクエリでは、計算されるメンバーは `Year Difference`の 1 つだけです。 計算されるメンバーが 1 つだけなので、キューブで計算されるメンバーが使用されない限り、解決順序を考慮する必要はありません。  
  
 この MDX クエリは、次の表のような結果セットを作成します。  
  
||Internet Sales Amount|Internet Total Product Cost|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**年の差**|($20,160.56)|$2,878.06|  
  
### <a name="query-2-percentage-of-income-after-expenses"></a>クエリ 2-経費後の収益の割合  
 2 番目のクエリとして、年ごとの経費差し引き後の収益のパーセンテージを計算するために、次の MDX クエリを使用します。  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 前のクエリと同様、この MDX クエリでも計算されるメンバーは `Profit Margin`の 1 つだけであるため、解決順序の複雑さはありません。  
  
 この MDX クエリは、次の表のようなわずかに異なる結果セットを作成します。  
  
||Internet Sales Amount|Internet Total Product Cost|利益率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 1 番目のクエリと 2 番目のクエリの結果セットの違いは、計算されるメンバーの配置位置の違いによるものです。 1 番目のクエリでは、計算されるメンバーは ROWS 軸の一部ですが、2 番目のクエリの場合は COLUMNS 軸の一部になっています。 次の例で、2 つの計算されるメンバーを 1 つの MDX クエリで組み合わせて使用するときに、この配置位置の違いが重要になります。  
  
### <a name="query-3-combined-year-difference-and-net-income-calculations"></a>クエリ 3-年の差と純利益の計算の組み合わせ  
 最後のクエリでは、前の 2 つの例を 1 つの MDX クエリに結合します。このとき、列と行の両方で計算を行うため、解決順序が重要になります。 計算が正しい順序で確実に行われるように、`SOLVE_ORDER` キーワードを使用して計算の行われる順序を定義します。  
  
 
  `SOLVE_ORDER` キーワードは、MDX クエリまたは `CREATE MEMBER` コマンド内の計算されるメンバーの解決順序を指定します。 
  `SOLVE_ORDER` キーワードで使用される整数値は相対値であり、0 で始まる必要はありません。また、連続値である必要もありません。 この値は、より高い値を持つメンバーを計算して得られる値に基づいてそのメンバーを計算するように MDX に指示するだけです。 計算されるメンバーの定義に `SOLVE_ORDER` キーワードが含まれていない場合、その計算されるメンバーの既定値は 0 です。  
  
 たとえば、最初の 2 つの例のクエリで使用されている計算を結合すると、計算対象となる 2 つのメンバーである `Year Difference` と `Profit Margin`は、MDX クエリの例の結果データセット内にある 1 つのセルで交差します。 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] がこのセルをどのように評価するかを決定する唯一の方法は、解決順序を指定することです。 このセルを作成するために使用する数式は、2 つの計算されるメンバーの解決順序に応じて、異なる結果を作成します。  
  
 まず、最初の 2 つのクエリで使用されている計算を次の MDX クエリのように結合してみます。  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 この結合された MDX クエリの例では、 `Profit Margin` が最も高い解決順序を持つため、2 つの式が相互作用するときに優先されます。 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は、問題のセルを `Profit Margin` の数式を使用して評価します。 この入れ子にされた計算は、次の表に示すような結果を作成します。  
  
||Internet Sales Amount|Internet Total Product Cost|利益率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**年の差**|($20,160.56)|$2,878.06|114.28%|  
  
 共有されるセルの結果は、 `Profit Margin`の数式に基づいています。 つまり、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は共有されるセルの結果を `Year Difference` のデータを使用して計算し、次の数式を作成します。結果はわかりやすくするために丸めてあります。  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 または  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 これは明らかに正しくありません。 しかし、MDX クエリ内の計算されるメンバーの解決順序を入れ替えると、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は共有されるセルの結果を異なる方法で計算します。 次の結合された MDX クエリでは、計算されるメンバーの解決順序を逆にしています。  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 計算されるメンバーの順序が入れ替わったため、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は `Year Difference` の数式を使用してセルを評価します。結果は次の表のようになります。  
  
||Internet Sales Amount|Internet Total Product Cost|利益率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**年の差**|($20,160.56)|$2,878.06|(0.15%)|  
  
 このクエリは `Year Difference` の数式を使用し、 `Profit Margin` のデータをその数式に使用するため、共有されるセルの数式は次の計算のようになります。  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 または  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>追加の考慮事項  
 解決順序の問題は、計算されるメンバー、カスタム ロールアップ式、または計算されるセルの関係するディメンションが多数あるキューブの場合は特に、非常に複雑になります。 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] が MDX クエリを評価するとき、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は、MDX クエリで指定されているキューブのディメンションも含め、特定のパスに関係するものすべての解決順序の値を考慮します。  
  
## <a name="see-also"></a>参照  
 [計算 Ationcurrentpass &#40;MDX&#41;](/sql/mdx/calculationcurrentpass-mdx)   
 [MDX&#41;&#40;計算 Ationpass 値](/sql/mdx/calculationpassvalue-mdx)   
 [CREATE MEMBER ステートメント &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [MDX&#41;&#40;データを操作する](mdx-data-manipulation-manipulating-data.md)  
  
