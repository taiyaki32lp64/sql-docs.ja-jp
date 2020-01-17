---
title: Expanded-qname() (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c50409ea35809c52de718a8281bf76f75a5a0e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004585"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>QNames に関係する関数 - expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定された URI 名前空間を使用して xs:QName 型の値を返します、 *$paramURI*とで指定されたローカル名、 *$paramLocal*します。 場合 *$paramURI*空の文字列または空のシーケンスでは、名前空間を表すありません。  
  
## <a name="syntax"></a>構文  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>引数  
 *$paramURI*  
 QName の URI 名前空間です。  
  
 *$paramLocal*  
 QName のローカル名部分です。  
  
## <a name="remarks"></a>コメント  
 次の状態に、 **expanded-QName()** 関数。  
  
-   場合、 *$paramLocal* xs:NCName 型の正しい形式で指定された値がない、空のシーケンスが返され、動的エラーを表します。  
  
-   Xs:QName 型から他の任意の型への変換でサポートされていない[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]します。 このため、 **expanded-QName()** 関数は、XML の構築では使用できません。 たとえば、`<e> expanded-QName(...) </e>` など、ノードを構築する場合、型指定なしの値を使用する必要があります。 これは、`expanded-QName()` で返される xs:QName の値を xdt:untypedAtomic に変換する必要性を意味します。 ただし、これはサポートされていません。 ソリューションは、このトピックで後述する例で提供されます。  
  
-   変更したり、既存の QName 型の値を比較できます。 たとえば、 `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` 、要素の値と比較します <`e`>、によって返される qname、 **expanded-QName()** 関数。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**内の列を入力、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]データベース。  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. QName 型ノードの値を置換する  
 この例では、QName 型の要素ノードの値を変更する方法を示しています。 この例では、次の操作が実行されます。  
  
-   QName 型の要素を定義する XML スキーマ コレクションを作成します。  
  
-   含むテーブルを作成、 **xml** XML スキーマ コレクションを使用して型の列。  
  
-   テーブルには、XML インスタンスを保存します。  
  
-   使用して、 **modify()** インスタンスの QName 型要素の値を変更する xml データ型のメソッド。 **Expanded-QName()** 関数を使用して、新しい QName 型の値を生成します。  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 次のクエリで、<`ElemQN`> を使用して要素の値が置き換えられます、 **modify()** of XML DML で示すように置換値と xml データ型メソッド。  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 結果は次のとおりです。 なお、要素 <`ElemQN`> QName の型が新しい値。  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 次のステートメントは、この例で使用しているオブジェクトを削除します。  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Expanded-QName() 関数を使用するときの制限に対処します。  
 **Expanded-qname**関数は、XML の構築では使用できません。 次に例を示します。 この制限を回避するために、この例では最初にノードを挿入してから、そのノードを変更しています。  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 次の試行追加 <`root`> 要素があるため、失敗、expanded-QName() 関数は、XML の構築ではサポートされていません。  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 これに対する解決策が最初の値を持つインスタンスを挿入するには、<`root`> 要素およびそれを変更します。 Nil 初期値を使用するこの例では、ときに、<`root`> 要素が挿入されます。 この例では、XML スキーマ コレクションの nil 値を許可して、<`root`> 要素。  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 次のクエリで示すように、QName 値を比較できます。 だけを返すクエリ、<`root`> 要素の値が QName に一致がによって返される値を入力、 **expanded-QName()** 関数。  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 1 つの制限があります。**Expanded-QName()** 関数が 2 番目の引数として空のシーケンスに受け取り、2 番目の引数が正しくない場合は、実行時エラーを発生させる代わりに空に戻ります。  
  
## <a name="see-also"></a>関連項目  
 [QNames に関係する関数&#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
