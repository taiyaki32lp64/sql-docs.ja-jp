---
title: XML アップデートグラムを使用したデータの挿入 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: caf6c6bc9e9807b042baf365c3a1efbe9d2b74c5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252499"
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>XML アップデートグラムを使用した、データの挿入 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  アップデートグラムは、レコードインスタンスが** \<after>** ブロックに存在していても、対応** \<する before>** ブロックに含まれていない場合に挿入操作を示します。 この場合、アップデートグラムでは、 ** \<after>** ブロックにレコードをデータベースに挿入します。  
  
 挿入操作のアップデートグラムの形式は次のとおりです。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<> ブロックの前  
 挿入操作では、 ** \<before>** ブロックを省略できます。 省略可能な**マッピングスキーマ**属性が指定されていない場合、アップデートグラムで指定した** \<ElementName>** はデータベーステーブルにマップされ、子要素または属性はテーブル内の列にマップされます。  
  
## <a name="after-block"></a>\<> ブロックの後  
 ** \<After>** ブロックに1つ以上のレコードを指定できます。  
  
 After>ブロックが特定の列の値を提供しない場合、アップデートグラムは注釈付きスキーマで指定された既定値を使用します (スキーマが指定されている場合)。 ** \<** スキーマで列の既定値が指定されていない場合、アップデートグラムではこの列に明示的な値が指定され[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ず、代わりに、この列に既定値 (指定されている場合) が割り当てられます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定値がなく、列で NULL 値が許容される場合、アップデートグラムでは列値に NULL が設定されます。 列に既定値がなく NULL 値が許容されない場合、コマンドは失敗し、アップデートグラムではエラーが返されます。 省略可能な**updg: returnid**属性を使用して、id 型の列を含むテーブルにレコードが追加されたときにシステムによって生成される id 値を返します。  
  
## <a name="updgid-attribute"></a>updg:id 属性  
 アップデートグラムでレコードのみを挿入する場合、アップデートグラムで**updg: id**属性は必要ありません。 **Updg: id**の詳細については、「 [XML アップデートグラムを使用したデータの更新 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)」を参照してください。  
  
## <a name="updgat-identity-attribute"></a>updg:at-identity 属性  
 アップデートグラムで、ID 型の列を含むテーブルにレコードを挿入すると、オプションの**updg: identity**属性を使用して、システムに割り当てられた値をキャプチャできます。 キャプチャした値は、後続のアップデートグラム操作で使用できます。 アップデートグラムの実行時に、 **updg: returnid**属性を指定することによって生成される id 値を返すことができます。  
  
## <a name="updgguid-attribute"></a>updg:guid 属性  
 **Updg: guid**属性は、グローバル一意識別子を生成する省略可能な属性です。 この値は、指定されている** \<同期>** ブロック全体のスコープ内に残ります。 この値は、 ** \<同期>** ブロックの任意の場所で使用できます。 属性は、一意の識別子を生成するために**newguid ()** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]関数を呼び出します。  
  
## <a name="examples"></a>例  
 次の例を使用して実際のサンプルを作成するには、 [SQLXML の例を実行するための要件](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)を満たす必要があります。  
  
 アップデートグラムの例を使用する前に、次の点に注意してください。  
  
-   ほとんどの例では、アップデートグラムでマッピング スキーマを指定せず、既定のマッピングを使用します。 マッピングスキーマを使用するアップデートグラムの例については、「[アップデートグラムでの注釈付きマッピングスキーマの指定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)」を参照してください。  
  
