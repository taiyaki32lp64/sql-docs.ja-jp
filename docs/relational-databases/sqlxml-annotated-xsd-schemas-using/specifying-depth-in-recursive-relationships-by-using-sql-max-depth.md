---
title: 'Sql を使用した再帰的な深さのリレーションシップの設定: 最大深度'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aaeeae8c0adfc34c80b986898c5209b744d7efc4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257353"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>sql:max-depth を使用した、再帰リレーションシップの深さの指定
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  リレーショナル データベースでは、テーブルのリレーションシップにそのテーブル自身が含まれることを、再帰リレーションシップと呼びます。 たとえば、監督者と被監督者のリレーションシップでは、従業員の記録を格納するテーブルのリレーションシップに、そのテーブル自身が含まれます。 この場合、従業員テーブルはリレーションシップの 1 つの側では監督者となり、別の側では被監督者となります。  
  
 マッピング スキーマには、要素とその先祖が同じ型の再帰リレーションシップを含めることができます。  
  
## <a name="example-a"></a>例 A  
 次のテーブルを考えてみます。  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 このテーブルでは、ReportsTo 列にマネージャーの従業員 ID が格納されています。  
  
 ここで従業員の XML 階層を生成して、次のサンプル XML フラグメントに示すように、マネージャーである従業員を階層の一番上に、マネージャーに報告を行う従業員をそれに対応する階層に表示したいとします。 このフラグメントが示すのは、employee 1 の*再帰ツリー*です。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 このフラグメントでは、従業員 5 が従業員 4、従業員 4 が従業員 3 に、従業員 3 と 2 は従業員 1 に報告を行います。  
  
 この結果を生成するには、次の XSD スキーマを使用して、これに対する XPath クエリを指定できます。 このスキーマでは、user.employeetype 型の** \<emp>** 要素が記述されています。これは、同じ型 user.employeetype の子要素である** \<emp>** で構成されます。 これは、要素とその先祖が同じ型の再帰リレーションシップです。 また、スキーマでは、 ** \<sql: relationship>** を使用して、スーパーバイザーと被監督者の間の親子リレーションシップを記述します。 この** \<sql: relationship>** では、Emp は親と子の両方のテーブルであることに注意してください。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 このリレーションシップは再帰的なので、何らかの方法でスキーマ内の再帰の深さを指定する必要があります。 指定しない場合、結果は無限再帰となり、従業員から次の従業員へと無限に報告を行うことになります。 **Sql: max depth**注釈を使用すると、再帰の深さを指定できます。 この特定の例では、 **sql: max depth**の値を指定するために、会社で管理階層がどの程度深くなっているかを把握している必要があります。  
  
> [!NOTE]  
>  スキーマでは**sql: limit-field**注釈が指定されていますが、 **sql: limit-value**注釈は指定されていません。 これにより、結果として生成される階層の一番上のノードは、だれにも報告しない従業員だけになります  (ReportsTo は NULL です)。**Sql: limit-field**を指定し、 **sql: limit-value** (既定値は NULL) を指定しない場合、注釈はこれを実行します。 生成される XML に、可能なすべてのレポートツリー (テーブル内のすべての従業員のレポートツリー) を含めるには、スキーマから**sql: limit-field**注釈を削除します。  
  
> [!NOTE]  
>  次の手順では、tempdb データベースを使用します。  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  仮想ルートが示す tempdb データベースに、Emp という名前のサンプル テーブルを作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 maxDepth.xml として保存します。  
  
