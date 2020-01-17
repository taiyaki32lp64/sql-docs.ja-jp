---
title: _ (ワイルドカード - 1 文字に一致) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f6876003c64889d32e31266ebe74b6532c1a8f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000307"
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (ワイルドカード - 1 文字に一致) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

アンダースコア _ を使用し、`LIKE` や `PATINDEX` などのパターン照合を含む文字列比較操作で任意の 1 文字に一致させます。  
  
## <a name="examples"></a>使用例  

## <a name="a-simple-example"></a>A:簡単な例   

次の例では、データベース名の文字 `m` から始まり、3 番目の文字が `d` のデータベースがすべて返されます。 アンダースコア文字は、名前の 2 番目の文字は何の文字でもよいことを指定します。 `model` データベースと `msdb` データベースがこの条件を満たしています。 `master` データベースはこの条件を満たしません。

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
さらに多くのデータベースがこの条件を満たすこともあるでしょう。

複数のアンダースコアを使用し、複数の文字を表すことができます。 `LIKE` 条件を変更し、2 つのアンダースコア `'m__%` を含めると、結果に master データベースが含まれます。

### <a name="b-more-complex-example"></a>B:より複雑な例
 次の例では、_ 演算子を使用して、`Person` テーブル内の `an` で終わる 3 文字の名前 (名) を持つすべての人物を検索します。  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: アンダースコア文字をエスケープ処理する   
次の例では、`db_owner` や `db_ddladmin` など、固定データベース ロールの名前を返しますが、`dbo` ユーザーも返します。 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

3 番目の文字位置に入っているアンダースコアはワイルドカードとして扱われ、文字 `db_` で始まるプリンシパルだけで絞り込んでくれません。 アンダースコアをエスケープ処理するには、かっこ `[_]` で囲みます。 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
これで `dbo` ユーザーが除外されます。   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>参照  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (ワイルドカード - 一致する文字列)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (ワイルドカード - 一致する文字列)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (ワイルドカード - 一致しない文字列)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
