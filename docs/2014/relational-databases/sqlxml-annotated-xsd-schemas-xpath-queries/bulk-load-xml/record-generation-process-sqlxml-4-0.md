---
title: (SQLXML 4.0) の生成プロセスを記録します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2b43765b03ba42cede8c6879e749f1701f306d1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013342"
---
# <a name="record-generation-process-sqlxml-40"></a>レコードの生成処理 (SQLXML 4.0)
  XML 一括読み込みでは、XML 入力データが処理され、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の適切なテーブルに格納するレコードが用意されます。 XML 一括読み込みのロジックでは、新しいレコードを生成するタイミングと、レコードのフィールドにコピーする子要素および属性値が決定され、完成したレコードを挿入のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信するタイミングが判断されます。  
  
 XML 一括読み込みでは、すべての XML 入力データがメモリに読み込まれるわけではなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にデータが送信される前に完全なレコード セットが作成されるわけではありません。 これは、XML 入力データが大きなドキュメントの場合に、ドキュメント全体をメモリに読み込むと時間がかかる可能性があるためです。 代わりに、XML 一括読み込みでは次の操作が行われます。  
  
1.  マッピング スキーマを分析し、必要な実行プランを準備する。  
  
2.  実行プランを入力ストリームのデータに適用する。  
  
 この順次処理では、決まった方法で XML 入力データを指定することが重要です。 また、XML 一括読み込みでマッピング スキーマがどのように分析されるかと、レコード生成処理がどのように行われるかについて理解しておく必要があります。 これらを理解しておくと、XML 一括読み込みに対し、必要な結果を生成するマッピング スキーマを指定できます。  
  
 XML 一括読み込みでは、注釈により明示的に、または既定のマッピングにより暗黙的に行われる列とテーブルのマッピングを含む一般的なマッピング スキーマ注釈、および結合リレーションシップが処理されます。  
  
> [!NOTE]  
>  注釈付き XSD または XDR マッピング スキーマについて理解していることを前提としています。 スキーマの詳細についてを参照してください[注釈付きの XSD スキーマの概要&#40;SQLXML 4.0&#41; ](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)または[注釈付き XDR スキーマ&#40;SQLXML 4.0 では非推奨&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
 レコード生成を理解するには、次の概念を理解する必要があります。  
  
-   ノードのスコープ  
  
-   レコード生成の規則  
  
-   レコードのサブセットとキーの順序付け規則  
  
-   レコード生成の規則の例外  
  
## <a name="scope-of-a-node"></a>ノードのスコープ  
 XML ドキュメント内のノード (要素または属性) を入力*スコープに*と XML 一括読み込みを検出すると、XML の入力データ ストリームにします。 要素ノードの場合、要素はその開始タグが現れた時点でスコープ内に入ります。 属性ノードの場合、属性はその名前が現れた時点でスコープ内に入ります。  
  
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
  
 スキーマを指定、 **\<お客様 >** を持つ要素 **[得意先コード]** と **[得意先名]** の属性です。 `sql:relation`注釈のマップ、 **\<顧客 >** Customers テーブルに要素。  
  
 次の XML ドキュメントの一部を考えてみます。  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 XML 一括読み込みで、入力用に前の段落で説明したスキーマと XML データが指定された場合、ソース データのノード (要素と属性) は次のように処理されます。  
  
-   最初の開始タグ **\<お客様 >** 要素がスコープ内でその要素を表示します。 このノードは Customers テーブルにマップされます。 したがって、XML 一括読み込みでは Customers テーブルのレコードが生成されます。  
  
-   スキーマのすべての属性で、 **\<お客様 >** [得意先] テーブルの列を要素のマップです。 これらの属性がスコープ内に入ると、XML 一括読み込みでは、これらの値が親スコープで生成された顧客レコードにコピーされます。  
  
-   XML 一括読み込みの終了タグに達したとき、 **\<お客様 >** 要素、要素がスコープ外です。 この時点で、XML 一括読み込みではレコードの準備が完了したと判断され、レコードが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。  
  
 XML 一括ロードごとにこのプロセスに依存してその後 **\<お客様 >** 要素です。  
  
> [!IMPORTANT]  
>  このモデルでは、終了タグに達した (ノードがスコープ外に出た) ときにレコードが挿入されるため、レコードに関連付けるすべてのデータをノードのスコープ内に定義する必要があります。  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>レコードのサブセットとルールの順序付けキー  
 `<sql:relationship>` を使用するマッピング スキーマを指定する場合、サブセットとは、リレーションシップの外部側で生成されたレコード セットを指します。 次の例では、CustOrder レコードが `<sql:relationship>` の外部側になります。  
  
 たとえば、データベースに次のテーブルが含まれているとします。  
  
-   Cust (CustomerID、CompanyName、City)  
  
-   CustOrder (CustomerID、OrderID)  
  
 CustOrder テーブルの CustomerID は、Cust テーブルの CustomerID 主キーを参照する外部キーです。  
  
 ここで、次の注釈付き XSD スキーマで指定される XML ビューを考えてみます。 このスキーマでは、`<sql:relationship>` によって、Cust テーブルと CustOrder テーブルの間のリレーションシップが指定されています。  
  
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
  
-   **\<お客様 >** XML データ ファイル内の要素ノードがスコープ内に入る、XML 一括読み込みは、Cust テーブルのレコードを生成します。 XML 一括ロードから必要な列の値 ([得意先コード]、[得意先名]、および市区町村) にコピーし、  **\<[得意先コード] >** 、  **\<[得意先名] >** 、および **\<市 >** としてこれらの要素の子要素がスコープ内に入力します。  
  
-   **\<注文 >** 要素ノードがスコープ内に入る、XML 一括読み込みには、CustOrder テーブルのレコードが生成されます。 XML 一括読み込みの値をコピーする、 **[受注コード]** 属性のこのレコードにします。 [得意先コード] 列から取得するために必要な値、  **\<[得意先コード] >** の子要素で、 **\<お客様 >** 要素です。 XML 一括読み込みで指定されている情報を使用して`<sql:relationship>`しない限り、このレコードの CustomerID 外部キーの値を取得する、 **CustomerID**で指定された属性、 **\<順序 >** 要素。 一般的な規則としては、子要素で外部キー属性の値が明示的に指定されている場合、XML 一括読み込みではその値が使用され、指定された `<sql:relationship>` によって親要素から値が取得されることはありません。 これと **\<注文 >** 要素ノードがスコープ外に出る、XML 一括読み込みのレコードを送信する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]し、すべての後続処理と **\<注文 >** 要素ノード同様にします。  
  
