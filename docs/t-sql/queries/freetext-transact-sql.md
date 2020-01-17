---
title: FREETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREETEXT
- FREETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXT predicate (Transact-SQL)
- words in predicate [full-text search]
- column searches [full-text search]
ms.assetid: 2f199d3c-440e-4bcf-bdb5-82bb3994005d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3c0d1ed26fa58934a51ec051eb3aa4e1d5b9a2bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902104"
---
# <a name="freetext-transact-sql"></a>FREETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントの [!INCLUDE[tsql](../../includes/tsql-md.md)] [WHERE 句](../../t-sql/queries/where-transact-sql.md)で使用される述語です。文字ベースのデータ型を含むフルテキスト インデックス列で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索を実行します。 この述語は、検索条件の文字列の並びと正確に一致しなくても意味が合っている値を検索できます。 FREETEXT を使用すると、フルテキスト クエリ エンジンによって、*freetext_string* を基に次の内部操作が実行され、各語に重みが割り当てられた後、一致するものが検索されます。  
  
-   単語の区切りに基づいて、文字列を個々の単語に分割。  
  
-   単語の語尾変化形を生成 (語幹への分割)。  
  
-   類義語との一致に基づいて、語の拡張と置き換えの一覧を決定。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているフルテキスト検索の形式については、「[フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」を参照してください。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658))。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
FREETEXT ( { column_name | (column_list) | * }   
          , 'freetext_string' [ , LANGUAGE language_term ] )  
```  
  
## <a name="arguments"></a>引数  
 *column_name*  
 FROM 句で指定したテーブルのフルテキスト インデックス付きの列の名前を指定します。 列には、**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary**、**varbinary(max)** のいずれかの型を指定できます。  
  
 *column_list*  
 コンマ区切りで複数の列を指定できます。 *column_list* は、かっこで囲む必要があります。 *language_term* を指定しない場合、*column_list* で指定するすべての列の言語は同じにする必要があります。  
  
 \*  
 フルテキスト検索用に登録されているすべての列を使用して、指定した *freetext_string* を検索します。 FROM 句に複数のテーブルが指定されている場合は、テーブル名で \* を限定する必要があります。 *language_term* を指定しない場合、テーブルのすべての列の言語は同じである必要があります。  
  
 *freetext_string*  
 *column_name* で検索するテキストです。 単語、フレーズ、文など、あらゆるテキストを入力できます。 用語または一定の形式になっている用語がフルテキスト インデックス内に見つかった場合、一致するものと判断されます。  
  
 CONTAINS と CONTAINSTABLE の検索条件では AND はキーワードになりますが、*freetext_string* では 'and' はノイズ語 ([ストップワード](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) と見なされ、破棄されます。  
  
 WEIGHT、FORMSOF、ワイルドカード、NEAR、その他の構文は使用できません。 *freetext_string* は単語、語幹に分割され、類義語がチェックされて渡されます。  
  
 *freetext_string* は **nvarchar** です。 入力に他の文字データ型が使用された場合は、暗黙の変換が行われます。 大きな文字列データ型 nvarchar (max) および varchar (max) は使用できません。 次の例では、`FREETEXT` 述語において、`varchar(30)` として定義されている変数 `@SearchWord` が暗黙に変換されます。  
  
```sql  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 変換では "パラメーターを見つけ出す" 動作が機能しないため、パフォーマンスの向上を目的とする場合には **nvarchar** を使用してください。 次の例では、`@SearchWord` を `nvarchar(30)` として宣言しています。  
  
