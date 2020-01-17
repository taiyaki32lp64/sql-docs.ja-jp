---
title: STRING_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f7dd020c0ec7f68dbd589b6e07026adfab86c890
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75720819"
---
# <a name="string_agg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

文字列式の値を連結し、値の間に区切り記号を挿入します。 文字列の末尾に区切り記号は追加されません。 

SQL Server 2017 で導入されました。
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>引数

*式 (expression)*  
任意のデータ型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 連結時に式は `NVARCHAR` または `VARCHAR` 型に変換されます。 文字列以外の型は `NVARCHAR` 型に変換されます。

*separator*  
連結される文字列の区切り記号として使用される `NVARCHAR` または `VARCHAR` 型の[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 リテラルまたは変数を使用できます。 

<order_clause>   
必要に応じて、`WITHIN GROUP` 句を使用して連結結果の順序を指定します。

```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  結果を並べ替えるために使用できる、定数ではない[式](../../t-sql/language-elements/expressions-transact-sql.md)のリスト。 クエリごとに 1 つの `order_by_expression` のみを使用できます。 既定の並べ替え順は昇順です。   
  
## <a name="return-types"></a>戻り値の型

戻り値の型は、最初の引数 (式) に依存します。 入力の引数が文字列型 (`NVARCHAR`、`VARCHAR`) の場合、結果の型は入力の型と同じになります。 次の表は自動変換の一覧です。  

|入力式の型 |結果 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1...4000) |NVARCHAR(4000) |
|VARCHAR(1...8000) |VARCHAR(8000) |
|int、bigint、smallint、tinyint、numeric、float、real、bit、decimal、smallmoney、money、datetime、datetime2、 |NVARCHAR(4000) |

## <a name="remarks"></a>解説

`STRING_AGG` は、すべての式を行から取り出し、それらを 1 つの文字列に連結する集計関数です。 式の値は、暗黙的に文字列型に変換され、連結されます。 文字列への暗黙の変換は、データ型変換の既存の規則に従います。 データ型の変換の詳細については、「[CAST および CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。 

入力式が `VARCHAR` 型の場合、区切り記号を `NVARCHAR` 型にすることはできません。 

null 値は無視され、対応する区切り記号は追加されません。 null 値のプレースホルダーを返すには、例 B を参照して `ISNULL` 関数を使用します。

`STRING_AGG` は任意の互換性レベルで使用できます。

## <a name="examples"></a>例

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. 新しい行で区切られた名前のリストを生成する

次の例では、復帰文字で区切られた名前のリストを単一の結果セルに生成します。
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`name` セルにある `NULL` 値は結果で返されません。   

> [!NOTE]  
>  Management Studio のクエリ エディターを使用している場合、 **[結果をグリッドに表示]** オプションで復帰文字を実装できません。 結果セットを正しく表示するには、 **[結果をテキストで表示]** に切り替えてください。   

### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. NULL 値を含まない、コンマ区切りの名前のリストを生成する

次の例では、null 値を 'N/A' に置き換え、コンマで区切った名前を 1 つの結果セルに返します。  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Csv | 
|--- |
|John,N/A,Mike,Peter,N/A,N/A,Alice,Bob |  

### <a name="c-generate-comma-separated-values"></a>C. コンマ区切り値を生成する

```sql
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|names |
|--- |
|Ken Sánchez (Feb  8 2003 12:00AM) <br />Terri Duffy (Feb 24 2002 12:00AM) <br />Roberto Tamburello (Dec  5 2001 12:00AM) <br />Rob Walters (Dec 29 2001 12:00AM) <br />... |

> [!NOTE]  
> Management Studio のクエリ エディターを使用している場合、 **[結果をグリッドに表示]** オプションで復帰文字を実装できません。 結果セットを正しく表示するには、 **[結果をテキストで表示]** に切り替えてください。

### <a name="d-return-news-articles-with-related-tags"></a>D. 関連するタグが付いたニュース記事を返す

記事とそのタグは別のテーブルに分かれています。 開発者は、すべての関連するタグが付いた記事ごとに 1 つの行を返したいと考えています。 この場合、次のクエリを使用します。

```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags
FROM dbo.Article AS a
LEFT JOIN dbo.ArticleTag AS t
    ON a.ArticleId = t.ArticleId
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |tags |
|--- |--- |--- |
|172 |Polls indicate close election results |politics,polls,city council |
|176 |New highway expected to reduce congestion |NULL |
|177 |Dogs continue to be more popular than cats |polls,animals|

> [!NOTE]
> `STRING_AGG` 関数が `SELECT` 一覧内の唯一の項目ではない場合は、`GROUP BY` 句が必要です。

### <a name="e-generate-list-of-emails-per-towns"></a>E. 町ごとの電子メール アドレスのリストを生成する

次のクエリは、従業員の電子メール アドレスを検索し、町ごとにグループ化します。

```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|町 |emails |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

emails 列に返された電子メール アドレスは、特定の町で働く従業員のグループに電子メールを送信する場合にそのまま使用できます。 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 町ごとの電子メール アドレスの並べ替えられたリストを生成する   
次のクエリは、前の例と同様に、従業員の電子メール アドレスを検索し、町ごとにグループ化し、電子メール アドレスをアルファベット順に並べ替えます。   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|町 |emails |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |

## <a name="see-also"></a>参照
 
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