-   ほとんどの例では、[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] サンプル データベースを使用します。 すべての更新内容は、このデータベースのテーブルに適用されます。  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. アップデートグラムを使用してレコードを挿入する  
 この属性中心のアップデートグラムでは、[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベース内の HumanResources.Employee テーブルにレコードを挿入します。  
  
 この例では、アップデートグラムでマッピングスキーマが指定されていません。 したがって、アップデートグラムでは既定のマッピングが使用されます。このマッピングでは、要素名はテーブル名にマップされ、属性または子要素はそのテーブル内の列にマップされます。  
  
 HumanResources.Department テーブルに対する [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] スキーマでは、すべての列に 'not null' 制限が設定されます。 したがって、アップデートグラムには、すべての列に指定する値を含める必要があります。 DepartmentID は IDENTITY 型の列であり、 値は指定しません。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 MyUpdategram.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 要素中心のマッピングの場合、アップデートグラムは次のようになります。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 要素中心と属性中心の混合モードのアップデートグラムでは、次のアップデートグラムのように、要素に属性と副要素の両方を含めることができます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>B. アップデートグラムを使用して複数のレコードを挿入する  
 このアップデートグラムでは、HumanResources.Shift テーブルに 2 つの新しい勤務時間レコードを追加します。 アップデートグラムでは、省略可能** \<な before>** ブロックが指定されていません。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 Updategram-AddShifts.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 この例の別のバージョンは、2つの従業員を挿入するために1つのブロックではなく** \<、** 2 つの>ブロックを使用するアップデートグラムです。 これは有効であり、次のようにエンコードできます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. SQL Server で有効で、XML では有効でない文字を処理する  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、テーブル名は、Northwind データベースの Order Details テーブルのようにスペースを含めて指定できます。 ただし、有効な[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]識別子である xml 文字では有効ではありませんが、有効な xml 識別子は\_\_エンコード値として ' __xHHHH ' を使用してエンコードできます。ここで、HHHH は、最上位ビットから順に、文字の4桁の16進数の UCS 2 コードを表します。  
  
> [!NOTE]  
>  この例では Northwind データベースを使用します。 この[Microsoft Web サイト](https://www.microsoft.com/download/details.aspx?id=23654)からダウンロードできる SQL スクリプトを使用して、Northwind データベースをインストールできます。  
  
 要素名も、角かっこ ([ ]) で囲む必要があります。 文字 [および] は XML では有効でないため、それぞれを _x005B\_としてエンコード\_し、_x005D する必要があります。 マッピング スキーマを使用して、空白文字など有効でない文字を含まない要素名を指定することもできます。 この場合、マッピング スキーマで必要なマッピングが行われるので、これらの文字をエンコードする必要はありません。  
  
 次のアップデートグラムでは、Northwind データベースの Order Details テーブルにレコードを追加します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Order Details テーブルの UnitPrice 列は**money**型です。 適切な型変換を (**文字列**型から**money**型に) 適用するには、ドル記号 ($) を値の一部として追加する必要があります。 アップデートグラムでマッピングスキーマが指定されていない場合は、**文字列**値の最初の文字が評価されます。 最初の文字がドル記号 ($) の場合、適切な変換が行われます。  
  
 列が**dt: type = "fixed. 14.4"** または**sql: datatype = "money"** のいずれかとして適切にマークされているマッピングスキーマに対してアップデートグラムを指定した場合、ドル記号 ($) は必要なく、マッピングによって変換が処理されます。 適切な型変換が行われるようにするには、この方法が推奨されます。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 UpdategramSpacesInTableName.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. at-identity 属性を使用して、IDENTITY 型の列に挿入されている値を取得する  
 次のアップデートグラムでは、Sales.SalesOrderHeader テーブルと Sales.SalesOrderDetail テーブルに 1 つずつ、合計 2 つのレコードを挿入します。  
  
 このアップデートグラムでは、最初にレコードを Sales.SalesOrderHeader テーブルに追加します。 このテーブルで、SalesOrderID 列は IDENTITY 型の列です。 このため、このレコードをテーブルに追加すると、アップデートグラムでは、 **id**属性を使用して、割り当てられた salesorderid 値を "x" (プレースホルダー値) としてキャプチャします。 次に、updat> SalesOrderDetail 要素の SalesOrderID 属性\<の値として、この**at id**変数を指定します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 **Updg: at identity**属性によって生成された id 値を返す場合は、 **updg: returnid**属性を使用できます。 次のアップデートグラムは、この ID 値を返すように変更されたものです。 例を少し複雑にするため、ここでは 2 つの注文レコードと 2 つの注文詳細レコードを追加します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 アップデートグラムを実行すると、次のような結果が返されます。この結果には、生成された ID 値 (テーブル ID に使用される ShiftID 列の生成値) が含まれます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 Updategram-returnId.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. updg:guid 属性を使用して一意な値を生成する  
 この例のアップデートグラムでは、Cust および CustOrder テーブルにレコードを挿入します。 また、アップデートグラムでは、 **updg: guid**属性を使用して CustomerID 属性の一意の値が生成されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 アップデートグラムでは、 **returnid**属性が指定されています。 結果として、生成された GUID が返されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 Updategram-GenerateGuid.xml として保存します。  
  
2.  次のテーブルを作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. アップデートグラムでスキーマを指定する  
 この例のアップデートグラムでは、レコードを次のテーブルに挿入します。  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 このアップデートグラムでは XSD スキーマを指定しています。アップデートグラム要素と属性に既定のマッピングはありません。 このスキーマでは、要素および属性からデータベース テーブルおよび列への必要なマッピングが提供されます。  
  
 次のスキーマ (custorderschema .xml) は、 **OrderID**属性と**EmployeeID**属性で構成される** \<custorder>** 要素を記述します。 スキーマをさらに興味深いものにするため、 **EmployeeID**属性には既定値が割り当てられています。 アップデートグラムでは、属性の既定値は、アップデートグラムでその属性が指定されていない挿入操作のみに使用されます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このアップデートグラムでは、CustOrder テーブルにレコードを挿入します。 このアップデートグラムでは OrderID および EmployeeID 属性の値のみを指定し、 OrderType 属性の値は指定しません。 したがって、アップデートグラムでは、前のスキーマで指定されている EmployeeID 属性の既定値が使用されます。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 マッピングスキーマを指定するアップデートグラムの例については、「[アップデートグラムでの注釈付きマッピングスキーマの指定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)」を参照してください。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  **Tempdb**データベースに次のテーブルを作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  上のスキーマをコピーして、テキスト ファイルに貼り付け、 CustOrderSchema.xml として保存します。  
  
3.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 上の手順と同じフォルダーに CustOrderUpdategram.xml として保存します。  
  
4.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. xsi:nil 属性を使用して列に null 値を挿入する  
 テーブルの対応する列に null 値を挿入する場合は、アップデートグラムの要素に対して**xsi: nil**属性を指定できます。 対応する XSD スキーマでは、XSD **nillable**属性も指定する必要があります。  
  
 たとえば、次の XSD スキーマを考えてみます。  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 XSD スキーマでは、 ** \<fname>** 要素に**nillable = "true"** が指定されています。 このスキーマを使用するアップデートグラムは次のとおりです。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 このアップデートグラムでは、 ** \<after>** ブロックの** \<fname>** 要素に**xsi: nil**が指定されています。 したがって、このアップデートグラムを実行すると、テーブルの first_name 列に NULL 値が挿入されます。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  次のテーブルを**tempdb**データベースに作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  上のスキーマをコピーして、テキスト ファイルに貼り付け、 StudentSchema.xml として保存します。  
  
3.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 上の手順の StudentSchema.xml と同じフォルダーに StudentUpdategram.xml として保存します。  
  
4.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. アップデートグラムで名前空間を指定する  
 アップデートグラム内の要素で名前空間を宣言し、その名前空間に属する要素として、同じ要素を保持することができます。 この場合、対応するスキーマで同じ名前空間を宣言する必要があり、対象の名前空間に要素が属している必要があります。  
  
 たとえば、次のアップデートグラム (updategram-elementhavingnamespace.xml) では、 ** \<Order>** 要素は、要素で宣言された名前空間に属します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="https://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 この場合、このスキーマに示すように、スキーマでも名前空間を宣言する必要があります。  
  
 次のスキーマ (XSD-ElementHavingNamespace.xml) では、対応する要素と属性の宣言方法を示しています。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="https://server/xyz/schemas/"   
     targetNamespace="https://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のスキーマをコピーして、テキスト ファイルに貼り付け、 XSD-ElementHavingNamespace.xml として保存します。  
  
2.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 XSD-ElementHavingnamespace.xml と同じフォルダーに Updategram-ElementHavingNamespace.xml として保存します。  
  
3.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>I. XML データ型列にデータを挿入する  
 **Xml**データ型はで[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]導入されました。 アップデートグラムを使用して、 **xml**データ型の列に格納されているデータを挿入および更新するには、次のように準備します。  
  
-   **Xml**列は、既存の行を識別するためには使用できません。 そのため、アップデートグラムの「 **updg: before** 」セクションには含めることができません。  
  
-   **Xml**列に挿入された xml フラグメントのスコープ内にある名前空間は保持され、その名前空間宣言は挿入されたフラグメントの最上位要素に追加されます。  
  
 たとえば、次のアップデートグラム (sampleupdategram .xml) では、 ** \<Desc>** 要素によって、 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]サンプルデータベースの Production>productdescription テーブルの productdescription 列が更新されます。 このアップデートグラムの結果として、productdescription 列の xml コンテンツが** \<Desc>** 要素の xml コンテンツに更新されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 このアップデートグラムでは、次の注釈付き XSD スキーマ (SampleSchema.xml) を参照しています。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のスキーマをコピーして、テキスト ファイルに貼り付け、 XSD-SampleSchema.xml として保存します。  
  
    > [!NOTE]  
    >  アップデートグラムでは既定のマッピングがサポートされているため、 **xml**データ型の先頭と末尾を識別する方法はありません。 これは実質的に、 **xml**データ型の列を含むテーブルを挿入または更新するときにマッピングスキーマが必要であることを意味します。 スキーマを指定しない場合、SQLXML では、テーブル内の列の 1 つが見つからないというエラーが返されます。  
  
2.  上のアップデートグラムをコピーして、テキスト ファイルに貼り付け、 SampleSchema.xml と同じフォルダーに SampleUpdategram.xml として保存します。  
  
3.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
