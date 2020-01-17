---
title: TargetNamespace 属性 (SQLXML 4.0) を使用してターゲット Namespace を指定します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: fd97b67974f248d002255c1977feebe4551e691f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013678"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>targetNamespace 属性を使用した、対象名前空間の指定 (SQLXML 4.0)
  XSD スキーマを作成するには、XSD を使用することができます**targetNamespace**ターゲット名前空間を指定する属性です。 このトピックで説明する方法、XSD **targetNamespace**、**よ**、および**されていません**属性を使用する XML インスタンスをどのように影響生成されると、名前空間と XPath クエリを指定する方法とします。  
  
 使用することができます、 **xsd:targetNamespace**属性を別の名前空間に要素と属性の既定の名前空間に配置します。 また、スキーマでローカルに宣言された要素と属性を、名前空間で修飾して表示するかどうかも指定できます。名前空間は、プレフィックスを使って明示的に、または既定により暗黙的に指定できます。 使用することができます、**よ**と**されていません**属性を **\<xsd:schema >** 要素をグローバルに指定するのには、ローカル要素と属性の修飾に使用できる、**フォーム**の個々 の要素と属性を個別に指定する属性です。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-a-target-namespace"></a>A. 対象名前空間を指定する  
 次の XSD スキーマを使用して、ターゲット名前空間を指定する、 **xsd:targetNamespace**属性です。 また、スキーマ、設定、**よ**と**されていません**属性に値を **「不適切な」** (これらの属性の既定値)。 これはグローバル宣言であり、すべてのローカル要素に影響を与えます ( **\<注文 >** スキーマで) と属性 ( **[得意先コード]** 、 **[担当者名]** 、および **[受注コード]** スキーマで)。  
  
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
  
-   **顧客タイプ**と**OrderType**型の宣言は、グローバルし、したがって、スキーマのターゲット名前空間に含まれますが。 宣言でこれらの種類は参照されているとその結果、 **\<お客様 >** 要素とその **\<注文 >** 子要素では、関連付けられているプレフィックスを指定ターゲット名前空間の。  
  
-   **\<お客様 >** スキーマのグローバル要素であるため、スキーマのターゲット名前空間に要素が含まれるもします。  
  
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
  
 このインスタンス ドキュメントでは、urn: マークアップの名前空間を定義しには、プレフィックス (y0) を関連付けます。 プレフィックスが適用されるだけに、 **\<お客様 >** 大域要素です。 (要素は、の子として宣言されているために、グローバル **\<xsd:schema >** スキーマ内の要素です)。  
  
 のローカル要素と属性にプレフィックスは適用されませんの値**よ**と**されていません**に属性が設定されて **「不適切な」** スキーマにします。 注意して、 **\<注文 >** 要素は、ローカルの子としてその宣言が表示されますので、 **\<複合型 >** を定義する要素、  **\<顧客タイプ >** 要素です。 同様に、属性 ( **[得意先コード]** 、 **[受注コード]** と **[担当者名]** ) は、ローカル、グローバルにできません。  
  
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
  
     テンプレートの XPath クエリを取得、 **\<お客様 >** 1 の [得意先コード] を持つ顧客の要素です。 この XPath クエリでは、属性ではなく、クエリ内の要素の名前空間プレフィックスが指定されることに注意してください。 ローカル属性は、スキーマ内の指定と同様、修飾されません。  
  
     マッピング スキーマ (targetNamespace.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 スキーマが指定されている場合**よ**と**されていません**属性の値を持つ **「修飾」** 、すべてのローカル インスタンス ドキュメントには要素および属性で修飾します。 これらの属性を含めるには、前のスキーマを変更することができます、  **\<xsd:schema >** 要素テンプレートを再度実行するとします。 この場合は、インスタンスで属性も修飾されるので、名前空間プレフィックスを含むよう XPath クエリを変更します。  
  
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
  
  
