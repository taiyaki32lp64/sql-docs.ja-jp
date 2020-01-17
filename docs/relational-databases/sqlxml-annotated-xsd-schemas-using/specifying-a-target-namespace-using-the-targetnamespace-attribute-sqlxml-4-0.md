---
title: TargetNamespace (SQLXML) を使用してターゲットの名前空間を指定する
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39469073a8affe82ee5231a71676d7046f712f9f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257360"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>targetNamespace 属性を使用した、対象名前空間の指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD スキーマの記述では、XSD **targetNamespace**属性を使用して、ターゲットの名前空間を指定できます。 このトピックでは、XSD **targetNamespace**、 **ElementFormDefault**、および**attributeFormDefault**属性の動作、生成される XML インスタンスへの影響、および名前空間での XPath クエリの指定方法について説明します。  
  
 **Xsd: targetNamespace**属性を使用して、既定の名前空間の要素と属性を別の名前空間に配置できます。 また、スキーマでローカルに宣言された要素と属性を、名前空間で修飾して表示するかどうかも指定できます。名前空間は、プレフィックスを使って明示的に、または既定により暗黙的に指定できます。 **** **Xsd: schema>要素の elementFormDefault 属性と attributeFormDefault 属性を使用して、ローカル要素と属性の修飾をグローバルに指定することも、form 属性を使用して個々の要素と属性を個別に指定することもでき\<** ます。 **** ****  
  
## <a name="examples"></a>例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、「 [SQLXML の例を実行するための要件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)」を参照してください。  
  
### <a name="a-specifying-a-target-namespace"></a>A. 対象名前空間を指定する  
 次の XSD スキーマでは、 **xsd: targetNamespace**属性を使用してターゲットの名前空間を指定しています。 また、このスキーマでは、 **elementFormDefault**属性と**attributeFormDefault**属性の値が **"非修飾"** (これらの属性の既定値) に設定されます。 これはグローバルな宣言であり、すべてのローカル**** 要素 ( **** ******\<スキーマの順序>** ) と属性 (スキーマ内の CustomerID、得意先、および OrderID) に影響します。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 このスキーマの内容は次のとおりです。  
  
-   **顧客型**と**ordertype**型の宣言はグローバルであるため、スキーマのターゲット名前空間に含まれています。 結果として、これらの型が** \<Customer>** 要素と** \<Order>** 子要素の宣言で参照されている場合は、ターゲットの名前空間に関連付けられているプレフィックスが指定されます。  
  
-   Customer>要素はスキーマのグローバル要素であるため、スキーマのターゲット名前空間にも含まれます。 ** \<**  
  
 このスキーマに対して次の XPath クエリを実行します。  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 この XPath クエリでは、次のインスタンス ドキュメントが生成されます。ここでは注文の一部のみを表示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 このインスタンスドキュメントでは、urn: MyNamespace 名前空間を定義し、プレフィックス (y0) をそれに関連付けます。 プレフィックスは、 ** \<Customer>** global 要素にのみ適用されます。 (要素は、スキーマの** \<xsd: schema>** 要素の子として宣言されているため、グローバルです)。  
  
 スキーマで**elementFormDefault**属性と**attributeFormDefault**属性の値が **"非修飾"** に設定されているため、プレフィックスはローカルの要素および属性には適用されません。 ** \<Order>** 要素は、その宣言が、 ** \<顧客の型>** 要素を定義する** \<complexType>** 要素の子として表示されるため、ローカルになっていることに注意してください。 同様に、属性 (**CustomerID**、 **OrderID** **、および**CustomerID) はグローバルではなくローカルになります。  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>このスキーマの実際のサンプルを作成するには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 targetNameSpace.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 targetNamespace.xml を保存したディレクトリに targetNameSpaceT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     このテンプレートの XPath クエリでは、CustomerID が1の顧客の** \<>** 要素が返されます。 この XPath クエリでは、属性ではなく、クエリ内の要素の名前空間プレフィックスが指定されることに注意してください。 ローカル属性は、スキーマ内の指定と同様、修飾されません。  
  
     マッピング スキーマ (targetNamespace.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 スキーマで**elementFormDefault**属性と**attributeFormDefault**属性が値 **"qualified"** で指定されている場合、インスタンスドキュメントには、すべてのローカル要素と属性が修飾されます。 前のスキーマを変更して、 ** \<これらの属性を xsd: schema>** 要素に含め、テンプレートを再度実行することができます。 この場合は、インスタンスで属性も修飾されるので、名前空間プレフィックスを含むよう XPath クエリを変更します。  
  
 次は変更した XPath クエリです。  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 次は返される XML ドキュメントです。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
