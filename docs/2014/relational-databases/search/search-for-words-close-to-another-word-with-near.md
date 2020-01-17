---
title: NEAR による他の単語の近くにある単語の検索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fadff7e68404ffae528cb4630e1f6c4b8156ccc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011064"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>NEAR による他の単語の近くにある単語の検索
  [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 述語または [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 関数で近接語句 (NEAR) を使用すると、互いに似た単語や語句を検索できます。 最初の検索語句と最後の検索語句を分離する非検索用語の最大数を指定することもできます。 さらに、任意の順序で語や句を検索したり、指定した順序で語や句を検索したりすることができます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 両方を以前サポート[汎用近接語句](#Generic_NEAR)が、非推奨となりましたが、[カスタム近接語句](#Custom_NEAR)、新機能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]します。  
  
##  <a name="Custom_NEAR"></a> カスタム近接語句  
 カスタム近接語句では、次のような新しい機能を使用できます。  
  
-   一致する順序で、最初と最後の検索語句を分離する非検索用語の最大数 (*最大距離*) を指定できます。  
  
-   語句の最大数を指定する場合、検索語句が特定の順序で一致するように指定することもできます。  
  
 一致と見なされるには、文字列が次の条件を満たす必要があります。  
  
-   指定した検索語句のいずれかで始まり、他の指定した検索語句のいずれかで終わる。  
  
-   指定したすべての検索語句を含む。  
  
-   ストップワードなど、最初の検索語句と最後の検索語句の間にある非検索用語の数は、最大距離以下である必要がある (指定した場合)。  
  
 基本構文は次のとおりです。  
  
 NEAR (  
  
 {  
  
 *search_term* [ ,...*n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
  
> [!NOTE]  
>  <custom_proximity_term> 構文の詳細については、「[CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)」を参照してください。  
  
 たとえば、次のように "Smith" から 2 つの語の範囲内にある "John" を検索できます。  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 一致する文字列の例としては、"`John Jacob Smith`" や "`Smith, John`" などがあります。 文字列"`John Jones knows Fred Smith`" は 3 つの非検索語句が間にあるので一致しません。  
  
 指定した順序で語句を検索する必要がある場合は、例の近接語句を `NEAR((John, Smith),2, TRUE).` に変更します。これにより、"`John`" が "`Smith`" の前にある場合のみ、"`John`" から 2 語の範囲内にある "`Smith`" が検索されます。 英語など、左から右に読む言語では、"`John Jacob Smith`" が一致する文字列です。  
  
 アラビア語、ヘブライ語など、右から左に読む言語では、フルテキスト エンジンは、指定した言語に逆の順序で適用されることに注意してください。 また、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーは、右から左に読む言語では指定した語句の表示順序を自動的に逆にします。  
  
> [!NOTE]  
>  詳細については、後の「[近接検索に関するその他の注意点](#Additional_Considerations)」を参照してください。  
  
### <a name="how-maximum-distance-is-measured"></a>最大距離の測定方法  
 10 や 25 など特定の最大距離を指定すると、指定した文字列の最初の検索語句と最後の検索語句の間にある、ストップワードなどの非検索語句の数が決定されます。 たとえば、 `NEAR((dogs, cats, "hunting mice"), 3)` は次の行を返します。ここでは、非検索語句の数は 3 つ ("`enjoy`"、"`but`"、および "`avoid`") です。  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 同じ近接語句でも次の行は返しません。非検索語句が 4つ ("`enjoy`"、"`but`"、"`usually`"、および "`avoid`") であるため最大距離を超えているからです。  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### <a name="combining-a-custom-proximity-term-with-other-terms"></a>カスタム近接語句とその他の語句との組み合わせ  
 カスタム近接語句とその他の語句とを組み合わせることができます。 AND (&)、OR (|)、または AND NOT (&!) を使用して、カスタム近接語句と他のカスタム近接語句、単純語句、またはプレフィックス語句を組み合わせることができます。 以下に例を示します。  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 例を次に示します。  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 汎用近接語句と、カスタム近接語句を組み合わせることはできません (*term1* NEAR *term2*)、生成語句 (ISABOUT…)、または重み付け語句 (FORMSOF…)。  
  
### <a name="example-using-the-custom-proximity-term"></a>例:カスタム近接語句の使用  
 次の例では、 `Production.Document` サンプル データベースの `AdventureWorks2012` テーブルを検索して、"reflector" という語を "bracket" と同一のドキュメント内に含むすべてのドキュメントの概要を検出します。  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  

  
##  <a name="Additional_Considerations"></a> 近接検索に関する追加の考慮事項  
 このセクションでは、汎用およびカスタム近接検索の両方に影響する注意点について説明します。  
  
-   検索語句の出現の重複  
  
     すべての近接検索は、重複しない語句だけを常に検索します。 検索語句で重複する語句は、一致とは認識されません。 たとえば、最大距離が 2 語で`A`および`AA`をこの順序で検索する次の近接語句について検討してみます。  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     一致する語句としては、`AAA`、`A.AA`、および`A..AA`が考えられます。 `AA`だけを含む行は一致しません。  
  
    > [!NOTE]  
    >  たとえば、 `NEAR("mountain bike", "bike trails")` または `(NEAR(comfort*, comfortable), 5)`などの重複する語句は指定できます。 重複する語句を指定すると、一致する可能性がある順列が増えることでクエリの複雑さが増大します。 このような重複する語句を多数指定するとリソースが不足し、クエリが失敗することがあります。 この現象が発生する場合は、クエリを簡略化してもう一度やり直してください。  
  
-   汎用 NEAR もカスタム NEAR も、指定した最大距離に関係なく、語句間の絶対的な距離ではなく論理的な距離を示します。 たとえば、段落内の別の語句や文に含まれている語は、同じ語句や文に含まれている語に比べて関連度が低いと想定されるため、実際の近接度に関係なく、より離れているものとして扱われます。 同様に、別の段落にある語は、さらに離れているものとして扱われます。 一致する語句が、文、段落、または章の末尾にまで及ぶ場合、ドキュメントの順位付けに使用される間隔は、それぞれ 8、128、または 1024 ずつ増加します。  
  
-   CONTAINSTABLE 関数による順位付けへの近接語句の影響  
  
     NEAR を CONTAINSTABLE 関数で使用する場合は、ドキュメント内のその長さに関連する一致数と、各一致における最初の検索語句と最後の検索語句の間の距離が、各ドキュメントの順位付けに影響します。 汎用近接語句では、たとえば、一致する検索語間の距離が 50 論理語より大きい場合、そのドキュメントについて返される順位は 0 になります。 最大距離として整数を指定しないカスタム近接語句では、間隔が 100 論理語より大きい一致のみを含むドキュメントは、順位 0 を取得します。 カスタム近接語句の順位付けの詳細については、「[RANK を使用して検索結果を制限する方法](limit-search-results-with-rank.md)」を参照してください。  
  
-   **transform noise words** サーバー オプション  
  
     **transform noise words[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の値は、ストップワードが近接検索で指定されている場合、** がストップワードを処理する方法に影響を与えます。 詳細については、「 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)」を参照してください。  
  

  
##  <a name="Generic_NEAR"></a> 非推奨の汎用近接語句  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用することをお勧め、[カスタム近接語句](#Custom_NEAR)します。  
  
 汎用近接語句とは、検索用語の間で検索されない語句の数 ( *距離*) に関係なく、特定の用語がドキュメントで一致すればすべて返されることを示します。 基本構文は次のとおりです。  
  
 { *search_term* { NEAR | ~ } *search_term* } [ ,...*n* ]  
  
 たとえば、次の例では、"fox" という語と "chicken" という語が任意の順序で両方とも含まれる場合に一致として検出されます。  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  <generic_proximity_term> 構文の詳細については、「[CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)」を参照してください。  
  
 詳細については、後述の「[近接検索に関するその他の注意点](#Additional_Considerations)」を参照してください。  
  
### <a name="combining-a-generic-proximity-term-with-other-terms"></a>汎用近接語句とその他の語句との組み合わせ  
 AND (&)、OR (|)、または AND NOT (&!) を使用して、汎用近接語句と他の汎用近接語句、単純語句、またはプレフィックス語句を組み合わせることができます。 例 :  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 など、カスタム近接語句と、汎用近接語句を組み合わせることはできません`NEAR((term1,term2),5)`、重み付け語句 (ISABOUT…)、または生成語句 (FORMSOF…)。  
  
### <a name="example-using-the-generic-proximity-term"></a>例:汎用近接語句の使用  
 次の例では、汎用近接語句を使用して、"reflector" という語と "bracket" という語を同一のドキュメント内で検索します。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 CONTAINSTABLE では用語の順序を逆に指定しても、同じ結果を得ることができます。  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 前の例で NEAR キーワードの代わりにチルダ (~) を指定しても同じ結果を得ることができます。  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 検索条件で 3 つ以上の語または句を指定できます。 たとえば、次のように記述できます。  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 これは、"reflector" という語が "bracket" と同じドキュメント内に含まれ、"bracket" という語が "installation" と同じドキュメント内に含まれる必要があることを意味しています。  
  

  
## <a name="see-also"></a>関連項目  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [フルテキスト検索でのクエリ](query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
