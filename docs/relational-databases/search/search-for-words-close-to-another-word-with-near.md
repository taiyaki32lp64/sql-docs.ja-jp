---
title: NEAR による他の単語の近くにある単語の検索 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e94bdcf4770190d3d84986b511996213fac17f9
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702830"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>NEAR による他の単語の近くにある単語の検索
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 述語または [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 関数で*近接語句* (**NEAR**) を使用すると、互いに似た単語や語句を検索できます。 
  
##  <a name="Custom_NEAR"></a> NEAR の概要  
**NEAR** には次の機能があります。  
-   最初の検索語句と最後の検索語句を分離する非検索用語の最大数を指定することができます。

-   任意の順序で単語や語句を検索したり、指定した順序で単語や語句を検索したりすることができます。
  
-   一致する順序で、最初と最後の検索語句を分離する非検索用語の最大数 ( *最大距離*) を指定できます。  

-   語句の最大数を指定する場合、検索語句が特定の順序で一致するように指定することもできます。

 
 一致と見なされるには、文字列が次の条件を満たす必要があります。  
  
-   指定した検索語句のいずれかで始まり、他の指定した検索語句のいずれかで終わる。  
  
-   指定したすべての検索語句を含む。  
  
-   ストップワードなど、最初の検索語句と最後の検索語句の間にある非検索用語の数は、最大距離 (指定されている場合) 以下である必要がある。  
  
## <a name="syntax-of-near"></a>NEAR の構文
**NEAR** の基本構文は次のとおりです。  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,...*n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

構文の詳細については、「[CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)」を参照してください。  

## <a name="examples"></a>使用例
### <a name="example-1"></a>例 1
 たとえば、次のように "Smith" から 2 つの語の範囲内にある "John" を検索できます。  
  
```sql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 一致する文字列の例としては、"`John Jacob Smith`" や "`Smith, John`" などがあります。 文字列"`John Jones knows Fred Smith`" は 3 つの非検索語句が間にあるので一致しません。  
  
 指定した順序で語句を検索する必要がある場合は、例の近接語句を `NEAR((John, Smith),2, TRUE).` に変更します。これにより、"`John`" が "`Smith`" の前にある場合のみ、"`John`" から 2 語の範囲内にある "`Smith`" が検索されます。 英語など、左から右に読む言語では、"`John Jacob Smith`" が一致する文字列です。  
  
 アラビア語、ヘブライ語など、右から左に読む言語では、フルテキスト エンジンは、指定した言語に逆の順序で適用されることに注意してください。 また、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーは、右から左に読む言語では指定した語句の表示順序を自動的に逆にします。   

### <a name="example-2"></a>例 2
 次の例では、 `Production.Document` サンプル データベースの `AdventureWorks` テーブルを検索して、"reflector" という語を "bracket" と同一のドキュメント内に含むすべてのドキュメントの概要を検出します。  
  
```sql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>最大距離の測定方法  
 10 や 25 など特定の最大距離を指定すると、指定した文字列の最初の検索語句と最後の検索語句の間にある、ストップワードなどの非検索語句の数が決定されます。 たとえば、 `NEAR((dogs, cats, "hunting mice"), 3)` は次の行を返します。ここでは、非検索語句の数は 3 つ ("`enjoy`"、"`but`"、および "`avoid`") です。  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 同じ近接語句でも次の行は返しません。非検索語句が 4つ ("`enjoy`"、"`but`"、"`usually`"、および "`avoid`") であるため最大距離を超えているからです。  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>NEAR と他の語句を組み合わせる  
 NEAR と他のいくつかの語句を組み合わせることができます。 AND (&)、OR (|)、または AND NOT (&!) を使用して、カスタム近接語句と他のカスタム近接語句、単純語句、またはプレフィックス語句を組み合わせることができます。 例:  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NEAR((*term3*, *term4*),2)')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR NEAR((*term3*, *term4*),2, TRUE)')  
  
 例を次に示します。  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 NEAR を生成語句 (ISABOUT ...) や重み付け語句 (FORMSOF ...) と組み合わせることはできません。  
  
##  <a name="Additional_Considerations"></a> 近接検索に関する詳細情報  
   
-   検索語句の出現の重複  
  
     すべての近接検索は、重複しない語句だけを常に検索します。 検索語句で重複する語句は、一致とは認識されません。 たとえば、最大距離が 2 語で`A`および`AA`をこの順序で検索する次の近接語句について検討してみます。  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA), 2, TRUE)')
    ```  
  
     一致する語句としては、`AAA`、`A.AA`、および`A..AA`が考えられます。 `AA`だけを含む行は一致しません。  
  
    > [!NOTE]  
    >  たとえば、 `NEAR("mountain bike", "bike trails")` または `(NEAR(comfort*, comfortable), 5)`などの重複する語句は指定できます。 重複する語句を指定すると、一致する可能性がある順列が増えることでクエリの複雑さが増大します。 このような重複する語句を多数指定するとリソースが不足し、クエリが失敗することがあります。 この現象が発生する場合は、クエリを簡略化してもう一度やり直してください。  
  
-   NEAR (指定した最大距離に関係なく) は、語句間の絶対的な距離ではなく論理的な距離を示します。 たとえば、段落内の別の語句や文に含まれている語は、同じ語句や文に含まれている語に比べて関連度が低いと想定されるため、実際の近接度に関係なく、より離れているものとして扱われます。 同様に、別の段落にある語は、さらに離れているものとして扱われます。 一致する語句が、文、段落、または章の末尾にまで及ぶ場合、ドキュメントの順位付けに使用される間隔は、それぞれ 8、128、または 1024 ずつ増加します。  
  
-   CONTAINSTABLE 関数による順位付けへの近接語句の影響  
  
    NEAR を CONTAINSTABLE 関数で使用する場合は、ドキュメント内のその長さに関連する一致数と、各一致における最初の検索語句と最後の検索語句の間の距離が、各ドキュメントの順位付けに影響します。 汎用近接語句では、たとえば、一致する検索語間の距離が 50 論理語より大きい場合、そのドキュメントについて返される順位は 0 になります。 最大距離として整数を指定しないカスタム近接語句では、間隔が 100 論理語より大きい一致のみを含むドキュメントは、順位 0 を取得します。 カスタム近接語句の順位付けの詳細については、「[RANK を使用して検索結果を制限する方法](../../relational-databases/search/limit-search-results-with-rank.md)」を参照してください。  
  
-   **transform noise words** サーバー オプション  
  
     **transform noise words[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の値は、ストップワードが近接検索で指定されている場合、** がストップワードを処理する方法に影響を与えます。 詳細については、「 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)」を参照してください。   
  
## <a name="see-also"></a>参照  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
