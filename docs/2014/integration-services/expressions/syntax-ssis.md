---
title: 構文 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], syntax
- syntax [Integration Services]
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ed5ea8e711fcc3013a682f8c63a01dc042556f40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768838"
---
# <a name="syntax-ssis"></a>構文 (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式の構文は、C 言語および C# 言語が使用する構文と同様です。 式には、識別子 (列および変数)、リテラル、演算子、関数などの要素が含まれます。 このトピックでは、式エバリュエーターの構文がさまざまな式要素を適用する際の、一意の必要条件の概要について説明します。  
  
> [!NOTE]  
>  前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、式の評価結果の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型が DT_WSTR または DT_STR であるとき、結果の文字数が 4,000 文字に制限されていました。 この制限はなくなっています。  
  
 特定の演算子と関数を使用するサンプル式については、「[演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)」と「[関数 &#40;SSIS 式&#41;](functions-ssis-expression.md)」の演算子または関数別のトピックを参照してください。  
  
 複数の演算子と関数、および識別子とリテラルを使用するサンプル式については、「 [Integration Services 式の詳細の例](examples-of-advanced-integration-services-expressions.md)」を参照してください。  
  
 プロパティの式で使用するサンプル式については、「 [パッケージでプロパティ式を使用する](use-property-expressions-in-packages.md)」を参照してください。  
  
## <a name="identifiers"></a>識別子  
 式には、列および変数の識別子を含めることができます。 列はデータ ソースで生成されるか、またはデータ フローの変換によって作成できます。 式では、系列 ID を使用して列を参照できます。 系列 ID は、パッケージの要素を一意に識別する数値です。 系列 ID を式の内部で参照する場合、系列 ID にポンド (#) プレフィックスを含める必要があります。 たとえば、系列 ID 138 を参照するには、#138 を使用します。  
  
 式には、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] で用意されているシステム変数と、カスタム変数を含めることができます。 変数を式の内部で参照する場合、変数に \@ プレフィックスを含める必要があります。 たとえば、`Counter` 変数を参照する場合、\@Counter を使用します。 \@ 文字は変数名の一部ではなく、式の評価において識別子が変数であることを示すだけのものです。 詳しくは、「[識別子 &#40;SSIS&#41;](identifiers-ssis.md)」をご覧ください。  
  
## <a name="literals"></a>リテラル  
 式には、数値、文字列、およびブール値のリテラルを含めることができます。 文字列リテラルを式で使用するには、引用符で囲む必要があります。 数値リテラルおよびブール値のリテラルには、引用符は付けません。 式言語には、通常エスケープされる文字のエスケープ シーケンスが含まれます。 詳細については、「[リテラル (SSIS)](numeric-string-and-boolean-literals.md)」を参照してください。  
  
## <a name="operators"></a>演算子  
 式エバリュエーターで提供される演算子セットの機能は、Transact-SQL、C++、C# などの言語に含まれる、演算子セットの機能と同様です。 ただし、式言語には別の演算子が含まれており、周知の記号とは異なる記号が使用されます。 詳細については、「[演算子 (SSIS)](operators-ssis-expression.md)」を参照してください。  
  
### <a name="namespace-resolution-operator"></a>名前空間を解決する演算子  
 式では名前空間を解決する演算子 (::) が使用され、同じ名前を持つ複数の変数を明確に識別します。 名前空間を解決する演算子を使用すると、変数をその名前空間で修飾でき、これによって、同じ名前を持つ複数の変数をパッケージ内で使用できます。  
  
#### <a name="cast-operator"></a>キャスト演算子  
 キャスト演算子は、式の結果、列の値、変数の値、および定数を、あるデータ型から別のデータ型に変換します。 式言語が提供するキャスト演算子は、C および C# 言語が提供するものと同様です。 Transact-SQL では、CAST 関数と CONVERT 関数によってこの機能が提供されます。 キャスト演算子の構文は、CAST 関数や CONVERT 関数が使用する構文と、次の点が異なります。  
  
-   式を引数として使用できます。  
  
-   構文に CAST キーワードが含まれません。  
  
-   構文に AS キーワードが含まれません。  
  
##### <a name="conditional-operator"></a>条件演算子  
 条件演算子は、ブール式の評価に基づいて 2 つの式のうちのいずれかの式を返します。 式言語が提供する条件演算子は、C および C# 言語が提供する条件演算子と同様です。 多次元式 (MDX) では、IIF 関数が同様の機能を提供します。  
  
###### <a name="logical-operators"></a>論理演算子  
 式言語では、論理 NOT 演算子の ! 文字がサポートされています。 Transact-SQL では、! 演算子は関係演算子のセットに組み込まれています。 たとえば、Transact-SQL には、> 演算子および !> 演算子が用意されています。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 式言語では、! 演算子とその他の演算子の組み合わせはサポートされません。 たとえば、! と > を結合して !> にすることはできません。 ただし、この式言語では、等しくない比較を表すために、!= の文字の組み合わせがあらかじめサポートされています。  
  
###### <a name="equality-operators"></a>等価演算子  
 式エバリュエーターの文法では、== 等価演算子が用意されています。 この演算子は、Transact-SQL での = 演算子、および C# での == 演算子と同等です。  
  
## <a name="functions"></a>関数  
 式言語には、日付と時刻の関数、数学関数、および文字列関数が提供されています。これらの関数は、Transact-SQL 関数や C# のメソッドと同様です。  
  
 いくつかの関数は、Transact-SQL 関数と同じ名前を持っていますが、式エバリュエーターの関数の機能は微妙に異なります。  
  
-   Transact-SQL の ISNULL 関数は指定した値に NULL 値を置き換えますが、式エバリュエーターの ISNULL 関数は、式が NULL であるかどうかに基づくブール値を返します。  
  
-   Transact-SQL の ROUND 関数には、結果セットを切り捨てるオプションが含まれますが、式エバリュエーターの ROUND 関数には含まれません。  
  
 詳細については、「[関数 (SSIS 式)](functions-ssis-expression.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントで式を使用する](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   pragmaticworks.com の技術記事「 [SSIS 式チート シート](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)」  
  
-   social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
  
