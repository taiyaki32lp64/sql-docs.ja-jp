---
title: 入れ子になった AUTO モードのクエリを使用した兄弟の生成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0db2a84b4be80fffec0f05aed11f39a3bcea7db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287357"
---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>入れ子になった AUTO モードのクエリを使用した兄弟の生成
  次の例では、入れ子になった AUTO モードのクエリを使用して兄弟を作成する方法を示します。 他の方法では、EXPLICIT モードを使用する以外に、このような XML を生成する方法はありません。 ただし、この方法は複雑になる場合があります。  
  
## <a name="example"></a>例  
 このクエリでは、販売注文情報を提供する XML が構築されます。 これには、次の内容が含まれます。  
  
-   販売注文ヘッダー情報、 `SalesOrderID`、 `SalesPersonID`、および `OrderDate`。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] の `SalesOrderHeader` テーブルにこの情報が格納されています。  
  
-   販売注文明細情報。 注文を受けた 1 つ以上の製品、単価、および受注数が含まれます。 この情報は `SalesOrderDetail` テーブルに格納されています。  
  
-   販売員情報。 これは注文を受けた販売員です。 `SalesPerson` は、 `SalesPersonID`テーブルで提供されています。 このクエリでは、販売員の名前を検索するために、このテーブルと `Employee` テーブルを結合する必要があります。  
  
 次に示す 2 つの異なる `SELECT` クエリは、やや形式の異なる XML を生成します。  
  
 最初のクエリで生成される XML では、<`SalesPerson`> と <`SalesOrderHeader`> は <`SalesOrder`> の子の兄弟として示されます。  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 上のクエリで、最も外側の `SELECT` ステートメントについて説明します。  
  
-   `SalesOrder` 句で指定された行セット `FROM` に対してクエリを実行しています。 結果は、1 つ以上の <`SalesOrder`> 要素を含む XML になります。  
  
-   `AUTO` モードと `TYPE` ディレクティブが指定されています。 `AUTO` モードを XML にクエリ結果を変換して、`TYPE`ディレクティブは、結果として返します`xml`型。  
  
-   2 つの `SELECT` ステートメントが含まれており、コンマで区切られ、入れ子構造になっています。 入れ子の最初の `SELECT` ステートメントで、販売注文情報、ヘッダー、および明細を取得し、入れ子の 2 番目の `SELECT` ステートメントで販売員情報を取得しています。  
  
    -   `SELECT` 、 `SalesOrderID`、および `SalesPersonID`自体を取得する `CustomerID` ステートメントには、販売注文明細情報を返す別の `SELECT ... FOR XML` ステートメント ( `AUTO` モードと `TYPE` ディレクティブを指定) が入れ子として含まれています。  
  
 販売員情報を取得する `SELECT` ステートメントは、 `SalesPerson`句で作成された行セット `FROM` に対してクエリを行います。 `FOR XML` クエリが機能するためには、 `FROM` 句で生成される匿名の行セットに名前を付ける必要があります。 ここで指定されている名前は `SalesPerson`です。  
  
 結果の一部を次に示します。  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 次のクエリでは、同じ販売注文情報が生成されます。ただし、結果の XML では、<`SalesPerson`> は <`SalesOrderDetail`> の兄弟として示されます。  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 クエリは次のとおりです。  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 結果を次に示します。  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 `TYPE` ディレクティブによってクエリの結果が `xml` 型で返されるので、各種の `xml` データ型メソッドを使用して結果の XML にクエリを実行できます。 詳細については、「 [xml データ型のメソッド](/sql/t-sql/xml/xml-data-type-methods)」を参照してください。 次のクエリでは、次の点に注意してください。  
  
-   上記のクエリが `FROM` 句に追加されています。 クエリの結果はテーブルで返されます。 追加された `XmlCol` 別名に注意してください。  
  
-   `SELECT` 句では、 `XmlCol` 句で返される `FROM` に対して XQuery を指定しています。 XQuery の指定では、`query()` データ型の `xml` メソッドを使用しています。 詳細については、「[クエリ&#40;&#41; メソッド &#40;xml データ型&#41;](/sql/t-sql/xml/query-method-xml-data-type)」を参照してください。  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>参照  
 [入れ子になった FOR XML クエリの使用](use-nested-for-xml-queries.md)  
  
  
