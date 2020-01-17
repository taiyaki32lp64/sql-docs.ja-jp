---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: 5d497064378b7fe34c95ffe9c886144bb3523256
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943333"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

SELECT クエリは、結果を行セットとして返します。 必要に応じて、SQL クエリに FOR XML 句を指定することで、SQL クエリの結果を XML 形式で取得することができます。 FOR XML 句は、最上位レベルのクエリとサブクエリのいずれでも使用できます。 最上位レベルの FOR XML 句は、SELECT ステートメント内でのみ使用できます。 サブクエリでは、FOR XML を INSERT、UPDATE、DELETE ステートメント内で使用できます。 FOR XML は代入ステートメントでも使用できます。

FOR XML 句には、次のモードのうち 1 つを指定します。

- RAW
- AUTO
- EXPLICIT
- PATH

RAW モードは SELECT ステートメントによって返された行セットの行 1 つにつき 1 つの \<row> 要素を生成します。 入れ子にした FOR XML クエリを作成することで、XML 階層を生成できます。

AUTO モードは、SELECT ステートメントがどのように指定されているかに基づき、帰納的な方法で入れ子になった結果の XML を生成します。 生成される XML の構造については最小限の制御しか行えません。 AUTO モードで帰納的に生成された XML 構造に対して、入れ子になった FOR XML クエリを作成し、XML 階層を生成することができます。

EXPLICIT モードでは、XML の構造をより厳密に制御することができます。 属性や要素を自由に組み合わせて、XML の構造を決めることができます。 このモードでは、クエリを実行した結果として生成される行セットに特定の形式を指定する必要があります。 その後、この行セットの形式が、XML の構造にマップされます。 EXPLICIT モードの利点は、属性と要素を自由に組み合わせることができる点です。また、ラッパーや入れ子にした複雑なプロパティを作成したり、スペースで区切られた値を作成したり (OrderID 属性に注文 ID 値の一覧を渡すなど)、混合コンテンツを作成することもできます。

ただし、EXPLICIT モードのクエリを記述する作業は複雑になることがあります。 EXPLICIT モードを使用して階層を生成する代わりに、RAW、AUTO、または PATH モードの入れ子にした FOR XML クエリと TYPE ディレクティブを作成するなど、FOR XML の新しい機能を使用できます。 このような入れ子にした FOR XML クエリでも、EXPLICIT モードで生成できる XML を作成することができます。 詳細については、 [入れ子になった FOR XML クエリの使用](../../relational-databases/xml/use-nested-for-xml-queries.md) および [FOR XML クエリの TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md)を参照してください。

PATH モードと FOR XML クエリの入れ子機能を組み合わせると、EXPLICIT モードと同等の柔軟性が得られます。

これらのモードは、モードが設定されたクエリの実行に限って有効です。 後続のクエリの結果に影響は与えません。

FOR BROWSE 句で使用されるどのような選択に対しても FOR XML は無効です。

## <a name="example"></a>例

次の `SELECT` ステートメントは、 `Sales.Customer` データベースの `Sales.SalesOrderHeader` テーブルおよび `AdventureWorks2012` テーブルの情報を取得します。 このクエリでは、 `AUTO` 句に `FOR XML` モードを指定しています。

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>FOR XML 句とサーバー名

FOR XML 句を伴う SELECT ステートメントが、クエリの中で 4 つの部分から構成される名前を指定している場合、クエリがローカル コンピューター上で実行されると、結果の XML ドキュメントにサーバー名は返されません。 しかし、クエリがネットワーク サーバー上で実行されると、4 つの部分から構成される名前でサーバー名が返されます。

たとえば、次のクエリについて考えてみます。

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**ローカル サーバー**:&nbsp; `ServerName` がローカル サーバーの場合、クエリでは次のテキストが返されます。

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**ネットワーク サーバー**:&nbsp; `ServerName` がネットワーク サーバーの場合、クエリでは次のテキストが返されます。

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**あいまいさの排除**:&nbsp; 次の別名を指定することによって、このようなあいまいさの可能性を排除できます。

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

明確なクエリで次のテキストが返されるようになります。

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>参照

[FOR XML 句の基本構文](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
