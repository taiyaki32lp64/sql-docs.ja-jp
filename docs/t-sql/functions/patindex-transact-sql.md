---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f718d61c351e11c0e5d159e683390cf311f49e48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914364"
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  すべて有効なテキストおよび文字データ型について、指定された式の中で、パターンが最初に現れる先頭位置を返します。パターンが見つからない場合は、0 を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>引数  
 *pattern*  
 検索するシーケンスを含む文字式です。 ワイルドカード文字も指定できますが、(先頭の文字または最後の文字を検索する場合を除き) *pattern* を % 文字で囲む必要があります。 *pattern* は文字列データ型に分類される式です。 *pattern* の上限は 8,000 文字です。  
  
 *式 (expression)*  
 [式](../../t-sql/language-elements/expressions-transact-sql.md)です。通常は、指定したパターンで検索する列です。 *式*は文字列データ型に分類されます。  
  
## <a name="return-types"></a>戻り値の型  
*expression* が **varchar(max)** または **nvarchar(max)** データ型の場合は **bigint**。それ以外の場合は **int**。  
  
## <a name="remarks"></a>Remarks  
*pattern* または*式*が NULL の場合、PATINDEX は NULL を返します。  
 
PATINDEX の開始位置は 1 です。
 
PATINDEX では、入力の照合順序に基づいて比較が行われます。 指定した照合順序で比較を実行するには、COLLATE を使って入力に明示的な照合順序を適用できます。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
SC の照合順序を使用する場合、戻り値では、*expression* パラメーターの UTF-16 サロゲート ペアが 1 文字としてカウントされます。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
0x0000 (**char(0)** ) の Windows 照合順序で未定義の文字は、PATINDEX に含めることができません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-simple-patindex-example"></a>A. 簡単な PATINDEX の例  
 次の例では、文字 `ter` の開始位置の短い文字列 (`interesting data`) を確認します。  
  
```sql  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. PATINDEX でパターンを使用する  
次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `ensure` テーブルにある `DocumentSummary` 列の特定の行で、パターン `Document` が始まる位置を検出します。  
  
```sql  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
検索する行を `WHERE` 句で限定しない場合は、クエリによりテーブル内のすべての行が返されます。パターンが見つかった行は 0 以外の値に、パターンが見つからなかったすべての行は 0 になります。  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. PATINDEX でワイルドカード文字を使用する  
 次の例では、ワイルドカードの % と _ を使用して、指定した文字列で任意の 1 文字と `'en'` が続くパターン `'ure'` が始まる位置を探します (インデックスは 1 から開始)。  
  
```sql  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
`PATINDEX` は `LIKE` と同様の機能を持つので、任意のワイルドカードを使用できます。 パターンを % で囲む必要はありません。 `PATINDEX('a%', 'abc')` は 1 を返し、`PATINDEX('%a', 'cba')` は 3 を返します。  
  
 `LIKE` とは異なり、`PATINDEX` は `CHARINDEX` と同様に位置を返します。  
  
### <a name="d-using-collate-with-patindex"></a>D. PATINDEX で COLLATE を使用する  
 次の例では、`COLLATE` 関数を使って、検索する式の照合順序を明示的に指定します。  
  
```sql  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. 変数を使用してパターンを指定する  
次の例では、変数を使用して *pattern* パラメーターに値を渡します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```sql  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
------------  
22
```  
  
## <a name="see-also"></a>参照  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [[ ] &#40;ワイルドカード - 一致する文字列&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [[^] &#40;ワイルドカード - 一致しない文字列&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;ワイルドカード - 1 文字に一致&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [パーセント文字 &#40;ワイルドカード - 一致する文字列&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