```sql  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 最適化されていないプランが生成される場合には、OPTIMIZE FOR クエリ ヒントを使用することもできます。  
  
 LANGUAGE *language_term*  
 クエリにおいて、単語区切り、語幹への分割、類義語のチェック、ストップワードの破棄を行うときに使用する言語リソースの言語を指定します。 このパラメーターは省略可能で、言語のロケール識別子 (LCID) に対応する文字列、整数、または 16 進数の値を指定できます。 *language_term* を指定した場合、その言語は検索条件のすべての要素に適用されます。 値を指定しなかった場合は、列のフルテキストの言語が使用されます。  
  
 1 つの列に言語の異なる複数のドキュメントが BLOB (Binary Large Object) として格納されている場合、そのインデックスの作成に使用される言語は、そのドキュメントのロケール識別子 (LCID) によって決まります。 そのような列に対してクエリを実行する場合は、LANGUAGE *language_term* を指定すると検索結果の一致率が高まります。  
  
 *language_term* を文字列で指定する場合は、[sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 互換性ビューの **alias** 列の値と同じ値を指定します。  文字列の場合は、'*language_term*' のように引用符 (') で囲む必要があります。 *language_term* を整数で指定する場合は、その言語を表す実際の LCID を指定します。 *language_term* を 16 進数の値で指定する場合は、「0x」の後に LCID の 16 進数の値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。  
  
 値を 2 バイト文字セット (DBCS) の形式で指定すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で Unicode に変換されます。  
  
 指定した言語が無効であるか、その言語に該当するリソースがインストールされていない場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によりエラーが返されます。 ニュートラル言語リソースを使用するには、*language_term* に「0x0」を指定してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 フルテキストの述語と関数の対象は、FROM 述語で示される 1 つのテーブルです。 複数のテーブルを検索するには、FROM 句で結合テーブルを使用して、複数のテーブルが組み合わされた結果セットを検索します。  
  
FREETEXT を使用するフルテキスト クエリは、CONTAINS を使用するフルテキスト クエリほど正確ではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索エンジンでは、重要な単語と語句が識別されます。 予約済みキーワードやワイルドカード文字は、CONTAINS 述語の \<contains_search_condition> パラメーターに指定した場合は特別な意味が与えられますが、FREETEXT の場合は特別な意味はありません。
  
 データベースの互換性レベルが 100 に設定されている場合、[OUTPUT 句](../../t-sql/queries/output-clause-transact-sql.md) でフルテキスト述語を使用することはできません。  
  
> [!NOTE]  
>  FREETEXTTABLE 関数は、FREETEXT 述語と同様の検索に役立ちます。 この関数は、SELECT ステートメントの [FROM 句](../../t-sql/queries/from-transact-sql.md)の中で通常のテーブル名のように参照できます。 詳細については、「[FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)」を参照してください。  
  
## <a name="querying-remote-servers"></a>リモート サーバーのクエリ  
 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) または FREETEXT 述語に 4 つの要素で構成される名前を使用して、リンク サーバー上にある対象テーブルのフルテキスト インデックス列にクエリを実行できます。 フルテキスト クエリを受け取るようリモート サーバーを準備するには、リモート サーバー上の検索対象のテーブルおよび列にフルテキスト インデックスを作成し、リモート サーバーをリンク サーバーとして追加します。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE とフルテキスト検索の比較  
 フルテキスト検索とは異なり、[LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 述語は、文字パターンにのみで動作します。 また、フォーマットされたバイナリ データのクエリには LIKE 述語を使用できません。 さらに、構造化されていない大量のテキスト データに対して LIKE クエリを実行すると、同じデータに対して同等のフルテキスト検索を実行する場合に比べてはるかに時間がかかります。 数百万行のテキスト データに対して LIKE クエリを実行すると、結果が得られるまでに数分かかる場合があります。一方、同じデータに対してフルテキスト クエリを実行すると、返される行数にもよりますが、数秒以内で結果を取得できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-freetext-to-search-for-words-containing-specified-character-values"></a>A. FREETEXT を使用して、指定した文字値を含む単語を検索する  
 次の例では、vital、safety、components に関連する単語を含むすべてのドキュメントを検索します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components' );  
GO  
```  
  
### <a name="b-using-freetext-with-variables"></a>B. FREETEXT で変数を使用する  
 次の例では、特定の検索語ではなく変数を使用します。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30);  
SET @SearchWord = N'high-performance';  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索の概要](../../relational-databases/search/get-started-with-full-text-search.md)   
 [フルテキスト カタログの作成と管理](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索クエリの作成 &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
