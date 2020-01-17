---
title: CONTAINS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- CONTAINS predicate (Transact-SQL)
- conditions [SQL Server], CONTAINS
- fuzzy (less precise) word or phrase search [full-text search]
- word weighting values [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- LANGUAGE option
- word inflectionally generated from another [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- word near another word search [full-text search]
- full-text search [SQL Server], searching on a property
- proximity searches [full-text search]
- less precise (fuzzy) searches [full-text search]
- property searching [SQL Server], searching on a property
- inflectional forms [full-text search]
- prefix searches [full-text search]
ms.assetid: 996c72fc-b1ab-4c96-bd12-946be9c18f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 613dc7c05707d9a432ec6f8f7eab7b8b3bce2cce
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982832"
---
# <a name="contains-transact-sql"></a>CONTAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、単語または語句との完全一致検索やあいまい一致検索、特定の範囲内での検索、または重み付き検索を行います。 CONTAINS は [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントの [WHERE 句](../../t-sql/queries/where-transact-sql.md)で使用される述語です。文字ベースのデータ型を含むフルテキスト インデックス列で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索を実行します。  
  
 次に CONTAINS の検索対象を示します。  
  
-   単語または語句。  
  
-   単語または語句のプレフィックス。  
  
-   別の単語の近くにある単語。  
  
-   他の単語を語形変化して生成された単語。たとえば、drive という単語からは、drives、drove、driving、driven などの単語が生成されます。  
  
-   シソーラスで別の単語のシノニムになっている単語。たとえば、"金属" という単語には、"アルミニウム" や "スチール" などのシノニムがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているフルテキスト検索の形式については、「[フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」を参照してください。  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CONTAINS (   
     {   
        column_name | ( column_list )   
      | *   
      | PROPERTY ( { column_name }, 'property_name' )    
     }   
     , '<contains_search_condition>'  
     [ , LANGUAGE language_term ]  
   )   
  
<contains_search_condition> ::=   
  {   
      <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    | <weighted_term>   
    }   
  |   
    { ( <contains_search_condition> )   
        [ { <AND> | <AND NOT> | <OR> } ]   
        <contains_search_condition> [ ...n ]   
  }   
<simple_term> ::=   
     { word | "phrase" }  
  
<prefix term> ::=   
  { "word*" | "phrase*" }  
  
<generation_term> ::=   
  FORMSOF ( { INFLECTIONAL | THESAURUS } , <simple_term> [ ,...n ] )   
  
<generic_proximity_term> ::=   
  { <simple_term> | <prefix_term> } { { { NEAR | ~ }   
     { <simple_term> | <prefix_term> } } [ ...n ] }  
  
<custom_proximity_term> ::=   
  NEAR (   
     {  
        { <simple_term> | <prefix_term> } [ ,...n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,...n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
  ISABOUT   
   ( {   
        {   
          <simple_term>   
        | <prefix_term>   
        | <generation_term>   
        | <proximity_term>   
        }   
      [ WEIGHT ( weight_value ) ]   
      } [ ,...n ]   
   )   
  
<AND> ::=   
  { AND | & }  
  
<AND NOT> ::=   
  { AND NOT | &! }  
  
<OR> ::=   
  { OR | | }  
  
```  
  
## <a name="arguments"></a>引数  
 *column_name*  
 FROM 句で指定されたテーブルのフルテキスト インデックス付き列の名前を指定します。 列には、**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary**、**varbinary(max)** のいずれかの型を指定できます。  
  
 *column_list*  
 複数の列をコンマで区切って指定します。 *column_list* は、かっこで囲む必要があります。 *language_term* を指定しない場合、*column_list* で指定するすべての列の言語は同じにする必要があります。  
  
 \*  
 検索条件の FROM 句で指定したテーブルのすべてのフルテキスト インデックス付きの列が検索対象になります。 CONTAINS 句内の列は、フルテキスト インデックスがある単一テーブルから取得する必要があります。 *language_term* を指定しない場合、テーブルのすべての列の言語は同じである必要があります。  
  
 PROPERTY ( *column_name* , '*property_name*')  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。 
  
 指定した検索条件を検索するドキュメント プロパティを指定します。  
  
> [!IMPORTANT]  
>  行を返すクエリの場合、フルテキスト インデックスの検索プロパティ リストで *property_name* を指定し、フルテキスト インデックスに *property_name* のプロパティに固有のエントリを含める必要があります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。  
  
 LANGUAGE *language_term*  
 クエリにおいて、単語区切り、語幹検索、類義語の拡張と置換、およびノイズ語 ([ストップワード](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) の破棄を行うときに使用する言語を指定します。 このパラメーターはオプションです。  
  
 1 つの列に複数の異なる言語のドキュメントが BLOB (Binary Large Object) として格納されている場合、インデックスの作成に使用される言語は、各ドキュメントのロケール識別子 (LCID) によって決まります。 そのような列に対してクエリを実行する場合は、LANGUAGE *language_term* を指定すると検索結果の一致率が高まります。  
  
 *language_term* には、言語の LCID に対応する文字列、整数、または 16 進数の値を指定できます。 *language_term* を指定した場合、その言語は検索条件のすべての要素に適用されます。 値を指定しなかった場合は、列のフルテキストの言語が使用されます。  
  
 *language_term* を文字列で指定する場合は、[sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 互換性ビューの **alias** 列の値と同じ値を指定します。 文字列の場合は、'*language_term*' のように引用符 (') で囲む必要があります。 *language_term* を整数で指定する場合は、その言語を表す実際の LCID を指定します。 *language_term* を 16 進数の値で指定する場合は、「0x」の後に LCID の 16 進数の値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。  
  
 値を 2 バイト文字セット (DBCS) の形式で指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で Unicode に変換されます。  
  
 指定した言語が無効であるか、その言語に該当するリソースがインストールされていない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によりエラーが返されます。 ニュートラル言語リソースを使用するには、*language_term* に「0x0」を指定してください。  
  
 \<*contains_search_condition*>  
 *column_name* で検索するテキストと、その一致条件を指定します。  
  
*\<contains_search_condition>* is **nvarchar**. 入力に他の文字データ型が使用された場合は、暗黙の変換が行われます。 大きな文字列データ型 nvarchar (max) および varchar (max) は使用できません。 次の例では、`CONTAINS` 述語において、`varchar(30)` として定義されている変数 `@SearchWord` が暗黙に変換されます。
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 変換では "パラメーターを見つけ出す" 動作が機能しないため、パフォーマンスの向上を目的とする場合には **nvarchar** を使用してください。 次の例では、`@SearchWord` を `nvarchar(30)` として宣言しています。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 最適化されていないプランが生成される場合には、OPTIMIZE FOR クエリ ヒントを使用することもできます。  
  
 *word*  
 スペースまたは句読点なしの文字列を指定します。  
  
 *phrase*  
 単語間をスペースで区切った 1 つ以上の語を指定します。  
  
> [!NOTE]  
>  アジアの一部の言語などのフレーズでは、語句を構成するときに単語間にスペースを挿入しないものがあります。  
  
\<simple_term>  
単語または語句に対する完全一致を指定します。 有効な単純語の例には、"blue berry"、blueberry、および "Microsoft SQL Server" などがあります。 語句は二重引用符 ("") で囲みます。 語句内の単語は、 *\<contains_search_condition>* の指定と同じ順序で、データベース列に含まれている必要があります。 単語または語句内の文字の検索では、大文字と小文字は区別されません。 フルテキスト インデックス化された列の a、and、the などのノイズ ワード ([ストップワード](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) は、フルテキスト インデックスには格納されません。 1 つの単語の検索にノイズ ワードを使用した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではクエリにノイズ ワードだけが指定されていることを示すエラーが返されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスのディレクトリ \Mssql\Binn\FTERef にノイズ ワードの標準リストがあります。  
  
 句読点は無視されます。 したがって、`CONTAINS(testing, "computer failure")` は、"Where is my computer? Failure to find it would be expensive." がある行に一致します。 ワード ブレーカーの動作の詳細については、「[検索用のワード ブレーカーとステミング機能の構成と管理](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)」を参照してください。  
  
 \<prefix_term>  
 指定のテキストで始まる単語または語句の一致を指定します。 プレフィックス語句を二重引用符 ("") で囲み、後ろの二重引用符の前にアスタリスク (\*) を挿入すると、アスタリスクの前に指定された文字列で始まるすべてのテキストが照合されます。 句は、`CONTAINS (column, '"text*"')` のように指定してください。 アスタリスクは、一致する文字がないか、1 つまたはそれ以上の文字に一致します。その単語または語句を語根とする文字も対象になります。 テキストとアスタリスクが二重引用符で区切られていないと、述語が読み取る内容は `CONTAINS (column, 'text*')` となり、フルテキスト検索でアスタリスクが文字と見なされ、`text*` への完全一致が検索されます。 単語区切りでは通常このような文字は無視されるため、アスタリスク (\*) 文字が付いた文字はフルテキスト エンジンによって検索されません。  
  
 *\<prefix_term>* が語句のときは、語句に含まれるそれぞれの単語が独立したプレフィックスと見なされます。 したがって、"local wine *" というプレフィックスを指定しているクエリでは、"local winery"、"locally wined and dined"などの行が一致します。  
  
 \<generation_term>  
 指定されている原形の語または語句が、検索対象である元の単語の変形を含んでいる場合に、これらの単語も照合の対象であることを指定します。  
  
 INFLECTIONAL  
 言語依存の語幹検索が、指定した単純語に対して使用されます。 語幹検索の動作は、各言語の語幹ルールに基づいて定義されています。 ニュートラル言語には、関連する語幹検索がありません。 クエリの対象となっている列の列言語は、必要な語幹検索を参照する場合に使用されます。 *language_term* が指定されると、その言語に対応する語幹検索が使用されます。  
  
 *\<generation_term>* 内に指定された *\<simple_term>* は、名詞と動詞のどちらにも一致しません。  
  
 THESAURUS  
 列のフルテキスト言語に対応する類義語、またはクエリで指定された言語が使用されます。 *\<simple_term>* の最も長いパターンが類義語と照合され、追加の用語が生成されて、元のパターンを拡張するか置き換えます。 *\<simple_term>* の全体または一部に対して一致が見られない場合、一致しない部分が *simple_term* として処理されます。 フルテキスト検索の類義語の詳細については、「[フルテキスト検索に使用する類義語辞典ファイルの構成と管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)」を参照してください。  
  
 \<generic_proximity_term>  
 検索対象のドキュメントに含まれている必要がある単語または語句の照合を指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] \<custom_proximity_term>を使用することをお勧めします。  
  
 NEAR | ~  
 一致が返されるには、NEAR (~) 演算子の両側の単語または語句がドキュメントに含まれている必要があります。 検索語句は 2 つ指定する必要があります。 検索語句には、二重引用符で区切られた 1 つの単語または語句を指定できます ("*語句*")。  
  
 `a NEAR b NEAR c` または `a ~ b ~ c` のように、複数の近接語句をつないで指定できます。 一致が返されるためには、指定したすべての近接語句がドキュメントに含まれている必要があります。  
  
 たとえば、`CONTAINS(*column_name*, 'fox NEAR chicken')` と `CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')` では、どちらの場合も、指定した列について "fox" と "chicken" の両方を含むドキュメントが返されますが、 CONTAINSTABLE ではさらに、"fox" と "chicken" の近接度に基づく各ドキュメントのランクも返されます。 たとえば、"The fox ate the chicken" という文が含まれているドキュメントのランクは高くなります。これは、他のドキュメントよりも語句が近接しているためです。  
  
 汎用近接語句の詳細については、「[NEAR による他の単語の近くにある単語の検索](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)」を参照してください。  
  
 \<custom_proximity_term>  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。
  
 一致させる単語または語句と、必要に応じて検索語句間の許容最大距離を指定します。 また、検索語句を指定したとおりの順序で検索するように指定することもできます (\<match_order>)。  
  
 検索語句には、二重引用符で区切られた 1 つの単語または語句を指定できます ("*語句*")。 一致が返されるためには、指定したすべての語句がドキュメントに含まれている必要があります。 2 つ以上の検索語句を指定する必要があります。 検索語句の最大数は 64 です。  
  
 カスタム近接語句の場合、既定では、語句の間の距離やその順序に関係なく、指定した語句が含まれているすべての行が返されます。 たとえば、次のクエリと一致するには、`term1` と "`term3 term4`" が任意の場所に任意の順序でドキュメントに含まれているだけで十分です。  
  
```  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 省略可能なパラメーターは次のとおりです。  
  
 \<maximum_distance>  
 文字列と一致すると見なされるための、その文字列の先頭と末尾にある検索語句間の許容最大距離を指定します。  
  
 *integer*  
 0 から 4294967295 の正の整数を指定します。 この値により、指定した他の検索用語を除く最初と最後の検索語句間にある非検索語句の数を制御できます。  
  
 たとえば、次のクエリでは、最大距離が 5 語以内で `AA` と `BB` を任意の順序で検索します。  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 文字列 `AA one two three four five BB` と一致します。 次の例のクエリでは、最大距離が 5 語以内で `AA`、`BB`、および `CC` の 3 つの検索語句を指定しています。  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 このクエリでは、総距離が 5 語の次の文字列と一致します。  
  
 `BB   one two   CC   three four five A  A`  
  
 間に含まれている検索語句の `CC` はカウントされないことに注意してください。  
  
 **MAX**  
 距離に関係なく、指定した語句が含まれているすべての行を返します。 これは既定値です。  
  
 \<match_order>  
 検索クエリによって返されるためには、語句が指定した順序で含まれている必要があるかどうかを指定します。 \<match_order> を指定するには、\<maximum_distance> も指定する必要があります。  
  
 \<match_order> には、次のいずれかの値を指定します。  
  
 **TRUE**  
 語句の指定した順序が適用されます。 たとえば、`NEAR(A,B)` は、`A ... B` とだけ一致します。  
  
 **FALSE**  
 指定した順序を無視します。 たとえば、`NEAR(A,B)` は、`A ... B` と `B ... A` の両方と一致します。  
  
 これは既定値です。  
  
 たとえば、次の近接語句では、距離に関係なく、"`Monday`"、"`Tuesday`"、および "`Wednesday`" という単語を指定した順序で検索します。  
  
```  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 カスタム近接語句の使用方法の詳細については、「[NEAR による他の単語の近くにある単語の検索](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)」を参照してください。  
  
 \<weighted_term>  
 クエリによって取得された一致する行と、単語または語句のリストが照合されます。このリストの単語や語句のそれぞれには、オプションで重み付け値が指定されます。  
  
 ISABOUT  
 *\<weighted_term>* キーワードを指定します。  
  
 WEIGHT(*weight_value*)  
 0\.0 から 1.0 の間で重み値を指定します。 *\<weighted_term>* 内の各コンポーネントには、*weight_value* を含めることができます。 *weight_value* は、クエリのさまざまな部分に影響を与える、クエリに一致する各行に割り当てられる順位値を変更することです。 WEIGHT は CONTAINS クエリの結果に影響しませんが、WEIGHT は [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) クエリ内のランクに影響します。  
  
> [!NOTE]  
>  小数点区切り文字は、オペレーティング システムのロケールにかかわらず常にピリオドです。  
  
 { AND | & } | { AND NOT | &! } | { OR | | }  
 2 つの contains 検索条件の間の論理演算を指定します。  
  
 { AND | & }  
 一致条件として、2 つの contains 検索条件を満たすことを指定します。 アンパサンド記号 (&) は、AND キーワードの代わりに使用して、AND 演算子を表すことができます。  
  
 { AND NOT | &! }  
 2 番目の検索条件が存在しないことを、一致条件として指定します。 アンパサンドとその次の感嘆符 (&!) は、AND NOT キーワードの代わりに使用して、AND NOT 演算子を表すことができます。  
  
 { OR | | }  
 一致条件として、2 つの contains 検索条件のいずれかを満たすことを指定します。 垂直バー記号 (|) は、OR キーワードの代わりに使用して、OR 演算子を表すことができます。  
  
 *\<contains_search_condition>* 内にかっこで囲まれたグループが含まれる場合は、かっこで囲まれたグループが最初に評価されます。 かっこで囲まれたグループを評価した後は、contains 検索条件で使用される論理演算子に対して次の規則が適用されます。  
  
-   NOT は AND より先に適用されます。  
  
-   NOT は AND NOT のように、AND の後にだけ指定できます。 OR NOT 演算子は使用できません。 NOT は最初の条件の前に指定できません。 たとえば、`CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )` は無効になります。  
  
-   AND は OR より先に適用されます。  
  
-   同じタイプの論理演算子 (AND、OR) は結合されるので、任意の順番で適用できます。  
  
 *n*  
 複数の CONTAINS 検索条件と、条件内の複数の語を指定できることを示すプレースホルダーです。  
  
## <a name="general-remarks"></a>全般的な解説  
 フルテキストの述語と関数の対象は、FROM 述語で示される 1 つのテーブルです。 複数のテーブルを検索するには、FROM 句で結合テーブルを使用して、複数のテーブルが組み合わされた結果セットを検索します。  
  
 データベースの互換性レベルが 100 に設定されている場合、[OUTPUT 句](../../t-sql/queries/output-clause-transact-sql.md) でフルテキスト述語を使用することはできません。  
  
## <a name="querying-remote-servers"></a>リモート サーバーのクエリ  
 この作業を終えると、CONTAINS または [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 述語に 4 つの要素で構成される名前を使用して、リンク サーバー上の対象のテーブルのフルテキスト インデックス列にクエリを実行できます。 フルテキスト クエリを受け取るようリモート サーバーを準備するには、リモート サーバー上の検索対象のテーブルおよび列にフルテキスト インデックスを作成し、リモート サーバーをリンク サーバーとして追加します。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE とフルテキスト検索の比較  
 フルテキスト検索とは異なり、[LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 述語は、文字パターンにのみで動作します。 また、フォーマットされたバイナリ データのクエリには LIKE 述語を使用できません。 さらに、構造化されていない大量のテキスト データに対して LIKE クエリを実行すると、同じデータに対して同等のフルテキスト検索を実行する場合に比べてはるかに時間がかかります。 数百万行のテキスト データに対して LIKE クエリを実行すると、結果が得られるまでに数分かかる場合があります。一方、同じデータに対してフルテキスト クエリを実行すると、返される行数とサイズにもよりますが、数秒以内で結果を取得できます。 もう 1 つの注意事項は、LIKE ではテーブル全体の単純なパターンのスキャンしか実行されないことです。 これに対し、フルテキスト クエリでは、言語が識別され、インデックスの作成時やクエリの実行時に、ストップワードのフィルター処理、類義語辞典と変化形の拡張の作成など、特定の変換が適用されます。 これらの変換により、フルテキスト クエリの再呼び出しの精度および結果の最終的なランク付けを向上させることができます。  
  
## <a name="querying-multiple-columns-full-text-search"></a>複数列のクエリ (フルテキスト検索)  
 検索する列のリストを指定することで、複数の列に対してクエリを実行できます。 クエリを実行する列は同じテーブルに含まれている必要があります。  
  
 たとえば、次の CONTAINS クエリでは、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースの `Production.Product` テーブルの `Name` 列と `Color` 列内で、`Red` という語句を検索します。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-contains-with-simple_term"></a>A. CONTAINS を \<simple_term> と共に使用する  
 次の例では、 `Mountain` という単語を含み、価格が `$80.99` であるすべての製品を検索します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain');  
GO  
```  
  
### <a name="b-using-contains-and-phrase-with-simple_term"></a>B. CONTAINS と語句を \<simple_term> と共に使用する  
 次の例では、`Mountain` または `Road` のいずれかの語句が含まれている、すべての製品を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefix_term"></a>C. CONTAINS を \<prefix_term> と共に使用する  
 次の例では、`Name` 列の中で、chain というプレフィックスで始まる 1 つ以上の単語が含まれている、すべての製品名を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefix_term"></a>D. CONTAINS および OR を \<prefix_term> と共に使用する  
 次の例では、`chain` または `full` のいずれかのプレフィックスを持つ文字列が含まれている、すべてのカテゴリ説明を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximity_term"></a>E. CONTAINS を \<proximity_term> と共に使用する  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。 
  
 次の例では、`Production.ProductReview` テーブルを対象として、10 語以内の距離で `bike` と "`control`" という単語を含むすべてのコメントを、指定した順序 (つまり、"`bike`"、"`control`" の順) で検索します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generation_term"></a>F. CONTAINS を \<generation_term> と共に使用する  
 次の例では、`ride` を原型とする riding、ridden などの単語が含まれている、すべての製品を検索します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weighted_term"></a>G. CONTAINS を \<weighted_term> と共に使用する  
 次の例では、`performance`、`comfortable`、または `smooth` という単語を含むすべての製品名を検索します。各単語にはそれぞれ異なる重み付けが割り当てられています。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, 'ISABOUT (performance weight (.8),   
comfortable weight (.4), smooth weight (.2) )' );  
GO  
```  
  
### <a name="h-using-contains-with-variables"></a>H. CONTAINS を変数と共に使用する  
 次の例では、特定の検索語ではなく変数を使用します。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>I. CONTAINS を論理演算子 (AND) と共に使用する  
 次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの ProductDescription テーブルを使用します。 このクエリでは、CONTAINS 述語を使用して、説明 ID が 5 以外で、説明に `Aluminum` と `spindle` という両方の単語が含まれている説明を検索します。 検索条件では、AND ブール演算子を使用します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>J. CONTAINS を使用して行の挿入を確認する  
 次の例では、SELECT サブクエリ内で CONTAINS を使用します。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを使用して、クエリは特定の自転車の ProductReview テーブルですべてのコメントのコメント値を取得します。 検索条件では、AND ブール演算子を使用します。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.ProductReview   
  (ProductID, ReviewerName, EmailAddress, Rating, Comments)   
VALUES  
  (780, 'John Smith', 'john@fourthcoffee.com', 5,   
'The Mountain-200 Silver from AdventureWorks2008 Cycles meets and exceeds expectations. I enjoyed the smooth ride down the roads of Redmond');  
  
-- Given the full-text catalog for these tables is Adv_ft_ctlg,   
-- with change_tracking on so that the full-text indexes are updated automatically.  
WAITFOR DELAY '00:00:30';     
-- Wait 30 seconds to make sure that the full-text index gets updated.  
  
SELECT r.Comments, p.Name  
FROM Production.ProductReview AS r  
JOIN Production.Product AS p   
    ON r.ProductID = p.ProductID  
    AND r.ProductID = (SELECT ProductID  
FROM Production.ProductReview  
WHERE CONTAINS (Comments,   
    ' AdventureWorks2008 AND   
    Redmond AND   
    "Mountain-200 Silver" '));  
GO  
```  
  
### <a name="k-querying-on-a-document-property"></a>K. ドキュメント プロパティに対してクエリを実行する  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。 
  
 次のクエリでは、`Production.Document` テーブルの `Document` 列内で、インデックス化されたプロパティ `Title` を検索します。 このクエリは、`Title` または `Maintenance` という文字列が `Repair` プロパティに含まれているドキュメントのみを返します。  
  
> [!NOTE]  
>  プロパティ検索で行が返されるためには、インデックスの作成中に列を解析するフィルターによって、指定されたプロパティが抽出される必要があります。 また、指定されたテーブルのフルテキスト インデックスが、プロパティを含めるように構成されている必要があります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Document 
FROM Production.Document  
WHERE CONTAINS(PROPERTY(Document,'Title'), 'Maintenance OR Repair');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索の概要](../../relational-databases/search/get-started-with-full-text-search.md)   
 [フルテキスト カタログの作成と管理](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [フルテキスト検索クエリの作成 &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
