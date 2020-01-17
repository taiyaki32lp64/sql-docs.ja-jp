---
title: サブクエリ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.technology: performance
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Subquery
- Subqueries
- subqueries [SQL Server], fundamentals
- subqueries [SQL Server], correlated
- subqueries [SQL Server], types
ms.assetid: bfc97432-c14c-4768-9dc5-a9c512f6b2bd
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2d4bb708142d4471381a1579baa943d11357823
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113285"
---
# <a name="subqueries-sql-server"></a>サブクエリ (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 
サブクエリとは、`SELECT`、`INSERT`、`UPDATE`、または `DELETE` の各ステートメントの内部、または別のサブクエリの内部で入れ子になっているクエリです。 サブクエリは、式が使えるところであればどこにでも使用できます。 次の例では、SELECT ステートメント内にある MaxUnitPrice という列に対する式としてサブクエリを使用します。

```sql
USE AdventureWorks2016;
GO
SELECT Ord.SalesOrderID, Ord.OrderDate,
    (SELECT MAX(OrdDet.UnitPrice)
     FROM Sales.SalesOrderDetail AS OrdDet
     WHERE Ord.SalesOrderID = OrdDet.SalesOrderID) AS MaxUnitPrice
FROM Sales.SalesOrderHeader AS Ord;
GO
```

## <a name="fundamentals"></a> サブクエリの基礎
サブクエリは内部クエリや内部選択と呼ばれることもあります。また、サブクエリを含むステートメントは外部クエリや外部選択と呼ばれます。   

サブクエリを含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの多くは、サブクエリを使う代わりに結合を使って表現することもできます。 サブクエリでしか発生しない問題もあります。 通常、[!INCLUDE[tsql](../../includes/tsql-md.md)] では、サブクエリを含むステートメントと、意味は同じでもサブクエリを含まないステートメントとの間にパフォーマンスの違いはありません。 ただし、存在を検査する必要がある場合には、結合によってパフォーマンスが向上することもあります。 それ以外の場合は、入れ子になったクエリを外側のクエリの結果ごとに処理し、重複が確実に解消されるようにする必要があります。 このような場合、結合のアプローチを使った方が良い結果になります。 次の例は、サブクエリ `SELECT` と結合の `SELECT` が同じ結果を返すことを示しています。

```sql
USE AdventureWorks2016;
GO

/* SELECT statement built using a subquery. */
SELECT Name
FROM Production.Product
WHERE ListPrice =
    (SELECT ListPrice
     FROM Production.Product
     WHERE Name = 'Chainring Bolts' );
GO

/* SELECT statement built using a join that returns
   the same result set. */
SELECT Prd1. Name
FROM Production.Product AS Prd1
     JOIN Production.Product AS Prd2
       ON (Prd1.ListPrice = Prd2.ListPrice)
WHERE Prd2. Name = 'Chainring Bolts';
GO
```

1 つ上のレベルの SELECT ステートメントの中で入れ子になったサブクエリの SELECT の構成要素は、次のようになります。    
-   標準の選択リスト構成要素を含んでいる標準の `SELECT` クエリ。   
-   1 つ以上のテーブル名またはビュー名を含んでいる標準の `FROM` 句。   
-   省略可能な `WHERE` 句。   
-   省略可能な `GROUP BY` 句。   
-   省略可能な `HAVING` 句。   

サブクエリの SELECT クエリは常にかっこで囲みます。 `COMPUTE` 句または `FOR BROWSE` 句を含むことはできず、TOP 句も指定された場合に `ORDER BY` 句を含むことだけができます。   

サブクエリは、1 つ上のレベルの `SELECT`、`INSERT`、`UPDATE`、または `DELETE` の各ステートメントの `WHERE` 句または `HAVING` 句の中、あるいは別のサブクエリの中で入れ子にできます。 32 レベルまで入れ子にできますが、上限はクエリの複雑さと使用可能なメモリによって変わります。 個々のクエリでは 32 レベルまで入れ子にすることはできません。 サブクエリは、単一の値を返す限り、式が使えるところであればどこにでも使用できます。   

