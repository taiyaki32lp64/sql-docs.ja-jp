---
title: xml データ型メソッドの使用に関するガイドライン | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b354f824da86e3bfcc5fb8d6279cb755048046d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051302"
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>xml データ型メソッドの使用に関するガイドライン

[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

このトピックでは、**xml** データ型のメソッドの使用に関するガイドラインを説明します。

## <a name="the-print-statement"></a>PRINT ステートメント

**xml** データ型メソッドは、次の例のように PRINT ステートメント内で使用することはできません。 **xml** データ型メソッドはサブクエリとして扱われますが、PRINT ステートメント内ではサブクエリの使用は認められていません。 このため、次の例ではエラーが返されます。

```sql
DECLARE @x xml
SET @x = '<root>Hello</root>'
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)
```

解決方法の 1 つとしては、まず **value()** メソッドの結果を **xml** 型の変数に割り当ててから、この変数をクエリに指定します。

```sql
DECLARE @x xml
DECLARE @c varchar(max)
SET @x = '<root>Hello</root>'
SET @c = @x.value('/root[1]', 'varchar(11)')
PRINT @c
```

## <a name="the-group-by-clause"></a>GROUP BY 句

**xml** データ型メソッドは、内部的にサブクエリとして扱われます。 GROUP BY はスカラーを必要とし、また、集計やサブクエリを許容しないため、GROUP BY 句には **xml** データ型メソッドは指定できません。 解決方法として、XML メソッドを内部で使用するユーザー定義関数を呼び出します。

## <a name="reporting-errors"></a>エラーの報告

エラーが報告されると、**xml** データ型メソッドは次の形式で単一のエラーを生成します。

```
Msg errorNumber, Level levelNumber, State stateNumber:
XQuery [database.table.method]: description_of_error
```

例:

```
Msg 2396, Level 16, State 1:
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element
```

## <a name="singleton-checks"></a>シングルトンの確認

実行時にシングルトンであることが確実かどうかをコンパイラで判断できない場合、シングルトンを必要とするロケーション ステップ、関数パラメーター、および演算子はエラーを返します。 型指定されていないデータではこの問題が頻繁に発生します。 たとえば、属性の参照には単一の親要素が必要ですが、 単一の親ノードを選択する序数があれば十分です。 **node()** -**value()** の組み合わせを評価して属性値を抽出するときは、序数を指定する必要がない場合もあります。 次の例を参照してください。

### <a name="example-known-singleton"></a>例:既知のシングルトン

次の例では、**nodes()** メソッドで `<book>` 要素ごとに個別の行が生成されます。 `<book>` ノードで評価される **value()** メソッドでは、`@genre` の値を抽出します。これは属性であり、シングルトンです。

```sql
SELECT nref.value('@genre', 'varchar(max)') LastName
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)
```

型指定された XML の型の確認には XML スキーマが使用されます。 XML スキーマでノードがシングルトンとして指定されている場合、その情報がコンパイラで使用され、エラーは発生しません。 それ以外の場合、単一ノードを選択する序数が必要です。 特に、`/book//title` などの、descendant-or-self 軸 (//) を使用すると、XML スキーマでシングルトンが指定されていても `<title>` 要素のシングルトン カーディナリティ推定が厳密ではなくなります。 そのため、これを「`(/book//title)[1]`」と書き換える必要があります。

型の確認では、`//first-name[1]` と `(//first-name)[1]` の違いを常に認識することが重要です。 前者は兄弟の中で最も左の `<first-name>` ノードのみから構成される `<first-name>` ノードのシーケンスを返します。 後者は XML インスタンスのドキュメント順で最初のシングルトンの `<first-name>` ノードを返します。

### <a name="example-using-value"></a>例:value() の使用

型指定されていない XML 列に対し次のクエリを実行すると、静的なコンパイル エラーが発生します。**value()** の最初の引数はシングルトン ノードでなければなりませんが、`<last-name>` ノードが実行時に現れる回数が 1 回のみかどうかをコンパイラで判断できないためです。

```sql
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName
FROM   T
```

次のような解決策が考えられます。

```sql
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName
FROM   T
```

しかし、各 XML インスタンスで `<author>` ノードが複数回現れる場合があるので、これではエラーは解決しません。 次のように書き換えると、正常に動作します。

```sql
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName
FROM   T
```

このクエリは、各 XML インスタンスの最初の `<last-name>` 要素の値を返します。

## <a name="see-also"></a>参照

- [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)
