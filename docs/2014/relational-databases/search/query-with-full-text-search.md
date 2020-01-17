---
title: フルテキスト検索でのクエリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 280f4bc3c20fb65be24ace423f69982ad96bfbff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011109"
---
# <a name="query-with-full-text-search"></a>フルテキスト検索でのクエリ
  フルテキスト検索を定義するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト クエリでは、フルテキスト述語 (CONTAINS と FREETEXT) およびフルテキスト関数 (CONTAINSTABLE と FREETEXTTABLE) が使用されます。 この述語と関数は、さまざまな形式のクエリ用語に対応する豊富な [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文をサポートします。 フルテキスト クエリを記述するには、これらの述語と関数をいつどのように使用するかを理解する必要があります。  
  
##  <a name="OV_ft_predicates"></a> 概要、フルテキストの述語 (CONTAINS と FREETEXT)  
 CONTAINS 述語と FREETEXT 述語は、TRUE 値または FALSE 値を返します。 これらの述語は、特定の行がフルテキスト クエリと一致するかどうかを判断する選択基準としてのみ使用します。 一致する行は結果セットで返されます。 CONTAINS と FREETEXT は、SELECT ステートメントの WHERE 句または HAVING 句で指定します。 これらの述語は、LIKE や BETWEEN など他の [!INCLUDE[tsql](../../includes/tsql-md.md)] 述語と組み合わせて使用できます。  
  
> [!NOTE]  
>  これらの述語の引数と構文については、次を参照してください。 [CONTAINS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/contains-transact-sql)と[FREETEXT &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)します。  
  
 CONTAINS または FREETEXT を使用する場合は、検索するテーブルの単一の列、一連の列、すべての列のいずれかを指定できます。 また、フルテキスト クエリで単語区切りとステミング、類義語辞典の検索、およびノイズ ワードの削除を行うために使用される言語リソースの言語を指定することもできます。  
  
 CONTAINS と FREETEXT は、次のようにさまざまな検索で利用できます。  
  
-   CONTAINS (または CONTAINSTABLE) は、単語または語句との完全一致検索やあいまい一致検索、特定の範囲内での近接検索、または重み付き検索に使用します。 CONTAINS を使用する場合は、検索するテキストを指定する検索条件を少なくとも 1 つ指定し、一致を判断する条件を指定する必要があります。  
  
     検索条件の間には論理演算を使用できます。 詳細については、次を参照してください。[ブール演算子の AND、OR、AND NOT (CONTAINS と CONTAINSTABLE) で](#Using_Boolean_Operators)、このトピックで後述します。  
  
-   FREETEXT (または FREETEXTTABLE) は、指定した単語、語句、または文章 ( *freetext 文字列*) の正確な文字列の並びではなく、意味を照合する場合に使用します。 指定した列のフルテキスト インデックスに、用語または一定の形式の用語が見つかった場合は、一致すると判断されます。  
  
 この作業を終えると、CONTAINS または FREETEXT 述語に 4 つの要素で構成される名前を使用して、リンク サーバー上の対象のテーブルのフルテキスト インデックス列にクエリを実行できます。 フルテキスト クエリを受け取るようリモート サーバーを準備するには、リモート サーバー上の検索対象のテーブルおよび列にフルテキスト インデックスを作成し、リモート サーバーをリンク サーバーとして追加します。  
  
> [!NOTE]  
>  データベースの互換性レベルが 100 に設定されている場合、 [OUTPUT 句](/sql/t-sql/queries/output-clause-transact-sql) でフルテキスト述語を使用することはできません。  
  
 
  
### <a name="examples"></a>使用例  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. CONTAINS を <simple_term> と共に使用する  
 次の例では、`$80.99` という単語を含み、価格が `"Mountain"` であるすべての製品を検索します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>B. FREETEXT を使用して、指定した文字値を含む単語を検索する  
 次の例では、vital、safety、components に関連する単語を含むすべてのドキュメントを検索します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> フルテキスト関数 (CONTAINSTABLE と FREETEXTTABLE) の概要  
 CONTAINSTABLE 関数と FREETEXTTABLE 関数は、SELECT ステートメントの FROM 句で通常のテーブル名と同じように指定できます。 この関数では、フルテキスト クエリと一致する 0 行、1 行、または 2 行以上で構成されるテーブルが返されます。 返されたテーブルには、ベース テーブルの行のうち、関数のフルテキスト検索条件に指定した選択基準に一致する行のみが含まれます。  
  
> [!NOTE]  
>  これらの関数の引数と構文については、次を参照してください。 [CONTAINSTABLE &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/containstable-transact-sql)と[FREETEXTTABLE &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)します。  
  
 このいずれかの関数を使用するクエリでは、次のように、各行の関連順位値 (RANK) とフルテキスト キー (KEY) が取得されます。  
  
-   KEY 列  
  
     KEY 列には、返された行の一意の値が格納されます。 KEY 列は、選択基準を指定する際に使用できます。  
  
-   RANK 列  
  
     RANK 列は、各行が選択条件にどの程度一致しているかを示す *順位値* を返します。 行内のテキストまたはドキュメントの順位値が高いほど、指定したフルテキスト クエリとその行との関連性が高いことを示します。 複数の行に同じ順位が付けられる可能性もあるので注意してください。 *top_n_by_rank* パラメーター (省略可能) を指定して、返される一致の数を制限することもできます。 詳細については、「 [RANK を使用して検索結果を制限する方法](limit-search-results-with-rank.md)」を参照してください。  
  
 どちらの関数を使用する場合も、フルテキスト検索の対象となるベース テーブルを指定する必要があります。 述語と同様に、検索するテーブルの単一の列、一連の列、またはすべての列を指定できます。また、必要に応じて、指定したフルテキスト クエリで使用される言語リソースの言語を指定することもできます。  
  
 CONTAINSTABLE は CONTAINS と同様の検索に役立ち、FREETEXTTABLE は FREETEXT と同様の検索に役立ちます。 詳細については、このトピックの前の「 [フルテキスト述語 (CONTAINS と FREETEXT) の概要](#OV_ft_predicates)」を参照してください。 CONTAINSTABLE 関数と FREETEXTTABLE 関数を使用するクエリを実行する場合は、返された行を元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベース テーブルの行と明示的に結合する必要があります。  
  
 通常、CONTAINSTABLE または FREETEXTTABLE の結果をベース テーブルと結合します。 その場合、一意なキー列の名前を把握している必要があります。 この列は、フルテキスト処理に対応する各テーブルに含まれ、テーブルの行を一意にするために使用されます ("*一意なキー列*")。 詳細については、「 [フルテキスト インデックスの管理](../indexes/indexes.md)」をご覧ください。  
  
 
  
### <a name="examples"></a>使用例  
  
#### <a name="a-using-containstable"></a>A. CONTAINSTABLE を使用する  
 次の例では、 **Description** 列の "light" または "lightweight" という語の近くに "aluminum" という語があるすべての製品の説明 ID と説明を返します。 また、順位値が 2 以上の行だけを返します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>B. FREETEXTTABLE を使用する  
 次の例では、FREETEXTTABLE クエリを拡張して、順位の高いものから順に行を返し、各行の順位を選択リストに追加します。 を、クエリを指定するを確認する必要があります**ProductDescriptionID**の一意のキー列には、`ProductDescription`テーブル。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 以下に、同じクエリを拡張して、順位の値が 10 以上の行だけを返す例を示します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 
  
##  <a name="Using_Boolean_Operators"></a> ブール演算子 - を使用して、OR、CONTAINS および CONTAINSTABLE ではなく、  
 CONTAINS 述語と CONTAINSTABLE 関数は、同じ検索条件を使用します。 ブール演算子を使用していくつかの検索語句を結合は両方ともサポート-AND、OR、および NOT の論理操作を実行します。 たとえば、AND を使用して "latte" と "New York-style bagel" の両方を含む行を検索できます。 また、AND NOT を使用して "bagel" を含み、かつ "cream cheese" を含まない行を検索することもできます。  
  
> [!NOTE]  
>  一方、FREETEXT と FREETEXTTABLE では、ブール演算子は検索対象の語として扱われます。  
  
 CONTAINS を、論理演算子 AND、OR、および NOT を使用する他の述語と組み合わせる方法については、「[検索条件 &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql)」を参照してください。  
  
### <a name="example"></a>例  
 次の例では、 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースの ProductDescription テーブルを使用します。 このクエリでは、CONTAINS 述語を使用して、説明 ID が 5 以外で、説明に "Aluminum" と "spindle" という両方の単語が含まれている説明を検索します。 検索条件では、AND ブール演算子を使用します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> フルテキスト クエリの追加の考慮事項  
 フルテキスト クエリを記述する場合は、次の点も考慮してください。  
  
-   LANGUAGE オプション  
  
     クエリ用語の多くは、ワード ブレーカーの動作に大きく依存します。 適切なワード ブレーカー (およびステミング機能) および類義語辞典ファイルを使用するために、LANGUAGE オプションを指定することをお勧めします。 詳細については、「 [フルテキスト インデックス作成時の言語の選択](choose-a-language-when-creating-a-full-text-index.md)」を参照してください。  
  
-   ストップワード  
  
     フルテキスト クエリを定義する際に、Full-Text Engine でストップワード (ノイズ ワードとも呼ばれます) が検索基準から除外されます。 ストップワードとは、"a"、"and"、"is"、"the" などの頻出する単語で、特定のテキストの検索には通常役立ちません。 ストップワードはストップリストに列挙されています。 各フルテキスト インデックスには特定のストップリストが関連付けられ、それによってクエリから、またはインデックス作成時にインデックスから除外されるストップワードが決まります。 詳細については、「 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](full-text-search.md)」を参照してください。  
  
-   類義語辞典  
  
     FREETEXT クエリと FREETEXTTABLE クエリでは、類義語辞典を既定で使用します。 CONTAINS と CONTAINSTABLE では、省略可能な THESAURUS 引数をサポートしています。  
  
-   大文字と小文字の区別  
  
     フルテキスト検索クエリでは大文字と小文字は区別されません。 ただし、日本語の場合は、同じ発音を複数の方法で表記できます。この表記方法を正規化することは、大文字と小文字の区別をなくすことに似ています。たとえば、「かな」で検索することで、大文字小文字を区別しない検索に近い検索を実現できます。 しかし、このような正規化はサポートされていません。  
  

  
##  <a name="varbinary"></a> Varbinary (max) 列および xml 列にクエリを実行します。  
 `varbinary(max)` 列、`varbinary` 列、または `xml` 列にフルテキスト インデックスが設定されている場合は、他のフルテキスト インデックス列と同様に、フルテキスト述語 (CONTAINS および FREETEXT) とフルテキスト関数 (CONTAINSTABLE および FREETEXTTABLE) を使用して、これらの列に対するクエリを実行できます。  
  
> [!IMPORTANT]  
>  フルテキスト検索は image 列に対しても実行できます。 ただし、`image` データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは削除される予定です。 新規の開発作業ではこのデータ型を使用せず、現在このデータ型を使用しているアプリケーションの変更を検討してください。 代わりに、`varbinary(max)` データ型を使用してください。  
  
### <a name="varbinarymax-or-varbinary-data"></a>varbinary(max) データまたは varbinary データ  
 単一の `varbinary(max)` 列または `varbinary` 列に、さまざまな型のドキュメントを格納できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、専用のフィルターがオペレーティング システムにインストールされ、使用できるようになっている任意のドキュメント型がサポートされます。 各ドキュメントのドキュメント型は、ドキュメントのファイル拡張子によって識別されます。 たとえば、ファイル拡張子が .doc である場合、フルテキスト検索では、Microsoft Word ドキュメントをサポートするフィルターが使用されます。 使用可能なドキュメント型の一覧を確認するには、 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) カタログ ビューに対してクエリを実行してください。  
  
 Full-Text Engine では、オペレーティング システムにインストールされている既存のフィルターを利用できます。 オペレーティング システムのフィルター、ワード ブレーカー、およびステミング機能を使用する前に、次のコードを実行してこれらのリソースをサーバー インスタンスに読み込む必要があります。  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 `varbinary(max)` 列にフルテキスト インデックスを作成するには、Full-Text Engine が `varbinary(max)` 列にあるドキュメントのファイル拡張子にアクセスする必要があります。 この情報は、型列と呼ばれるテーブル列に格納されている必要があります。型列は、フルテキスト インデックスの `varbinary(max)` 列に関連付けられている必要があります。 Full-Text Engine は、ドキュメントにインデックスを作成する際に、型列のファイル拡張子を参照して、使用するフィルターを特定します。  
  
 
  
### <a name="xml-data"></a>xml データ  
 `xml` データ型の列には、XML ドキュメントと XML フラグメントのみが格納されます。XML ドキュメントには XML フィルターのみが使用されるため、 型列は必要ありません。 `xml` 列では、フルテキスト インデックスによって XML 要素のコンテンツにインデックスが設定されますが、XML マークアップは無視されます。 属性値には、数値でない限り、フルテキスト インデックスが設定されます。 要素タグはトークンの境界として使用されます。 複数言語を含む整形式の XML または HTML ドキュメントやフラグメントはサポートされます。  
  
 に対するクエリの実行の詳細については、`xml`列を参照してください[XML 列でフルテキスト検索の使用](../xml/use-full-text-search-with-xml-columns.md)します。  
  
 
  
##  <a name="supported"></a> サポートされるクエリ用語の形式  
 このセクションでは、フルテキスト述語および行セット値関数による各クエリ形式のサポートの概要について説明します。  
  
> [!NOTE]  
>  指定したクエリ語句の構文については、次の表の **Supported by** 列の対応するリンクをクリックしてください。  
  
|クエリ用語の形式|説明|Supported by|  
|----------------------|-----------------|------------------|  
|1 つ以上の語または句 (*単純語句*)|フルテキスト検索において、語 (または *トークン*) とは、指定された言語の規則に従って適切なワード ブレーカーによって境界が識別された文字列です。 有効な句は、複数の語から構成されます。句読点を含む場合も含まない場合もあります。<br /><br /> たとえば、「クロワッサン」は、word、および"カフェ?? オーストラリア lait"は、語句です。 このような語や句は単純語句と呼ばれています。<br /><br /> 詳細については、このトピックの後の「 [特定の語または句 (単純語句) の検索](#Simple_Term)」を参照してください。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) は、句に完全一致するものを検索します。<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) および [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) は、句を個々の語に分解します。|  
|指定した文字列で始まる語または句 (*プレフィックス語句*)|プレフィックス語句とは、派生語または変化形を生成するために語の前に付けられる文字列です。<br /><br /> 1 つのプレフィックス語句の場合、指定したプレフィックス語句で始まるすべての語が、結果セットに含まれます。 たとえば、"auto*" は、"automatic"、"automobile" などに一致します。<br /><br /> 句の場合、句を構成する各語がプレフィックス語句と見なされます。 たとえば、"auto tran\*" は "automatic transmission" や "automobile transducer" に一致しますが、"automatic motor transmission" には一致しません。<br /><br /> 詳細については、このトピックの後の「 [プレフィックス検索 (プレフィックス語句) の実行](#Prefix_Term)」を参照してください。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|特定の単語の変化形 (*用語変化形生成*)|変化形は、動詞のさまざまな時制および活用、または名詞の単数形と複数形です。 たとえば、"drive" という語の変化形を検索します。 テーブルのさまざまな行に、"drive"、"drives"、"drove"、"driving"、および "driven" が含まれている場合、これらはどれも drive という語から変化して生成されているので結果セットに入ります。<br /><br /> 詳細については、このトピックの後の「 [特定の語の変化形 (生成語) の検索](#Inflectional_Generation_Term)」を参照してください。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) および [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) は、指定されたすべての語の変化形の語句を既定で検索します。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) は、省略可能な INFLECTIONAL 引数をサポートしています。|  
|特定の単語のシノニム形 (*生成の用語の類義語辞典*)|類義語辞典は、ユーザー指定の用語のシノニムを定義します。 たとえば、エントリ "{car, automobile, truck, van}" が類義語辞典に追加されると、"car" という語の類義語形式を検索できます。 "automobile"、"truck"、"van"、または "car" という語は、"car" という語を含むシノニムの拡張セットに属しているため、クエリ処理されるテーブルの行のうち、これらのいずれかの語を含むすべての行が結果セットに表示されます。<br /><br /> 類義語辞典ファイルの構造の詳細については、「 [フルテキスト検索に使用する類義語辞典ファイルの構成と管理](configure-and-manage-thesaurus-files-for-full-text-search.md)」を参照してください。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) と [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) は、類義語辞典を既定で使用します。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) は、省略可能な THESAURUS 引数をサポートしています。|  
|他の語または句に近接する語または句 (*近接語句*)|近接語句とは、互いに近接する語または句を表します。最初の検索語句と最後の検索語句を分離する非検索用語の最大数を指定することもできます。 さらに、任意の順序で語や句を検索したり、指定した順序で語や句を検索したりすることができます。<br /><br /> たとえば、"ice" という語の近くに "hockey" という語がある行や、"ice skating" という句の近くに "ice hockey" という句がある行を検索できます。<br /><br /> 詳細については、「 [NEAR による他の単語の近くにある単語の検索](search-for-words-close-to-another-word-with-near.md)」を参照してください。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|重み付け値を使用している語または句 (*重み付け語句*)|一連の語句内における各語句の重要度を示す重み付け値です。 重み付け値 0.0 は最低値であり、重み付け値 1.0 は最高値です。<br /><br /> たとえば、複数の語句を検索するクエリでは、検索条件の各検索語に、他の語との相対的な重要性を示す重み付け値を割り当てることができます。 この種のクエリ結果では、検索語に割り当てた相対的な重みに従って、最も関連性の高い行が最初に返されます。 結果セットには、指定した語句 (またはそれらの間のコンテンツ) のいずれかを含むドキュメントまたは行が含まれます。ただし、各検索語句に関連付けられている重み付け値の違いにより、一部の結果が他の結果より関連性が高いと見なされます。<br /><br /> 詳細については、このトピックの後の「 [重み付け値を使用する語または句 (重み付け語句) の検索](#Weighted_Term)」を参照してください。|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> 特定の語または句 (単純語句) の検索  
 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)、または [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) を使用すると、テーブルで特定の句を検索できます。 検索する場合など、`ProductReview`テーブルに、[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]次のように CONTAINS 述語を使用することで、"learning curve"という句を使用して、製品に関するすべてコメントを検索するデータベース。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 検索条件 (この場合は "learning curve") には、1 つ以上の語で構成される複雑な条件を指定できます。  
  
 
  
###  <a name="Prefix_Term"></a> プレフィックス検索 (プレフィックス語句) の実行  
 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) または [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) を使用すると、指定したプレフィックスを持つ語または句を検索することができます。 指定したプレフィックスで始まるテキストが含まれる列のすべてのエントリが返されます。 たとえば、 `top`というプレフィックス ( `top``ple`、 `top``ping`、 `top`など) が含まれるすべての行を検索する場合、 クエリは次のようになります。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 アスタリスク (*) より前のテキストに一致するすべてのテキストが返されます。 `CONTAINS (DESCRIPTION, 'top*')`のように、テキストとアスタリスクを二重引用符で囲まなかった場合、フルテキスト検索ではアスタリスクはワイルドカードとして認識されません。  
  
 プレフィックス語句が句の場合、句を構成する各トークンは、それぞれ独立したプレフィックス語句と見なされます。 それらのプレフィックス語句で始まる語を持つすべての行が返されます。 たとえば、"light bread*" というプレフィックス語句を使用すると、"light breaded"、"lightly breaded"、または "light bread" というテキストを含む行が検索されますが、"lightly toasted bread" は対象から除外されます。  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> 変化形 (生成語) の特定の単語の検索  
 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)、または [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) を使用すると、動詞のさまざまな時制および活用、または名詞の単数形と複数形 (変化形検索)、または特定の語のシノニム形 (類義語辞典検索) を検索できます。  
  
 次の例は `Comments` データベースの `ProductReview` テーブルの `AdventureWorks` 列にある "foot" のすべての語形 ("foot"、"feet" など) を検索します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  フルテキスト検索では、動詞のさまざまな時制および活用または名詞の単数形と複数形の検索を可能にするステマーが使用されます。 ステマーの詳細については、「 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md)」を参照してください。  
  

  