あるテーブルがサブクエリにのみ現れていて、1 つ上のレベルのクエリに現れていない場合、そのテーブルの列は出力 (1 つ上のレベルのクエリの選択リスト) に含めることはできません。   

サブクエリを含むステートメントは、通常、次の形式のいずれかになります。   
-   WHERE 式 \[NOT] IN (サブクエリ)
-   WHERE 式 comparison_operator \[ANY | ALL] (サブクエリ)
-   WHERE \[NOT] EXISTS (サブクエリ)   

[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの中には、サブクエリが独立したクエリであるように評価されるものがあります。 概念的には、サブクエリの結果が 1 つ上のレベルのクエリに代入されることになります。ただし、サブクエリを含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってこのように処理されるとは限りません。    

サブクエリの種類は、大きく 3 つに分けられます。 具体的には、次のように大別されます。 
-   `IN` で導かれるリスト、あるいは `ANY` または `ALL` で修飾された比較演算子で導かれるリストを操作するサブクエリ。
-   修飾されていない比較演算子で導かれ、単一の値を返す必要があるサブクエリ
-   `EXISTS` で導かれる、存在を検査するサブクエリ。

## <a name="rules"></a> サブクエリの規則
サブクエリには次の制限があります。 
-   比較演算子で導かれたサブクエリの選択リストには、式または列名を 1 つしか入れることができません。ただし、`EXISTS` および `IN` では、それぞれ `SELECT *` とリストを使用できます。   
-   1 つ上のレベルのクエリの `WHERE` 句に列名が含まれている場合、サブクエリの選択リストで指定されている列との結合互換性が必要です。   
-   **ntext**、**text**、**image** の各データ型は、サブクエリの選択リストでは使用できません。   
-   修飾されていない比較演算子 (キーワード ANY または ALL が後に付いていないもの) で導かれたサブクエリは、単一の値を返す必要があるため、`GROUP BY` 句および `HAVING` 句を含めることはできません。   
-   GROUP BY を含むサブクエリでは、`DISTINCT` キーワードは使用できません。
-   `COMPUTE` 句と `INTO` 句は指定できません。   
-   `ORDER BY` 句を指定できるのは、`TOP` 句が指定されているときだけです。   
-   サブクエリで作成されたビューは、更新できません。   
-   `EXISTS` で導かれたサブクエリの選択リストには、通例、単一の列名ではなくアスタリスク (\*) が使用されます。 `EXISTS` で導かれるサブクエリの規則は、標準の選択リストの規則と同じです。これは、`EXISTS` で導かれるサブクエリは存在検査を行うもので、データではなく TRUE または FALSE を返すためです。   

## <a name="qualifying"></a> サブクエリで使用する列名の修飾
次の例で、外側のクエリの `WHERE` 句内の *BusinessEntityID* 列は、外側のクエリの `FROM` 句内のテーブル名 (*Sales.Store*) で暗黙的に修飾されています。 サブクエリの選択リスト内の *CustomerID* への参照は、サブクエリの `FROM` 句、つまり *Sales.Customer* テーブルで修飾されています。

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE BusinessEntityID NOT IN
    (SELECT CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

一般的な規則としては、ステートメント内の列名は、同じレベルの `FROM` 句で参照しているテーブルで暗黙的に修飾されます。 サブクエリの `FROM` 句で参照しているテーブルに列名が存在しない場合、外側のクエリの `FROM` 句で参照しているテーブルで暗黙的に修飾されます。   

これらの暗黙的な修飾関係を明示的に指定すると、クエリは次のようになります。

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE Sales.Store.BusinessEntityID NOT IN
    (SELECT Sales.Customer.CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

テーブル名を明示的に記述しても間違いであるということはありません。明示的に修飾することで、テーブル名に関する暗黙的な修飾関係をいつでもオーバーライドすることができます。   

> [!IMPORTANT]
> サブクエリで参照している列が、サブクエリの `FROM` 句で参照しているテーブルにない場合でも、外側のクエリの `FROM` 句で参照しているテーブルに存在すれば、エラーが発生することなくクエリが実行されます。 サブクエリで参照している列は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、外側のクエリのテーブル名で暗黙的に修飾されます。   

## <a name="nesting"></a> 複数レベルの入れ子
サブクエリには 1 つ以上のサブクエリを含めることができます。 1 つのステートメント内で任意の数のサブクエリを入れ子にできます。   

次のクエリでは、従業員であり販売員でもある者の名前を検索しています。   

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person
WHERE BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM HumanResources.Employee
     WHERE BusinessEntityID IN
        (SELECT BusinessEntityID
         FROM Sales.SalesPerson)
    );
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName                                           FirstName
-------------------------------------------------- -----------------------
Jiang                                              Stephen
Abbas                                              Syed
Alberts                                            Amy
Ansman-Wolfe                                       Pamela
Campbell                                           David
Carson                                             Jillian
Ito                                                Shu
Mitchell                                           Linda
Reiter                                             Tsvi
Saraiva                                            Jos
Vargas                                             Garrett
Varkey Chudukatil                                  Ranjit
Valdez                                             Rachel
Tsoflias                                           Lynn
Pak                                                Jae
Blythe                                             Michael
Mensa-Annan                                        Tete

(17 row(s) affected)
```

最も内側のクエリは、販売員 ID を返します。 1 つ上のレベルのクエリはその販売員 ID で評価され、対応する従業員の連絡先 ID 番号を返します。 最後に、外側のクエリはこの連絡先 ID を使用して、従業員の名前を検索します。   

このクエリは、次のように結合の形で記述することもできます。

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person c
INNER JOIN HumanResources.Employee e
ON c.BusinessEntityID = e.BusinessEntityID
JOIN Sales.SalesPerson s 
ON e.BusinessEntityID = s.BusinessEntityID;
GO
```

## <a name="correlated"></a> 相関サブクエリ
多くのクエリは、サブクエリを 1 回実行し、その結果である 1 つまたは複数の値を外側のクエリの `WHERE` 句に代入することにより評価されます。 相関サブクエリ (繰り返しサブクエリとも呼びます) を含むクエリでは、サブクエリの値は外側のクエリによって決まります。 つまり、外側のクエリで選択される各行に対して 1 回ずつ、サブクエリが繰り返し実行されることになります。
次のクエリでは、各従業員の姓と名を検索し、その中から *SalesPerson* テーブルで示される特別手当の値が 5,000 で、従業員 ID が *Employee* テーブルと *SalesPerson* テーブルで一致しているものを取得しています。

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT c.LastName, c.FirstName, e.BusinessEntityID 
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000.00 IN
    (SELECT Bonus
    FROM Sales.SalesPerson sp
    WHERE e.BusinessEntityID = sp.BusinessEntityID) ;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName FirstName BusinessEntityID
-------------------------- ---------- ------------
Ansman-Wolfe Pamela 280
Saraiva José 282

(2 row(s) affected)
```

上記のステートメントのサブクエリは、外側のクエリから独立して評価できません。 このサブクエリでは *Employee.BusinessEntityID* の値が必要ですが、その値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により *Employee* テーブルの他の行が調べられると、それに応じて変化します。   
このクエリでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、Employee テーブルの各行の値が内側のクエリに代入されることによって、各行を結果に含めるかどうかが判断されます。
たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、最初に `Syed Abbas` の行が調べられると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により内側のクエリに代入された値 285 が変数 *Employee.BusinessEntityID* で取得されます。

```sql
USE AdventureWorks2016;
GO
SELECT Bonus
FROM Sales.SalesPerson
WHERE BusinessEntityID = 285;
GO
```

結果は 0 なので (`Syed Abbas` は販売員ではないので特別手当が出ません)、外側のクエリは次のように評価されます。

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000 IN (0.00);
GO
```

これは偽なので、`Syed Abbas` の行は結果に含められません。 同じ手順を `Pamela Ansman-Wolfe` の行に対して実行します。 この行が結果に含められることがわかります。     

相関サブクエリでは、特定のテーブルに含まれている列をテーブル値関数の引数として外側のクエリで参照することにより、`FROM` 句にテーブル値関数を含めることもできます。 この場合、外側のクエリの各行について、サブクエリに従ってテーブル値関数が評価されます。    
  
## <a name="types"></a> サブクエリの種類
サブクエリは、次のようにクエリのさまざまな部分で指定できます。 
-   別名と共に指定します。 詳しくは、「[別名を使ったサブクエリ](#aliases)」をご覧ください。
-   `IN` または `NOT IN` で。 詳しくは、「[IN で導かれるサブクエリ](#in)」および「[NOT IN で導かれるサブクエリ](#notin)」をご覧ください。
-   `UPDATE`、`DELETE`、`INSERT` ステートメントで。 詳しくは、「[UPDATE、DELETE、および INSERT ステートメントでのサブクエリ](#upsert)」をご覧ください。
-   比較演算子と共に指定します。 詳しくは、「[比較演算子によるサブクエリ](#comparison)」をご覧ください。
-   `ANY`、`SOME`、`ALL` で。 詳しくは、「[ANY、SOME、または ALL で修飾された比較演算子](#comparison_modified)」をご覧ください。
-   `EXISTS` または `NOT EXISTS` で。 詳しくは、「[EXISTS を使ったサブクエリ](#exists)」および「[NOT EXISTS を使用したサブクエリ](#notexists)」をご覧ください。
-   式の代わりに指定します。 詳しくは、「[式の代わりに使われるサブクエリ](#expression)」をご覧ください。

### <a name="aliases"></a> 別名を使ったサブクエリ
サブクエリと 1 つ上のレベルのクエリで同じテーブルを参照しているステートメントは、テーブルをそのテーブル自体に結合する自己結合として表すこともできます。 たとえば、サブクエリを使用して特定の州に住む従業員の住所を見つけられます。   

```sql
USE AdventureWorks2016;
GO
SELECT StateProvinceID, AddressID
FROM Person.Address
WHERE AddressID IN
    (SELECT AddressID
     FROM Person.Address
     WHERE StateProvinceID = 39);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
StateProvinceID AddressID
----------- -----------
39 942
39 955
39 972
39 22660

(4 row(s) affected)
```   

または、次のように自己結合を使うこともできます。   

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
INNER JOIN Person.Address AS e2
ON e1.AddressID = e2.AddressID
AND e2.StateProvinceID = 39;
GO
```

テーブルをそれ自体に結合する場合、テーブルが 2 つの異なる役割で使用されるので、テーブルの別名が必要になります。 別名は、次のように、内側のクエリと 1 つ上のレベルのクエリで同じテーブルを参照する入れ子になったクエリでも使えます。    

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
WHERE e1.AddressID IN
    (SELECT e2.AddressID
     FROM Person.Address AS e2
     WHERE e2.StateProvinceID = 39);
GO
```

別名を明示的に指定すると、サブクエリ内の *Person.Address* への参照が、1 つ上のレベルのクエリ内の参照と同一ではないことが明確になります。   

### <a name="in"></a> IN で導かれるサブクエリ
`IN` または `NOT IN` で導かれたサブクエリの結果は、0 個以上の値のリストになります。 サブクエリが結果を返すと、1 つ上のレベルのクエリがこの結果を使用します。    
次のクエリでは、Adventure Works Cycles が製造しているすべてのホイール製品の名前が検索されます。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]     

```
Name
----------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```

このステートメントは、2 段階で評価されます。 まず、内側のクエリが名前 "Wheel" と一致するサブカテゴリの ID 番号 (17) を返します。 次に、この値が 1 つ上のレベルのクエリに代入され、1 つ上のレベルのクエリがサブカテゴリの ID 番号に対応する製品名を Product の中から検索します。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN ('17');
GO
```

この例やこれに似た問題に対して、サブクエリではなく結合を使用すると、1 つの違いが生じます。結合では、複数のテーブルの列が結果に表示されます。 たとえば、製品のサブカテゴリ名を結果に含めるには、次のような結合を使う必要があります。    

```sql
USE AdventureWorks2016;
GO
SELECT p.Name, s.Name
FROM Production.Product p
INNER JOIN Production.ProductSubcategory s
ON p.ProductSubcategoryID = s.ProductSubcategoryID
AND s.Name = 'Wheels';
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
LL Mountain Front Wheel Wheels
ML Mountain Front Wheel Wheels
HL Mountain Front Wheel Wheels
LL Road Front Wheel Wheels
ML Road Front Wheel Wheels
HL Road Front Wheel Wheels
Touring Front Wheel Wheels
LL Mountain Rear Wheel Wheels
ML Mountain Rear Wheel Wheels
HL Mountain Rear Wheel Wheels
LL Road Rear Wheel Wheels
ML Road Rear Wheel Wheels
HL Road Rear Wheel Wheels
Touring Rear Wheel Wheels

(14 row(s) affected)
```    

次のクエリは、信用格付けが高く、Adventure Works Cycles が少なくとも 20 種類の商品を仕入れていて、納品までの期間が平均で 16 日未満のベンダーの名前を検索します。    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Purchasing.Vendor
WHERE CreditRating = 1
AND BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM Purchasing.ProductVendor
     WHERE MinOrderQty >= 20
     AND AverageLeadTime < 16);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Name
--------------------------------------------------
Compete Enterprises, Inc
International Trek Center
First National Sport Co.
Comfort Road Bicycles
Circuit Cycles
First Rate Bicycles
Jeff's Sporting Goods
Competition Bike Training Systems
Electronic Bike Repair & Supplies
Crowley Sport
Expert Bike Co
Team Athletic Co.
Compete, Inc.   

(13 row(s) affected)
```   

まず、内側のクエリが評価され、サブクエリの条件を満たすベンダーの ID 番号が返されます。 次に、1 つ上のレベルのクエリが評価されます。 内側のクエリと 1 つ上のレベルのクエリ両方の WHERE 句に複数の条件を含めることができることに注意してください。   

結合を使うと、上記のクエリは次のように表されます。

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT Name
FROM Purchasing.Vendor v
INNER JOIN Purchasing.ProductVendor p
ON v.BusinessEntityID = p.BusinessEntityID
WHERE CreditRating = 1
  AND MinOrderQty >= 20
  AND AverageLeadTime < 16;
GO
```

結合は常にサブクエリとして表すことができます。 サブクエリは、多くの場合、結合として表すことができますが、常に表せるわけではありません。 これは、結合に対照性があるためです。つまり、テーブル A とテーブル B をどのような順序で結合しても、得られる答えは同じになります。 サブクエリを使った場合、同じことが当てはまりません。    

### <a name="notin"></a> NOT IN で導かれるサブクエリ
キーワード NOT IN で導かれるサブクエリも、0 個以上の値のリストを返します。   
次のクエリでは、自転車 (完成品) 以外の製品名が検索されます。   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID NOT IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Mountain Bikes' 
        OR Name = 'Road Bikes'
        OR Name = 'Touring Bikes');
GO
```

このステートメントは結合に変換できません。 非等価結合はこれとよく似ていますが、意味は異なります。つまり、自転車 (完成品) 以外のサブカテゴリに属する製品名が検索されます。      

### <a name="upsert"></a> UPDATE、DELETE、および INSERT ステートメントでのサブクエリ
サブクエリは、`UPDATE`、`DELETE`、`INSERT`、`SELECT` の各データ操作言語 (DML) ステートメントで入れ子にできます。    

次の例では、*ListPrice* テーブルの *Production.Product* 列の値が 2 倍になります。 `WHERE` 句のサブクエリでは *Purchasing.ProductVendor* テーブルを参照して、*Product* テーブルで更新される行を *BusinessEntity* 1540 の行だけに制限しています。

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
WHERE ProductID IN
    (SELECT ProductID 
     FROM Purchasing.ProductVendor
     WHERE BusinessEntityID = 1540);
GO
```

上のクエリと同等の、結合を使用した `UPDATE` ステートメントを次に示します。

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
FROM Production.Product AS p
INNER JOIN Purchasing.ProductVendor AS pv
    ON p.ProductID = pv.ProductID AND BusinessEntityID = 1540;
GO   
```

### <a name="comparison"></a> 比較演算子によるサブクエリ
サブクエリは、次の比較演算子のいずれかで導くことができます (=、< >、>、> =、<、! >、! <、< =)。   

修飾されていない比較演算子 (後ろに `ANY` や `ALL` がない比較演算子) で導かれるサブクエリでは、`IN` によって導かれるサブクエリと同様に、値のリストでなく単一の値を返す必要があります。 このようなサブクエリから複数の値が返された場合は、SQL Server によりエラー メッセージが表示されます。    

修飾されていない比較演算子で導かれるサブクエリを使用するには、データや問題の性質を十分に理解して、そのサブクエリで値が 1 つしか返されないことを把握しておく必要があります。     

たとえば、販売員 1 人が 1 販売区域を担当すると仮定した場合に、`Linda Mitchell` が担当する区域の顧客を検索するには、次のように単純な = 比較演算子を使用したステートメントを作成できます。    

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID =
    (SELECT TerritoryID
     FROM Sales.SalesPerson
     WHERE BusinessEntityID = 276);
GO
```

ただし、`Linda Mitchell` が複数の販売区域を担当している場合は、エラー メッセージが返されます。 この場合、比較演算子 = の代わりに `IN` 式または = ANY を使用することができます。    

集計関数は単一の値を返すため、多くの場合、修飾されていない比較演算子で導かれるサブクエリには、集計関数が含まれます。 たとえば、次のステートメントでは、表示価格が平均表示価格よりも高いすべての製品の名前が検索されます。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT AVG (ListPrice)
     FROM Production.Product);
GO
```     

修飾されていない比較演算子で導かれるサブクエリでは単一の値を返す必要があるため、`GROUP BY` 句や `HAVING` 句を含めることはできません。ただし、GROUP BY 句や HAVING 句が単一の値を返すことがわかっている場合は例外です。 たとえば、次のクエリでは、サブカテゴリが 14 の製品で、最低価格の製品より高い価格の付けられた製品が検索されます。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT MIN (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID
     HAVING ProductSubcategoryID = 14);
GO
```

### <a name="comparison_modified"></a> ANY、SOME、または ALL で修飾された比較演算子
サブクエリを導く比較演算子は、キーワード ALL または ANY で修飾できます。 SOME は `ANY` に相当する ISO 標準です。     

修飾した比較演算子で導かれたサブクエリは、0 個以上の値のリストを返し、`GROUP BY` 句または `HAVING` 句を含むことができます。 これらのサブクエリは、`EXISTS` を使用して書き換えることができます。     

> 比較演算子を例として使用すると、`>ALL` は、どの値よりも大きいという意味になります。 つまり、最大値よりも大きいという意味です。 たとえば、`>ALL (1, 2, 3)` は 3 より大きいという意味になります。 `>ANY` は少なくとも 1 つの値より大きい、つまり最小値より大きいという意味です。 したがって、`>ANY (1, 2, 3)` は 1 より大きいという意味になります。
`>ALL` が含まれたサブクエリの行が外側のクエリで指定された条件を満たすには、サブクエリを導く列の値がサブクエリによって返される値のリストのどの値よりも大きい必要があります。    

同様に、`>ANY` は、行が外側のクエリで指定された条件を満たすには、サブクエリを導く列の値がサブクエリによって返される値のリストの少なくとも 1 つの値よりも大きい必要があることを意味します。    

次のクエリでは、ANY によって修飾された比較演算子で導かれたサブクエリの例を示します。 このクエリでは、製品のサブカテゴリの中から最も高い定価以上の定価が付けられた製品を検索します。    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >= ANY
    (SELECT MAX (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID);
GO
```    

Product サブカテゴリごとに、内側のクエリが最も高い定価を検索します。 外側のクエリは、これらすべての値を比較し、製品のサブカテゴリの中で最も高い定価以上の定価が付けられた製品を決定します。 `ANY` を `ALL` に変更すると、クエリは内側のクエリで返されたすべての定価以上の定価が付けられた製品のみを返します。    

サブクエリが値を返さない場合は、クエリ全体が値を返しません。    

`=ANY` 演算子は `IN` と同じ意味を持ちます。 たとえば、Adventure Works Cycles が製造しているすべてのホイール製品の名前を検索するときに、`IN` または `=ANY` を使用できます。

```sql
--Using =ANY
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID =ANY
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO

--Using IN
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

次に各クエリの結果セットを示します。

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

ただし、`<>ANY` 演算子は `NOT IN` とは異なります。`<>ANY` は、"not = a または not = b または not = c" という意味です。 `NOT IN` は、"not = a かつ not = b かつ not = c" という意味です。 `<>ALL` は `NOT IN` と同じ意味になります。     

たとえば、次のクエリでは、担当販売員がいない区域の顧客を検索します。     

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID <> ANY
    (SELECT TerritoryID
     FROM Sales.SalesPerson);
GO
```    

結果には、販売区域が NULL の顧客を除くすべての顧客が含まれます。これは、顧客に割り当てられている区域はすべて、いずれかの販売員が担当しているためです。 内側のクエリで販売員が担当しているすべての販売区域が検索されてから、外部クエリで各区域に属していない顧客が検索されます。    

同様の理由で、このクエリで `NOT IN` を使用すると、結果にはどの顧客も含められません。      

`NOT IN` と同じ意味の `<>ALL` 演算子を使用しても同じ結果が得られます。   

### <a name="exists"></a> EXISTS を使ったサブクエリ
サブクエリの導入にキーワード `EXISTS` を使用した場合、そのサブクエリは存在検査として機能します。 外側のクエリの `WHERE` 句により、このサブクエリから返される行が存在するかどうかがテストされます。 サブクエリは実際にはデータを生成せず、TRUE または FALSE の値を返します。   

EXISTS を使用して導入するサブクエリの構文は、次のとおりです。   

`WHERE [NOT] EXISTS (subquery)`    

次のクエリは、Wheels サブカテゴリに属するすべての製品の名前を検出します。    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

このクエリの結果を理解するには、各製品の名前を順番に考察してください。 その値があるとき、サブクエリから 1 行以上が返されるでしょうか。 つまり、存在検査は TRUE と評価されるでしょうか。   

EXISTS を使用して導入するサブクエリは、他のサブクエリとは次の点で少し違うことに注意してください。 
-   キーワード `EXISTS` の前に、列名、定数、またはその他の式は配置されません。     
-   ほとんどの場合、`EXISTS` で導かれたサブクエリの選択リストはアスタリスク (*) で構成されます。 サブクエリで指定された条件を満たす行が存在するかどうかを検査するだけなので、列名を指定する理由はありません。    

サブクエリを使用しない記述形式で置き換えることのできない場合が多いので、`EXISTS` キーワードは重要です。 EXISTS を使ったクエリの中には他の表現に変えられないものがありますが、多くのクエリでは、IN を使用したり、`ANY` または `ALL` で修飾した比較演算子を使用したりすることにより、同じような結果を得ることができます。     

たとえば、上記のクエリは IN を使用して表現できます。   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```   

### <a name="notexists"></a> NOT EXISTS を使用したサブクエリ
`NOT EXISTS` の機能は `EXISTS` と似ています。ただし、NOT EXISTS が使用されている `WHERE` 句が条件を満たすのは、対応するサブクエリによって返される行がない場合です。    

たとえば、Wheels サブカテゴリに含まれていない製品の名前を検出するには、次のクエリを実行します。   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE NOT EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```   

### <a name="expression"></a> 式の代わりに使われるサブクエリ
[!INCLUDE[tsql](../../includes/tsql-md.md)] では、`SELECT`、`UPDATE`、`INSERT`、`DELETE` の各ステートメントで式が使えるところであればどこでも、サブクエリを式の代わりに使用できます。ただし、`ORDER BY` リストにはサブクエリを使用できません。    

次の例に、この拡張機能の使用方法を示します。 次のクエリにより、すべてのマウンテン バイク製品の価格、平均価格、および各マウンテン バイクの価格と平均価格との差がわかります。    

```sql
USE AdventureWorks2016;
GO
SELECT Name, ListPrice, 
(SELECT AVG(ListPrice) FROM Production.Product) AS Average, 
    ListPrice - (SELECT AVG(ListPrice) FROM Production.Product)
    AS Difference
FROM Production.Product
WHERE ProductSubcategoryID = 1;
GO
```   

## <a name="see-also"></a>参照  
[IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)       
[EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)     
[ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)     
[SOME | ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)     
[結合](../../relational-databases/performance/joins.md)    
[比較演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)       
  