4.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 maxDepth.xml を保存したディレクトリに maxDepthT.xml としてファイルを保存します。 このテンプレートのクエリでは、Emp テーブル内のすべての従業員が返されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (maxDepth.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。 詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  

 結果を次に示します。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  結果内の階層の深さが異なる場合は、スキーマ内の**sql: max depth**注釈の値を変更し、各変更後に再びテンプレートを実行します。  
  
 前のスキーマでは、すべての** \<Emp>** 要素は、まったく同じ属性のセット (**EmployeeID**、 **FirstName**、および**LastName**) を持っていました。 次のスキーマは、マネージャーに報告するすべての** \<Emp>** 要素に対して、追加の**ReportsTo**属性を返すように若干変更されています。  
  
 たとえば、次の XML フラグメントでは、従業員 1 の部下が示されています。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 変更後のスキーマは次のようになります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>sql:max-depth 注釈  
 再帰リレーションシップで構成されるスキーマでは、スキーマ内に再帰の深さを明示的に指定する必要があります。 これは、対応する FOR XML EXPLICIT クエリを正常に作成し、要求された結果を返すために必要です。  
  
 スキーマで説明されている再帰的なリレーションシップの再帰の深さを指定するには、スキーマで**sql: max depth**注釈を使用します。 **Sql: max depth**注釈の値は、再帰の数を示す正の整数 (1 ~ 50) です。値1は、 **sql: max depth**注釈が指定されている要素の再帰を停止します。値が2の場合、 **sql: max depth**が指定されている要素から次のレベルで再帰が停止します。などなど。  
  
> [!NOTE]  
>  基になる実装では、マッピングスキーマに対して指定された XPath クエリは、SELECT...FOR XML EXPLICIT クエリ。 このクエリでは、再帰に有限の深さを指定する必要があります。 **Sql: max depth**に指定する値が大きいほど、生成される FOR XML EXPLICIT クエリのサイズが大きくなります。 これによって、取得に時間がかかることがあります。  
  
> [!NOTE]  
>  アップデートグラムと XML 一括読み込みでは、max-depth 注釈は無視されます。 つまり、再帰更新や再帰挿入は、max-depth に指定されている値に関係なく行われます。  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>複合要素での sql:max-depth の指定  
 **Sql: max depth**注釈は、任意の複合コンテンツ要素で指定できます。  
  
### <a name="recursive-elements"></a>再帰要素  
 場合**sql: 最大深度**が親要素と子要素の両方に再帰リレーションシップで指定されている場合、親で指定された**sql: の最大深度**注釈が優先されます。 たとえば、次のスキーマでは、親と子の両方の employee 要素に**sql: max depth**注釈が指定されています。 この場合、 ** \<Emp>** 親要素に指定されている**sql: max depth = 4**が優先されます。 **子\<Emp>** 要素に指定された**sql: max 深度**(被監督者のロールを再生) は無視されます。  
  
#### <a name="example-b"></a>例 B  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 このスキーマをテストするには、このトピックの「サンプル A」に記載されている手順に従います。  
  
### <a name="nonrecursive-elements"></a>非再帰要素  
 **Sql: max depth**注釈が、再帰を発生させないスキーマ内の要素に対して指定されている場合は、無視されます。 次のスキーマでは、 ** \<emp の>** 要素は、子要素を持つ** \<定数>** で構成されます。この子要素には、 ** \<emp>** 子要素があります。  
  
 このスキーマでは、 ** \<定数>** 要素に指定された**sql: max 深度**注釈は無視されます。これは、 ** \<Emp>** 親と** \<定数>** 子要素の間に再帰がないためです。 しかし、 ** \<emp>** 先祖と** \<emp>** 子の間に再帰があります。 スキーマでは、 **sql: max depth**注釈を両方とも指定しています。 そのため、先祖 (**\<** スーパーバイザーロールの Emp>) で指定されている**sql: 最大深度**注釈が優先されます。  
  
#### <a name="example-c"></a>例 C  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 このスキーマをテストするには、このトピックの例 A の手順に従ってください。  
  
## <a name="complex-types-derived-by-restriction"></a>制限により派生する複合型  
 ** \<制限>** による複合型の派生がある場合、対応する基本複合型の要素は、 **sql: max depth**注釈を指定できません。 このような場合は、派生型の要素に**sql: max depth**注釈を追加できます。  
  
 一方、 ** \<拡張>** による複合型の派生がある場合、対応する基本複合型の要素は**sql: max depth**注釈を指定できます。  
  
 たとえば、次の XSD スキーマでは、基本データ型に**sql: max depth**注釈が指定されているため、エラーが生成されます。 この注釈は、別の型の** \<制限>** によって派生された型ではサポートされていません。 この問題を解決するには、スキーマを変更し、派生型の要素に対して**sql: max depth**注釈を指定する必要があります。  
  
#### <a name="example-d"></a>例 D  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 スキーマでは、 **sql: max depth**は、**顧客 basetype**複合型に対して指定されています。 また、このスキーマでは、Customer **basetype**から派生し**た型の** ** \<顧客>** 要素を指定します。 このようなスキーマで XPath クエリを指定すると、エラーが発生します。これは、制限の基本型で定義されている要素で**sql: max depth**がサポートされていないためです。  
  
## <a name="schemas-with-a-deep-hierarchy"></a>深い階層のスキーマ  
 要素に子要素が含まれ、その子要素にさらに別の子要素が含まれるというような深い階層のスキーマの場合は、 このようなスキーマで指定された**sql: max depth**注釈によって、500レベルを超える階層を含む XML ドキュメントが生成された場合 (レベル1のトップレベル要素、レベル2の子がある場合など)、エラーが返されます。  
  
  
