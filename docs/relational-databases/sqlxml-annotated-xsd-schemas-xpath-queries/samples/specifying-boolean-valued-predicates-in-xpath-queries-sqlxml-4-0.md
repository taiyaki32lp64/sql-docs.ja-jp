---
title: XPath クエリでのブール述語の指定 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- nested predicates
- successive predicates
- predicates [SQLXML]
- top-level predicates
- Boolean-valued predicates
- multiple predicates
ms.assetid: 5f6e7219-6911-4bca-a54b-56b95e0b43dd
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: acf43b7fd863690259719a81ec60b136f9f4996d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252564"
---
# <a name="specifying-boolean-valued-predicates-in-xpath-queries-sqlxml-40"></a>XPath クエリでのブール値述語の指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以下の例では、XPath クエリにブール値述語を指定する方法を示します。 これらの例では、SampleSchema1.xml に格納されているマッピング スキーマに対して XPath クエリを指定しています。 このサンプルスキーマの詳細については、「 [XPath のサンプルの注釈付き XSD スキーマの例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-specify-multiple-predicates"></a>A. 複数の述語を指定する  
 次の XPath クエリでは、複数の述語を使用して、任意の注文 ID と顧客 ID の注文情報を検索します。  
  
```  
/child::Customer[attribute::CustomerID="1"]/child::Order[attribute::OrderID="Ord-43860"]  
```  
  
 `attribute`軸 (@) へのショートカットを指定できます。 `child`軸が既定値であるため、クエリから省略できます。  
  
```  
/Customer[@CustomerID="1"]/Order[@SalesOrderID="Ord-43860"]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  [サンプルスキーマコード](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)をコピーし、テキストファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (BooleanValuedPredicatesA.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="1"]/Order[@SalesOrderID="Ord-43860"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  

     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
     次に結果を示します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <Order SalesOrderID="Ord-43860" SalesPersonID="280" OrderDate="2001-08-01T00:00:00" DueDate="2001-08-13T00:00:00" ShipDate="2001-08-08T00:00:00">  
        <OrderDetail ProductID="Prod-729" UnitPrice="226.8571" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-738" UnitPrice="220.2496" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-761" UnitPrice="503.3507" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-762" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-763" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-765" UnitPrice="503.3507" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-768" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-770" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
      </Order>  
    </ROOT>  
    ```  
  
### <a name="b-specify-successive-and-nested-predicates"></a>B. 連続する述語を入れ子で指定する  
 次のクエリでは、述語を連続して使用しています。 このクエリでは、 **SalesPersonID**属性の値が277で、 **TerritoryID**属性の値が3である、コンテキストノードのすべての** \<顧客>** 子要素が返されます。  
  
```  
/child::Customer[attribute::SalesPersonID="277"][attribute::TerritoryID="3"]  
```  
  
 このクエリでは、述語で指定された両方の条件を満たす要素** \<>顧客**が返されます。  
  
 **属性**軸 (@) へのショートカットを指定できます。また、**子**軸が既定値であるため、クエリから省略できます。  
  
```  
/Customer[@SalesPersonID="277"][@TerritoryID="3"]  
```  
  
 次の XPath クエリでは、述語を入れ子にして使用しています。 このクエリは、 **SalesPersonID**属性の値が2である order ** \<>** 要素を少なくとも1つ持つ子要素** \<>order**を含むコンテキストノードのすべての** \<顧客>** 子要素を返します。  
  
```  
/Customer[Order[@SalesPersonID=2]]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  [サンプルスキーマコード](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)をコピーし、テキストファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (nestedSuccessive.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
             /Customer[@SalesPersonID="277"][@TerritoryID="3"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 次は結果の一部です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="22" SalesPersonID="277" TerritoryID="3"   
            AccountNumber="22" CustomerType="S"   
            Orders="Ord-43874 Ord-44519 Ord-46989 Ord-48013 Ord-49130 Ord-50274 Ord-51807 Ord-57113 Ord-63162 Ord-69495">  
    <Order SalesOrderID="Ord-43874" SalesPersonID="277"   
           OrderDate="2001-08-01T00:00:00"   
           DueDate="2001-08-13T00:00:00"   
           ShipDate="2001-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
                   OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    ...  
  </Customer>  
  <Customer CustomerID="39" SalesPersonID="277" TerritoryID="3"   
            AccountNumber="39" CustomerType="S"   
            Orders="Ord-47428 Ord-48367 Ord-49529 Ord-50742 Ord-53591 Ord-59051 Ord-65301 Ord-71912">    <Order SalesOrderID="Ord-47428" SalesPersonID="277"   
           OrderDate="2002-09-01T00:00:00"   
           DueDate="2002-09-13T00:00:00"   
           ShipDate="2002-09-08T00:00:00">  
      <OrderDetail ProductID="Prod-759" UnitPrice="563.7528" OrderQty="2" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-769" UnitPrice="563.7528" OrderQty="1" UnitPriceDiscount="0" />   
      ...  
    </Order>  
    ...  
  </Customer>  
  ...  
</ROOT>  
```  
  
### <a name="c-specify-a-top-level-predicate"></a>C. 最上位の述語を指定する  
 次のクエリでは、 ** \<Order>** 要素の子を持つコンテキストノードの子要素ノード** \<>Customer**が返されます。 このクエリでは、ロケーション パスを最上位の述語としてテストします。  
  
```  
/child::Customer[child::Order]  
```  
  
 **子**軸が既定値です。 そのため、クエリは次のように指定できます。  
  
```  
/Customer[Order]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  [サンプルスキーマコード](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)をコピーし、テキストファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (TopLevelPredicate.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 次に結果の一部を示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" SalesPersonID="280" TerritoryID="1" AccountNumber="1" CustomerType="S" Orders="Ord-43860 Ord-44501 Ord-45283 Ord-46042">  
    <Order SalesOrderID="Ord-43860" SalesPersonID="280" OrderDate="2001-08-01T00:00:00" DueDate="2001-08-13T00:00:00" ShipDate="2001-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-729" UnitPrice="226.8571" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-738" UnitPrice="220.2496" OrderQty="1" UnitPriceDiscount="0" />   
      ...  
    </Order>  
    <Order SalesOrderID="Ord-44501" SalesPersonID="280" OrderDate="2001-11-01T00:00:00" DueDate="2001-11-13T00:00:00" ShipDate="2001-11-08T00:00:00">  
      <OrderDetail ProductID="Prod-725" UnitPrice="226.8571" OrderQty="3" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-726" UnitPrice="226.8571" OrderQty="2" UnitPriceDiscount="0" />   
      ...  
    </Order>    ...  
  </Customer>  
  ...  
</ROOT>  
```  
  
  