###  <a name="Weighted_Term"></a> 重み付け値 (重み付け語句) の語または句を使用して検索  
 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) を使用すると、重み付け値を指定して語または句を検索することができます。 重みは 0.0 ～ 1.0 の数値で指定し、一連の語句内における各語句の重要度を示します。 重み 0.0 は最低値であり、重み 1.0 は最高値です。  
  
 次の例のクエリは、重みを使用して、文字列 "Bay" で始まるテキストに "Street" または "View" が含まれる顧客住所をすべて検索します。 結果では、指定した語が多く含まれている行ほど高い順位が付けられます。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 重み付け語句は、単純語句、プレフィックス語句、生成語、または近接語句と組み合わせて使用できます。  
  

  
##  <a name="tokens"></a> ワード ブレーカー、類義語辞典、およびストップ リストの組み合わせのトークン化の結果を表示します。  
 特定のワード ブレーカー、類義語辞典、ストップリストの組み合わせをクエリ文字列入力に適用した後に、**sys.dm_fts_parser** 動的管理ビューを使用すると、トークン化の結果を確認できます。 詳細については、「[sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)」を参照してください。  
  
 
  
## <a name="see-also"></a>参照  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [フルテキスト検索クエリの作成 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [フルテキスト クエリのパフォーマンスの向上](improve-the-performance-of-full-text-queries.md)  
  
  
