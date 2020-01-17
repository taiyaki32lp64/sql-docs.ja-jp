---
title: レコード生成処理 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e5b1919afda67f421146d028ef0d5247977175a9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246702"
---
# <a name="record-generation-process-sqlxml-40"></a>レコードの生成処理 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 一括読み込みでは、XML 入力データが処理され、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の適切なテーブルに格納するレコードが用意されます。 XML 一括読み込みのロジックでは、新しいレコードを生成するタイミングと、レコードのフィールドにコピーする子要素および属性値が決定され、完成したレコードを挿入のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信するタイミングが判断されます。  
  
 XML 一括読み込みでは、すべての XML 入力データがメモリに読み込まれるわけではなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にデータが送信される前に完全なレコード セットが作成されるわけではありません。 これは、XML 入力データが大きなドキュメントの場合に、ドキュメント全体をメモリに読み込むと時間がかかる可能性があるためです。 代わりに、XML 一括読み込みでは次の操作が行われます。  
  
1.  マッピング スキーマを分析し、必要な実行プランを準備する。  
  
2.  実行プランを入力ストリームのデータに適用する。  
  
 この順次処理では、決まった方法で XML 入力データを指定することが重要です。 また、XML 一括読み込みでマッピング スキーマがどのように分析されるかと、レコード生成処理がどのように行われるかについて理解しておく必要があります。 これらを理解しておくと、XML 一括読み込みに対し、必要な結果を生成するマッピング スキーマを指定できます。  
  
 XML 一括読み込みでは、注釈により明示的に、または既定のマッピングにより暗黙的に行われる列とテーブルのマッピングを含む一般的なマッピング スキーマ注釈、および結合リレーションシップが処理されます。  
  
> [!NOTE]  
>  注釈付き XSD または XDR マッピング スキーマについて理解していることを前提としています。 スキーマの詳細については、「sqlxml 4.0&#41;または[注釈付き XDR&#41;4.0 &#40;スキーマ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md) [&#40;の注釈付き XSD スキーマの概要](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)」を参照してください。  
  
 レコード生成を理解するには、次の概念を理解する必要があります。  
  
-   ノードのスコープ  
  
-   レコード生成の規則  
  
-   レコードのサブセットとキーの順序付け規則  
  
-   レコード生成の規則の例外  
  
## <a name="scope-of-a-node"></a>ノードのスコープ  
 Xml ドキュメント内のノード (要素または属性) は、xml 一括読み込みで xml 入力データストリームで検出されたときに*スコープ内に*入ります。 要素ノードの場合、要素はその開始タグが現れた時点でスコープ内に入ります。 属性ノードの場合、属性はその名前が現れた時点でスコープ内に入ります。  
  
 要素ノードの場合は終了タグ、属性ノードの場合は属性値の最後に達し、ノードのデータがなくなると、ノードはスコープ外に出ます。  
  
## <a name="record-generation-rule"></a>レコード生成の規則  
 ノード (要素または属性) がスコープ内に入ると、そのノードからレコードを生成できるようになります。 レコードは、関連付けられたノードがスコープ内にある間、存在します。 ノードがスコープ外に出ると、XML 一括読み込みでは生成されたレコードへのデータの格納が完了したと判断され、レコードが挿入のために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。  
  
 たとえば、次の XSD スキーマ フラグメントを考えてみます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このスキーマでは、 **CustomerID**属性と**CompanyName**属性を持つ** \<Customer>** 要素を指定します。 **Sql: relation**注釈は、 ** \<customer>** 要素を Customers テーブルにマップします。  
  
 次の XML ドキュメントの一部を考えてみます。  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 XML 一括読み込みで、入力用に前の段落で説明したスキーマと XML データが指定された場合、ソース データのノード (要素と属性) は次のように処理されます。  
  
-   最初** \<の Customer>** 要素の開始タグによって、その要素がスコープ内に表示されます。 このノードは Customers テーブルにマップされます。 したがって、XML 一括読み込みでは Customers テーブルのレコードが生成されます。  
  
-   スキーマでは、 ** \<Customer>** 要素のすべての属性が Customers テーブルの列にマップされます。 これらの属性がスコープ内に入ると、XML 一括読み込みでは、これらの値が親スコープで生成された顧客レコードにコピーされます。  
  
-   XML 一括読み込みが** \<Customer>** 要素の終了タグに達すると、要素はスコープ外になります。 この時点で、XML 一括読み込みではレコードの準備が完了したと判断され、レコードが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。  
  
 XML 一括読み込みでは、後続** \<の Customer>** 要素ごとにこのプロセスに従います。  
  
> [!IMPORTANT]  
>  このモデルでは、終了タグに達した (ノードがスコープ外に出た) ときにレコードが挿入されるため、レコードに関連付けるすべてのデータをノードのスコープ内に定義する必要があります。  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>レコードのサブセットとキーの順序付け規則  
 ** \<Sql: relationship>** を使用するマッピングスキーマを指定すると、リレーションシップの外部側で生成されるレコードのセットがサブセット用語によって参照されます。 次の例では、custorder レコードが外部側、 ** \<sql: relationship>** にあります。  
  
 たとえば、データベースに次のテーブルが含まれているとします。  
  
-   Cust (CustomerID、CompanyName、City)  
  
