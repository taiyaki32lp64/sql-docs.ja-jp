---
title: 識別子 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c11561ac71aa72469a809ea25297d62133aa93da
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891219"
---
# <a name="identifiers-mdx"></a>識別子 (MDX)


  識別子は Analysis Services オブジェクトの名前です。 すべてのオブジェクトは、識別子を持つことができます。 これには、キューブ、ディメンション、階層、レベル、メンバーなどが含まれます。 多次元式 (MDX) ステートメントの中でオブジェクトを参照するには、オブジェクトの識別子を使用します。  
  
 オブジェクトの名前を指定する方法によっては、オブジェクト識別子の識別子は、標準または区切られた識別子のいずれかになります。  
  
> [!NOTE]  
>  標準識別子と区切られた識別子は、どちらも 1 ~ 100 文字で指定する必要があります。  
  
## <a name="using-regular-identifiers"></a>標準識別子の使用  
 標準識別子は、標準識別子の次の書式規則に準拠するオブジェクト名です。 標準識別子は、区切り記号の有無にかかわらず使用できます。  
  
### <a name="formatting-rules-for-regular-identifiers"></a>標準識別子の規則の書式設定  
  
1.  最初の文字が次のいずれかである必要があります。  
  
    -   Unicode 規格 &#xa0;2.0 で定義されている文字。 Unicode の文字の定義には、他の言語の文字に加えて、a ~ z および A ~ Z のラテン文字も含まれます。  
  
    -   アンダースコア (_)。  
  
2.  名前の先頭以外では、次の文字を使用できます。  
  
    -   Unicode 規格 &#xa0;2.0 で定義されているようになりました。  
  
    -   Basic Latin スクリプトまたはその他の各国スクリプトの 10 進数  
  
    -   アンダースコア (_)。  
  
3.  MDX の予約されたキーワードを識別子にすることはできません。 MDX では、予約済みキーワードの大文字と小文字は区別されません。 詳細については、「 [Reserved &#40;Keywords&#41;MDX 構文](../mdx/reserved-keywords-mdx-syntax.md)」を参照してください。  
  
4.  埋め込み型スペースおよび特殊文字は使用できません。  
  
### <a name="examples-of-regular-identifiers"></a>標準識別子の例  
 以下の MDX ステートメントで、`Measures`、`Product`、および `Style` 識別子は、標準識別子の形式の規則に従っています。 これらの標準識別子には、区切り記号は必要ありません。  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 必須ではありませんが、標準識別子に区切り記号を使用することもできます。 次の MDX ステートメントでは、 `Measures`、 `Product`、および`Style`の標準識別子は、角かっこで正しく区切られています。  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>区切られた識別子の使用  
 標準識別子の形式の規則に従わない識別子は、必ず角かっこ ([]) で区切る必要があります。  
  
> [!NOTE]  
>  区切り記号は識別子のみに使用されます。 キーワードがで[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]予約済みとしてマークされているかどうかにかかわらず、キーワードに区切り記号を使用することはできません。  
  
 区切られた識別子は、次のような場合に使用します。  
  
-   オブジェクトの名前または名前の一部に予約語を使用する場合。  
  
     予約されたキーワードをオブジェクト名として使用しないことをお勧めします。 以前のバージョンのからアップグレード[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]されたデータベースには、以前のバージョンでは予約されていないが予約済みの単語を含む識別子が含まれる場合があります。 オブジェクトの識別子を変更できるようになるまでの間は、区切られた識別子を使ってオブジェクトを参照できます。  
  
-   オブジェクトの名前に、修飾された識別子として示されていない文字を使用する場合。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]区切られた識別子で現在のコードページ内の任意の文字を使用できるようにします。 しかし、むやみにオブジェクト名に特殊文字を使用すると、MDX ステートメントやスクリプトが読みにくくなり、メンテナンスが困難になります。  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>区切られた識別子の形式の規則  
 区切られた識別子の本体には、現在のコードページ内の文字の任意の組み合わせを含めることができます (区切り文字自体を含む)。 区切られた識別子の本体に区切り記号が含まれている場合、特殊な処理が必要です。  
  
-   識別子の本体に左角かっこ ([) しか含まれていない場合は、追加の処理は必要ありません。  
  
-   識別子の本体に右角かっこ (]) が含まれている場合は、2つの右角かっこ (]) を指定する必要があります。  
  
### <a name="examples-of-delimited-identifiers"></a>区切られた識別子の例  
 次の MDX ステートメント`Sales Volume` `Sales Cube`では、、、および`select`は区切られた識別子です。  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 次の例のオブジェクトの名前は `Total Profit [Domestic]` です。 このオブジェクトを参照するには、以下の区切られた識別子を使用する必要があります。  
  
 `[Total Profit [Domestic]]]`  
  
 `Domestic` の前の左角かっこを変更せずに、区切られた識別子を作成できることに注意してください。 しかし、`Domestic` の後の右角かっこは、2 つの右角かっこに置き換える必要があります。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>複数の部分に区切られた識別子  
 修飾されたオブジェクト名を使用する場合、オブジェクト名を構成する識別子の1つ以上を区切る必要があります。 たとえば、次のコードのフロントブレーキ識別子には、区切り記号を使用する必要があります。  
  
 [Measures] を選択します。列のメンバー、  
  
 [Product]。[Product]。[前面ブレーキ]行  
  
 FROM [Adventure Works]  
  
 また、前の例の Measures 識別子は、複数の識別子を区切るために区切られています。  
  
## <a name="see-also"></a>関連項目  
 [MDX 言語リファレンス &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX クエリの基礎 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)   
 [Mdx 構文要素&#40;mdx&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
