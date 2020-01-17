---
title: DrilldownLevel (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b9c623a1e99053e796609dc82f27519f27c07a9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049290"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  セットで表される最低レベルより 1 つ下のレベルに、セットのメンバーをドリルダウンします。  
  
 レベルを指定する位置をドリル ダウン オプションですのレベルを設定する場合は、いずれかを使用する**レベル式**または**インデックス レベル**。 これらの引数では、相互に排他的です。 最後に、計算されるメンバーがクエリに存在する場合は、行セットに含める引数を指定することができます。  
  
## <a name="syntax"></a>構文  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Level_Expression*  
 (省略可)。 ドリルダウンするレベルを明示的に識別する MDX 式です。 レベル式を指定する場合は、次のインデックスの引数をスキップします。  
  
 *Index*  
 (省略可)。 セット内にドリル ダウン階層数を指定する有効な数値式です。 Level_Expression の代わりに、インデックス レベルを使用すると、ドリルダウンするのにレベルを明示的に識別します。  
  
 *Include_Calc_Members*  
 (省略可)。 計算されるメンバーがドリルダウン レベルに存在する場合にそれらを含めるかどうかを示すフラグです。  
  
## <a name="remarks"></a>コメント  
 **DrilldownLevel**関数は、指定されたセットに含まれるメンバーに基づいて階層の順序で一連の子メンバーを返します。 指定されたセット内の元のメンバー間で順序を維持、それぞれの親メンバーの結果に含まれるすべての子メンバーを設定する点を除いて、関数がすぐに含まれています。  
  
 複数レベルの階層データ構造を指定するには、ドリルダウンするレベルを明示的に選択できます。 レベルを指定する 2 つの相互に排他的な方法はあります。 最初の方法を設定するのには、 **level_expression**は、レベル、別のアプローチを返す MDX 式を使用して引数を指定、**インデックス**引数、数値式を使用しています。番号でレベルを指定します。  
  
 レベル式が指定されている場合、関数は、指定されたレベルにあるメンバーのみの子を取得することによって階層の順序でセットを構築します。 レベル式を指定して、そのレベルのメンバーはありません、レベル式は無視されます。  
  
 インデックス値が指定された場合、この関数は、インデックス (0 を基点とするインデックス) を基準にして、指定されたセット内で参照されている階層の最低レベルより 1 つ上のレベルにあるメンバーの子メンバーだけを取得し、階層の順序でセットを構築します。  
  
 レベル式もインデックス値が指定されている場合、関数は、指定されたセットで参照されている最初の次元の最も低いレベルにあるメンバーのみの子を取得することによって、階層の順序でセットを構築します。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
## <a name="examples"></a>使用例  
 Adventure Works キューブを使用して SSMS で MDX クエリ ウィンドウで次の例を試すことができます。  
  
 **例 1 - 最小構文をデモします。**  
  
 最初の例では、最小構文**DrilldownLevel**します。 唯一必要な引数は、セット式です。 このクエリを実行するとなる親 [All Categories] と [次へ] レベルのメンバーに注意してください: [Accessories]、[Bikes] など。 この例は、単純な基本的な目的を示しています、 **DrilldownLevel**関数で、下のレベルをドリルダウンします。  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 例 2 - 明示的なインデックス レベルを使用する代替構文  
  
 この例では、数値式でインデックスのレベルが指定されている、代替構文を示します。 この場合、インデックス レベルは 0 です。 0 から始まるインデックスでは、これは、最下位のレベルです。  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 前のクエリと同じ結果セットが返されることに注意してください。 一般に、特定のレベルからドリルダウンする場合を除き、インデックス レベルを設定する必要はありません。 上記のクエリでインデックス値を 1 および 2 に設定を再実行します。 インデックスの値が 1 に設定、ドリルダウンされますが、階層内の 2 番目のレベルで参照してください。 インデックスの値が 2 に設定、ドリルダウン、3 番目のレベルが起動し、この例では、最高レベルです。 数値式を大きくするほど、インデックス レベルは高くなります。  
  
 **例 3 - レベル式をデモします。**  
  
 次の例では、レベル式を使用する方法を示します。 階層構造を表すセットを指定するには、レベル式を使用することができます、ドリルダウンを開始する階層のレベルを選択します。  
  
 この例でのドリル ダウン レベルから開始 [市区町村] の 2 番目の引数として、 **DrilldownLevel**関数。 このクエリを実行すると、ワシントン州およびオレゴン州の [City] レベルからドリルダウンされます。 ごと、 **DrilldownLevel**関数場合、結果セットもには [Postal codes] 下のレベルのメンバーが含まれています。  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **例 4 - 計算されるメンバーを含む**  
  
 計算されるメンバーが含まれ、結果の下に表示される設定を追加すると、最後の例に示す、 **include_calculated_members**フラグ。 4 番目のパラメーターとしてフラグが指定されていることを確認します。  
  
 計算されるメンバーが、計算されないメンバーと同じレベルに存在するため、この例は正常に実行されます。 計算されるメンバー [West Coast] は [United States] のメンバーとメンバーの 1 つのレベル [United States] の下のすべてで構成されます。  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 このフラグだけを削除してクエリを再実行すると、計算されるメンバー [West Coast] が除かれた、同じ結果が返されます。  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
