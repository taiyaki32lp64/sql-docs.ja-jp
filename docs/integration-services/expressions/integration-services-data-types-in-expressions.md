---
title: 式における Integration Services データ型 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e2c8c8f77fd0643c503f5b817b050ff64529751
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297547"
---
# <a name="integration-services-data-types-in-expressions"></a>式における Integration Services データ型

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  式エバリュエーターは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型を使用します。 データが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローに入力されると、データ フロー エンジンはすべての列データを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に変換します。このため、式が列データを使用するときには、既に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型になっています。 条件分割変換および派生列変換で使用される式は、列データが含まれるデータ フローの一部であるため、列を参照できます。  
  
## <a name="variables"></a>変数:  
 また、式は変数を使用することもできます。 変数は variant データ型で、式エバリュエーターは、変数のデータ型を variant サブタイプから [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に変換してから式を評価します。 変数では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型のサブセットのみが使用できます。 たとえば、変数はバイナリ ラージ オブジェクト (BLOB) データ型を使用することはできません。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型と [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に対する ｖariant データ型のマッピングについては、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="literals"></a>リテラル  
 式には、文字列、ブール、および数値リテラルも含めることができます。 数値リテラルの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数値データ型への変換の詳細については、「[ &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)」を参照してください。  
  
## <a name="strings"></a>文字列  
 DT_STR または DT_WSTR のいずれかを、式の戻り値の型として使用できます。 ただし、式の内部でサポートされるのは DT_WSTR のみです。DT_STR 値は DT_WSTR 値に変換されます。 式を作成するときは、これを考慮する必要があります。  
  
-   式の内部では、NULL(DT_STR, ...) ではなく NULL(DT_WSTR, ...) を使用します。この関数の詳細については、「[NULL &#40;SSIS 式&#41;](../../integration-services/expressions/null-ssis-expression.md)」を参照してください。  
  
-   式の内部では、式のルートでのみ、つまり最終的な式の結果を返すときにのみ、CAST 関数を使用して、値を DT_STR 型にキャストできます。 それ以外の場合は、式で DT_WSTR 型を使用します。  
  
 次のスクリーン ショットの式について考えてみましょう。  
  
 ![SSIS 式の文字列データ型](../../integration-services/expressions/media/stringsinssisexpressions.png "SSIS 式の文字列データ型")  
  
1.  最初の式は、NULL(DT_STR, ...) 関数が式のルート レベルにあるため、エラーなしで実行されます。  
  
2.  2 番目の式は、NULL(DT_WSTR, ...) が使用されているため、エラーなしで実行されます。  
  
3.  3 番目の式は、式の内部で NULL(DT_STR, ...) が使用されているため、エラーが発生します。  
  
4.  4 番目の式は、式の内部で NULL(DT_STR, ...) の結果をキャストしているため、エラーなしで実行されます。  
  
     この式エバリュエーターは、計算が式のルート レベルで行われていないことを認識し、このキャストをインテリジェントに処理して、DT_STR ではなく DT_WSTR にキャストします。  
  
 以下の例は、キャストの影響を示しています。  
  
 ![SSIS 式のキャスト文字列](../../integration-services/expressions/media/stringsinssisexpressions2.png "SSIS 式のキャスト文字列")  
  
1.  最初の式は、キャストが式のルート レベルにありません。 式エバリュエーターは、このキャストをインテリジェントに処理し、DT_STR ではなく、DT_WSTR にキャストします。 式は DT_WSTR を返します。  
  
2.  2 番目の式は、キャストが式のルート レベルにあります。 式は DT_STR を返します。  
  
## <a name="implicit-data-conversion"></a>暗黙的なデータ変換  
 データ型の暗黙的な変換は、式エバリュエーターがあるデータ型を別のデータ型に自動的に変換するときに行われます。 たとえば、 **smallint** 型を **int**型と比較する場合、比較を実行する前に、 **smallint** 型から **int** 型に暗黙的に変換されます。  
  
 引数やオペランドに互換性のないデータ型がある場合は、式エバリュエーターは暗黙的なデータ変換を実行できません。 また、式エバリュエーターは、どのような値もブール値に暗黙的に変換することはできません。 代わりに、キャスト演算子を使用して引数とオペランドを明示的に変換する必要があります。 詳細については、「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」を参照してください。  
  
 次の図は、BINARY 演算での暗黙的な変換の結果のデータ型を示しています。 この表の列と行の交差部分は、左 (変換元) と右 (変換先) の型のオペランドによるバイナリ演算の結果のデータ型です。  
  
 ![データ型間における暗黙的なデータ型の変換](../../integration-services/expressions/media/mw-dts-impl-conver-02.gif "データ型間における暗黙的なデータ型の変換")  
  
 符号付き整数と符号なし整数の積集合は符号付き整数になり、この値はどちらかの引数よりも大きい場合があります。  
  
 演算子は、文字列、日付、ブール値、およびその他のデータ型を比較します。 演算子が 2 つの値を比較する前に、式エバリュエーターは特定の暗黙的な変換を実行します。 式エバリュエーターは、文字列リテラルを DT_WSTR データ型に、ブール型リテラルを DT_BOOL データ型に、常に変換します。 式エバリュエーターは、引用符で囲まれたすべての値を文字列として解釈します。 数値リテラルは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の数値データ型のいずれかに変換されます。  
  
> [!NOTE]  
>  ブール値は論理値であり、数値ではありません。 ブール値は一部の環境で数値として表示される場合がありますが、数値として格納されることはありません。また、.NET Framework のメソッドと同様に、さまざまなプログラミング言語でブール値が個別の数値として表されます。  
>   
>  たとえば、Visual Basic で利用できる変換関数では **True** は -1 に変換されますが、.NET Framework の **System.Convert.ToInt32** メソッドでは **True** は +1 に変換されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の式言語では、 **True** は -1 に変換されます。  
>   
>  エラーや予期しない結果が発生しないように、 **True** および **False**については、特定の数値を参照するようなコードは記述しないでください。 可能な限り、ブール型の変数には、仕様で定められている論理値以外の値を使用しないようにしてください。  
  
 詳細については、次の各トピックを参照してください。  
  
-   [== &#40;等しい&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/equal-ssis-expression.md)  
  
-   [\!= &#40;等しくない&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/unequal-ssis-expression.md)  
  
-   [&#62; &#40;より大きい&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)  
  
-   [&#60; &#40;より小さい&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/less-than-ssis-expression.md)  
  
-   [&#62;= &#40;以上&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)  
  
-   [&#60;= &#40;以下&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)  
  
 関数の引数が 1 つの場合、その関数は引数と同じデータ型の結果を返します。ただし、次の場合は除きます。  
  
-   DAY、MONTH、および YEAR は、日付型から整数 (DT_I4) 型の結果を返します。  
  
-   ISNULL は、任意の [!INCLUDE[ssIS](../../includes/ssis-md.md)] データ型の式からブール (DT_BOOL) 型の結果を返します。  
  
-   SQUARE および SQRT は、数値式から非整数の数値 (DT_R8) 型の結果を返します。  
  
 複数の引数が同じデータ型の場合、結果も同じデータ型になります。 ただし、DT_DECIMAL データ型の 2 つの値におけるバイナリ演算の結果だけは例外で、DT_NUMERIC データ型の結果を返します。  
  
## <a name="requirements-for-data-used-in-expressions"></a>式で使用されるデータの要件  
 式エバリュエーターは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のすべてのデータ型をサポートします。 ただし、演算または関数によっては、オペランドや引数で特定のデータ型が必要になります。 式エバリュエーターは、式で使用されるデータに対し、次のデータ型を要求します。  
  
-   **論理** 演算で使用するオペランドは、ブール型に評価される必要があります。 たとえば、ColumnA > 1&&ColumnB < 2 などの場合です。  
  
-   **数学的** 演算で使用するオペランドは、数値に評価される必要があります。 たとえば、23.75 * 4 などの場合です。  
  
-   論理演算や等価演算などの比較演算で使用するオペランドは、互換性のあるデータ型に評価される必要があります。  
  
     たとえば、次の例に示す式の 1 つでは DT_DBTIMESTAMPOFFSET データ型が使用されています。  
  
     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`  
  
     式 `(DT_DBDATE)"1999-10-12"`は DT_DBTIMESTAMPOFFSET に変換されます。 変換された式は "1999-10-12 00:00:00.000 +00:00" となり、他の式の値 `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`と一致しないため、TRUE に評価されます。  
  
-   数学関数に渡される引数は、数値データ型に評価される必要があります。 関数または演算によっては、特定の数値データ型が必要となる場合があります。 たとえば HEX 関数では、符号付き整数または符号なし整数が必要です。  
  
-   文字列関数に渡される引数は、次の文字データ型に評価される必要があります。DT_STR または DT_WSTR。 たとえば、UPPER("flower") などの場合です。 SUBSTRING などの一部の文字列関数では、さらに、文字列の開始位置や長さを指定するために整数の引数が必要となります。  
  
-   日付と時刻の関数に渡される引数は、有効な日付に評価される必要があります。 たとえば、DAY(GETDATE()) などの場合です。 DATEADD などの一部の関数では、さらに、関数が日付に追加する日数を指定するために整数の引数が必要となります。  
  
 符号なし 8 バイト整数と符号付き整数を結合する演算では、結果の形式を明確にするために明示的なキャストが必要です。 詳細については、「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 演算や関数の結果のデータ型は、多くの場合、定義済みのものです。 つまり、引数のデータ型、または式エバリュエーターが結果をキャストするデータ型として定義されています。 たとえば、論理 OR 演算子 (||) の結果は常にブール型で、ABS 関数の結果は引数と同じ数値データ型になります。また、乗算の結果は、結果を失うことなく保持可能な最小の数値データ型になります。 結果のデータ型については、「[ &#40;SSIS Expression&#41;](../../integration-services/expressions/operators-ssis-expression.md)」と「[ &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントで式を使用する](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   pragmaticworks.com の技術記事「 [SSIS 式チート シート](https://go.microsoft.com/fwlink/?LinkId=746575)」  
  
-   social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
  
