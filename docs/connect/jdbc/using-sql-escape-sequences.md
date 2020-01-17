---
title: SQL エスケープシーケンスの使用 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da2ae6b5353448d5281910d94aeef05ee0999c6a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025893"
---
# <a name="using-sql-escape-sequences"></a>SQL エスケープ シーケンスの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、JDBC API で定義された SQL エスケープ シーケンスを使用することができます。 SQL ステートメント内のエスケープ シーケンスは、SQL 文字列のエスケープ部分を異なる方法で処理することを、JDBC ドライバーに指示するために使用します。 JDBC ドライバーが SQL 文字列のエスケープ部分を処理すると、文字列の該当部分は SQL Server が理解する SQL コードに変換されます。  
  
 JDBC API で要求されるエスケープ シーケンスには 5 つの種類があり、すべて JDBC ドライバーによってサポートされています。  
  
- LIKE ワイルドカード リテラル
- 関数処理
- 日付および時刻のリテラル
- ストアド プロシージャの呼び出し
- 外部結合
- LIMIT エスケープ構文

JDBC ドライバーで使用されるエスケープ シーケンスの構文は、次のとおりです。  
  
`{keyword ...parameters...}`  
  
> [!NOTE]  
> SQL のエスケープ処理は、JDBC ドライバーに対して常に有効化されています。  
  
以下のセクションでは、5 つの種類のエスケープ シーケンスと、それらが JDBC ドライバーでどのようにサポートされているかについて説明します。  
  
## <a name="like-wildcard-literals"></a>LIKE ワイルドカード リテラル

JDBC ドライバーは、LIKE 句でワイルドカードをリテラルとして使用する `{escape 'escape character'}` 構文をサポートします。 たとえば次のコードでは、col2 の値が (ワイルドカードとしてではなく) 文字どおりアンダースコアで始まっている行の col3 の値が返されます。  

```java
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```

> [!NOTE]  
> エスケープ シーケンスは、SQL ステートメントの末尾に置く必要があります。 コマンド文字列内に複数の SQL ステートメントがある場合、エスケープ シーケンスは該当する各 SQL ステートメントの末尾に置く必要があります。  

## <a name="function-handling"></a>関数処理

JDBC ドライバーは、次の構文で SQL ステートメント内の関数エスケープ シーケンスをサポートしています。  

```sql
{fn functionName}  
```

`functionName` は、JDBC ドライバーでサポートされている関数です。 例: 

```sql
SELECT {fn UCASE(Name)} FROM Employee  
```

次の表は、JDBC ドライバーで関数エスケープ シーケンスを使用する場合にサポートされている、さまざまな関数を示します。  
  
| 文字列関数                                                                                                                                                                                                                                                                                                                        | 数値関数                                                                                                                                                                                                                                                                                                                                                                                                   | 日付時刻関数                                                                                                                                                                                                                                                                                                                                             | システム関数                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> [LTRIM]<br /><br /> REPEAT<br /><br /> [REPLACE]<br /><br /> RIGHT<br /><br /> [RTRIM]<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> [SUBSTRING]<br /><br /> UCASE | ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> [ROUND]<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE | CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> [DAYOFWEEK]<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> [NOW]<br /><br /> [QUARTER]<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> [WEEK]<br /><br /> YEAR | DATABASE<br /><br /> IFNULL<br /><br /> User |

> [!NOTE]  
> データベースでサポートされていない関数を使用すると、エラーが発生します。  

## <a name="date-and-time-literals"></a>日付および時刻のリテラル

日付、時刻、およびタイムスタンプのリテラルに使用するエスケープ構文は、次のとおりです。  

```sql
{literal-type 'value'}  
```

ここで `literal-type` は、次のいずれかです。  
  
| リテラルの種類 | [説明] | 値の形式               |
| ------------ | ----------- | -------------------------- |
| d            | date        | yyyy-mm-dd                 |
| t            | Time        | hh:mm:ss [1]               |
| ts           | TimeStamp   | yyyy-mm-dd hh:mm:ss[.f...] |
  
例:  

```sql
UPDATE Orders SET OpenDate={d '2005-01-31'}
WHERE OrderID=1025  
```

## <a name="stored-procedure-calls"></a>ストアド プロシージャの呼び出し

JDBC ドライバーでは、ストアド プロシージャ呼び出しについては、戻りパラメーターを処理する必要があるかどうかによって、`{? = call proc_name(?,...)}` および `{call proc_name(?,...)}` というエスケープ構文がサポートされています。  
  
プロシージャは、データベースに格納されている実行可能なオブジェクトです。 これは通常、プリコンパイルされた 1 つ以上の SQL ステートメントです。 ストアド プロシージャを呼び出すためのエスケープ シーケンス構文は、次のとおりです。  

```sql
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```

`procedure-name` にはストアド プロシージャの名前を指定し、`parameter` にはストアド プロシージャのパラメーターを指定します。  
  
ストアドプロシージャでのエスケープシーケンス`call`の使用の詳細については、「[ストアドプロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md)」を参照してください。  

## <a name="outer-joins"></a>外部結合

JDBC ドライバーでは、SQL92 の左外部結合、右外部結合、および完全外部結合で使用する構文がサポートされています。 外部結合用のエスケープ シーケンスは、次のとおりです。  

```sql
{oj outer-join}  
```

outer-join の内容は次のとおりです。  

```sql
table-reference {LEFT | RIGHT | FULL} OUTER JOIN
{table-reference | outer-join} ON search-condition  
```

`table-reference` はテーブル名で、`search-condition` はテーブルで使用する結合条件です。  
  
例:  

```sql
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status
   FROM {oj Customers LEFT OUTER JOIN
      Orders ON Customers.CustID=Orders.CustID}
   WHERE Orders.Status='OPEN'  
```

JDBC ドライバーでは、次の外部結合エスケープ シーケンスがサポートされています。  

- 左外部結合
- 右外部結合
- 完全外部結合
- 入れ子になった外部結合

## <a name="limit-escape-syntax"></a>LIMIT エスケープ構文  

> [!NOTE]  
> LIMIT エスケープ構文は、Microsoft JDBC Driver 4.2 for SQL Server (以降) でのみ、JDBC 4.1 以降を使用する場合にサポートされます。  
  
 LIMIT のエスケープ構文は次のとおりです。  

```sql
LIMIT <rows> [OFFSET <row offset>]  
```

エスケープ構文には 2 つの部分があります。\<*rows*> は必須であり、返される行数を指定します。 OFFSET と \<*row offset*> は省略可能であり、返される行の先頭までスキップする行数を指定します。 JDBC ドライバーでは、このうち必須の部分のみがサポートされ、LIMIT の代わりに TOP を使用するようにクエリを変換して処理されます。 SQL Server は、LIMIT 句をサポートしていません。 **JDBC ドライバーは、省略可能な \<row offset> をサポートしていません。これを使用すると、ドライバーが例外をスローします**。  
  
## <a name="see-also"></a>参照

[JDBC ドライバーでのステートメントの使用](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