-   最後に、 **\<お客様 >** 要素ノードがスコープ外に出る。 XML 一括読み込みで顧客レコードが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。 XML 一括読み込みでは、XML データ ストリームの後続の顧客すべてについて、この処理が行われます。  
  
 マッピング スキーマに関しては、次の 2 つの点に注意してください。  
  
-   スキーマが「包含」規則に適合する場合 (顧客と注文書に関連付けられているすべてのデータが関連付けられているスコープ内で定義されているなど、 **\<お客様 >** と **\<順序 >** 要素ノード)、一括読み込みは成功します。  
  
-   説明に、 **\<お客様 >** 要素、その子が適切な順序で要素を指定します。 ここで、  **\<[得意先コード] >** する前に子要素が指定されている、 **\<注文 >** 子要素です。 つまり、入力 XML データ ファイルで、  **\<[得意先コード] >** 要素の値が外部キーとして使用可能な値と、 **\<注文 >** 要素がスコープ内に入る。 キー属性は最初に指定されます。これを "キーの順序付け規則" といいます。  
  
     指定する場合、  **\<[得意先コード] >** 子要素の後に、 **\<注文 >** ときに、子要素の値が使用されない、  **\<注文 >** 要素がスコープ内に入力します。 **\<注文/>** 終了タグが読み取られるし、CustOrder テーブルのレコードを選択し、完了と見なされます [得意先コード] 列で、目的の結果ではありませんに NULL 値を持つ CustOrder テーブルに挿入します。  
  
#### <a name="to-create-a-working-sample"></a>実際のサンプルを作成するには  
  
1.  この例のスキーマを SampleSchema.xml として保存します。  
  
2.  これらのテーブルを作成します。  
  
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
 XML 一括読み込みでは、IDREF または IDREFS 型のノードがスコープ内に入っても、ノードのレコードは生成されません。 スキーマのどこかで、レコードを完全に記述するようにしてください。 IDREFS 型が無視されるのと同様に、`dt:type="nmtokens"` 注釈は無視されます。  
  
 例えば、次の XSD スキーマを記述する **\<お客様 >** と **\<注文 >** 要素です。 **\<お客様 >** 要素が含まれています、 **OrderList** IDREFS 型の属性です。 `<sql:relationship>` タグでは、顧客と注文リストの間の一対多のリレーションシップが指定されています。  
  
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
  
 レコード生成がないので、IDREFS 型のノードを無視して読み込み、ときに、 **OrderList**属性のノードがスコープ内に入る。 このため、注文レコードを Orders テーブルに追加したい場合は、スキーマ内のどこかでこれらの注文を記述する必要があります。 このスキーマで指定する、 **\<注文 >** 要素は、XML 一括ロードが Orders テーブルに注文レコードを追加することにより。 **\<注文 >** 要素は、CustOrder テーブルのレコードを入力するために必要なすべての属性を記述します。  
  
 確認する必要があります、 **[得意先コード]** と **[受注コード]** の値は、 **\<お客様 >** 要素の値に一致、  **\<順序 >** 要素です。 参照の整合性は必ず維持する必要があります。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  これらのテーブルを作成します。  
  
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
  
  
