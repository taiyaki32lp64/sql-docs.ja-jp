---
title: XPath クエリ (SQLXML 4.0) で明示的な変換関数の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43e7067f00e21f57d64f2206fb1008f21d77dd4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010699"
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>XPath クエリでの明示変換関数の指定 (SQLXML 4.0)
  次の例では、XPath クエリに明示変換関数を指定する方法を示します。 これらの例では、SampleSchema1.xml に格納されているマッピング スキーマに対して XPath クエリを指定しています。 このサンプル スキーマについては、次を参照してください。 [XPath の例のサンプル注釈付き XSD スキーマ&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>A. number() 明示変換関数を使用する  
 `number()` 関数は、引数を数値に変換します。  
  
 値と仮定すると**ContactID**は数値型以外は、次のクエリに変換します**ContactID**を数値と値 4 を比較します。 クエリが、すべてを返します**\<従業員 >** 、コンテキスト ノードの子要素、 **ContactID** 4 の数値の値を持つ属性。  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 ショートカット、`attribute`軸 (@) を指定できますので、`child`軸は既定のクエリから省略できます。  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 具体的には、クエリを持つ従業員を返します、 **ContactID** 4。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  コピー、[サンプル スキーマ コード](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)テキスト ファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (ExplicitConversionA.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 このテンプレートの実行の結果セットは次のとおりです。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>B. string() 明示変換関数を使用する  
 `string()` 関数は、引数を文字列に変換します。  
  
 次のクエリに変換します**ContactID**文字列値「4」文字列を比較します。 クエリでは、すべてを返します**\<従業員 >** 、コンテキスト ノードの子要素を**ContactID** 「4」の文字列値を持つ。  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 ショートカット、`attribute`軸 (@) を指定できますので、`child`軸は既定のクエリから省略できます。  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 機能的には、このクエリでは上の例のクエリと同じ結果が返されます。ただし、評価は数値 (4) ではなく文字列に対して行われます。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>マッピング スキーマに対して XPath クエリをテストするには  
  
1.  コピー、[サンプル スキーマ コード](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)テキスト ファイルに貼り付けます。 SampleSchema1.xml として保存します。  
  
2.  次のテンプレート (ExplicitConversionB.xml) を作成し、SampleSchema1.xml を保存したディレクトリに保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleSchema1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリの相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 このテンプレートを実行した場合の結果セットは次のとおりです。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
