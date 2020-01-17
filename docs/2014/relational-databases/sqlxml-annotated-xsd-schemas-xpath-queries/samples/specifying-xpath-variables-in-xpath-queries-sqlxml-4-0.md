---
title: (SQLXML 4.0) の XPath クエリの XPath の変数を指定します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], XPath variables
- XPath variables [SQLXML]
ms.assetid: c11ab816-11b8-4131-8b77-c03fe500fa10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25e6c96ccbe51ccc0d2d88c4b119c08538d37fcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010691"
---
# <a name="specifying-xpath-variables-in-xpath-queries-sqlxml-40"></a>XPath クエリ内での XPath 変数の指定 (SQLXML 4.0)
  次の例では、XPath クエリに XPath 変数を指定する方法を示します。 これらの例では、SampleSchema1.xml に格納されているマッピング スキーマに対して XPath クエリを指定しています。 このサンプル スキーマについては、次を参照してください。 [XPath の例のサンプル注釈付き XSD スキーマ&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-use-the-xpath-variables"></a>A. XPath 変数を使用する  
 サンプル テンプレートは、2 つの XPath クエリで構成されており、 各 XPath クエリは 1 つのパラメーターをとります。 テンプレートでは、これらのパラメーターの既定値も指定しています。 パラメーター値が指定されない場合は、既定値が使用されます。 2 つのパラメーターに既定値がで指定された **\<sql:header >** 。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='CustomerID'>1</sql:param>  
     <sql:param name='ContactID'>1</sql:param>   
  </sql:header>  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
    Customer[@CustomerID=$CustomerID]   
  </sql:xpath-query >  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
   Contact[@ContactID=$ContactID]   
  </sql:xpath-query>  
</ROOT>  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  コピー、[サンプル スキーマ コード](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)テキスト ファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (XPathVariables.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:header>  
         <sql:param name='CustomerID'>1</sql:param>  
         <sql:param name='ContactID'>1</sql:param>   
      </sql:header>  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[@CustomerID=$CustomerID]   
      </sql:xpath-query >  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
       Contact[@ContactID=$ContactID]   
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。 詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
> [!NOTE]  
>  この例では、パラメーターは渡されていません。 このため、パラメーターの既定値が使用されます。  
  
  
