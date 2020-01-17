---
title: CDATA セクションを使用して sql:use を作成する-cdata (SQLXML 4.0) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cddde2ed1e40b2ea21cf4ebff75bea3beed8f2ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014008"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>sql:use-cdata を使用した、CDATA セクションの作成 (SQLXML 4.0)
  XML では、文字がマークアップ文字として処理されないよう、文字を含むテキスト ブロックをエスケープするときに CDATA セクションを使用します。  
  
 Microsoft では、データベース[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、XML パーサーでマークアップ文字として扱われますたとえば、角かっこを山以外の文字を含めることができます場合があります (\<と >)、小さいよりも-または-をシンボル (< =)、および、アンパサンド (&) は。マークアップ文字として扱われます。 この種類の特殊文字は、CDATA セクションで囲むことでマークアップ文字として扱われないようにできます。 CDATA セクション内の文字は、XML パーサーでプレーン テキストとして扱われます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で返されるデータを CDATA セクションで囲むには、`sql:use-cdata` 注釈を使用します。この注釈では、`sql:field` で指定される列の値を CDATA セクションで囲むかどうかを指定できます。 `sql:use-cdata` 注釈は、データベース列にマップされる要素だけに指定できます。  
  
 `sql:use-cdata` 注釈はブール値 (0 = false、1 = true) をとります。 指定できる値は 0、1、true、false です。  
  
 この注釈は、`sql:url-encode` と共に使用したり、ID、IDREF、IDREFS、NMTOKEN、NMTOKENS 属性型に使用することはできません。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. 要素に対して sql:use-cdata を指定する  
 次のスキーマで`sql:use-cdata`の 1 (True) に設定されている、  **\<AddressLine1 >** 内、 **\<アドレス >** 要素。 この結果、データは CDATA セクション内に返されます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 UseCData.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 UseCData.xml を保存したディレクトリに UseCDataT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (UseCData.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、結果セットの一部です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