-   CustOrder (CustomerID、OrderID)  
  
 CustOrder テーブルの CustomerID は、Cust テーブルの CustomerID 主キーを参照する外部キーです。  
  
 ここで、次の注釈付き XSD スキーマで指定される XML ビューを考えてみます。 このスキーマでは、 ** \<sql: relationship>** を使用して、Cust テーブルと custorder テーブル間のリレーションシップを指定します。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 サンプル XML データと、実際のサンプルを作成する手順は次のとおりです。  
  
-   Xml データファイル内の** \<Customer>** 要素ノードがスコープ内に入ると、xml 一括読み込みでは Cust テーブルのレコードが生成されます。 次に、XML 一括読み込みでは、必要な列の値 (customerid、companyname、および city) を** \<customerid>**、 ** \<companyname>**、および** \<city>** 子要素からコピーします。これらの要素は、これらの要素がスコープ内に入ります。  
  
-   ** \<Order>** 要素ノードがスコープ内に入ると、XML 一括読み込みでは custorder テーブルのレコードが生成されます。 XML 一括読み込みでは、 **OrderID**属性の値がこのレコードにコピーされます。 Customerid 列に必要な値は、 ** \<Customer>** 要素の** \<customerid>** 子要素から取得されます。 XML 一括読み込みでは、 ** \<Order>** 要素で**customerid**属性が指定されていない限り、 ** \<sql: relationship>** で指定されている情報を使用して、このレコードの customerid 外部キー値を取得します。 一般的な規則として、子要素が外部キー属性の値を明示的に指定すると、XML 一括読み込みではその値が使用され、指定した** \<sql: relationship>** を使用して親要素から値が取得されません。 この** \<順序>** 要素ノードがスコープ外になると、XML 一括読み込みではレコード[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]がに送信され、後続** \<** のすべての order>要素ノードが同じ方法で処理されます。  
  
-   最後に、 ** \<Customer>** element ノードがスコープ外に出ます。 XML 一括読み込みで顧客レコードが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。 XML 一括読み込みでは、XML データ ストリームの後続の顧客すべてについて、この処理が行われます。  
  
 マッピング スキーマに関しては、次の 2 つの点に注意してください。  
  
-   スキーマが "含有" ルールを満たす場合 (たとえば、顧客と注文に関連付けられているすべてのデータが、関連付けられて** \<いる顧客の>** および** \<注文>** 要素ノードのスコープ内で定義されている場合)、一括読み込みは成功します。  
  
-   ** \<Customer>** 要素の記述では、その子要素が適切な順序で指定されます。 この場合は、 ** \<CustomerID>** 子要素が** \<順序>** 子要素の前に指定されています。 これは、入力 XML データファイルで、 ** \<Order>** 要素がスコープ内に入るときに、 ** \<CustomerID>** 要素の値を外部キー値として使用できることを意味します。 キー属性は最初に指定されます。これを "キーの順序付け規則" といいます。  
  
     Order>子要素の** \<後に CustomerID>** 子要素を指定した場合、 ** \<order>** 要素がスコープ内に入るときに値は使用できません。 ** \<** 次に、 ** \</order>** 終了タグが読み取られると、custorder テーブルのレコードは完了したと見なされ、custorder テーブルに挿入されます。このテーブルには、CustomerID 列に NULL 値が挿入されますが、これは目的の結果ではありません。  
  
#### <a name="to-create-a-working-sample"></a>実際のサンプルを作成するには  
  
1.  この例のスキーマを SampleSchema.xml として保存します。  
  
2.  次のテーブルを作成します。  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  次のサンプル XML 入力データを SampleXMLData.xml として保存します。  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  XML 一括読み込みを実行するには、次の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) の例 (BulkLoad.vbs) を保存し、実行します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>レコード生成の規則の例外  
 XML 一括読み込みでは、IDREF または IDREFS 型のノードがスコープ内に入っても、ノードのレコードは生成されません。 スキーマのどこかで、レコードを完全に記述するようにしてください。 IDREFS 型が無視されるのと同様に、 **dt: type = "nmtokens"** 注釈は無視されます。  
  
 たとえば、 ** \<顧客の>** と** \<注文>** 要素を記述する次の XSD スキーマについて考えてみます。 ** \<Customer>** 要素には、IDREFS 型の**orderlist**属性が含まれています。 ** \<Sql: relationship>** タグは、顧客と注文リストの間の一対多リレーションシップを指定します。  
  
 スキーマは次のようになります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
                 parent="Cust"  
                 parent-key="CustomerID"  
                 child="CustOrder"  
                 child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 一括読み込みでは IDREFS 型のノードが無視されるため、 **Orderlist**属性ノードがスコープ内に入ってもレコードは生成されません。 このため、注文レコードを Orders テーブルに追加したい場合は、スキーマ内のどこかでこれらの注文を記述する必要があります。 このスキーマでは、 ** \<order>** 要素を指定することで、XML 一括読み込みで Orders テーブルに注文レコードが追加されるようになります。 Order>要素には、custorder テーブルのレコードを埋めるために必要なすべての属性が記述されています。 ** \<**  
  
 Customer>要素の**CustomerID**と**OrderID**の値が** \<Order>** 要素の値と一致していることを確認する必要があります。 ** \<** 参照の整合性は必ず維持する必要があります。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  次のテーブルを作成します。  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  この例のマッピング スキーマを SampleSchema.xml として保存します。  
  
3.  次のサンプル XML データを SampleXMLData.xml として保存します。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  XML 一括読み込みを実行するには、次の VBScript の例 (SampleVB.vbs) を保存し実行します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
