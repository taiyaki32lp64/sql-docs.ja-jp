---
title: XQuery での名前空間の処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 07158d4131c60cf46f49a860721333c78213c982
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004534"
---
# <a name="handling-namespaces-in-xquery"></a>XQuery での名前空間の処理
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックでは、クエリで名前空間の処理のサンプルを提供します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-declaring-a-namespace"></a>A. 名前空間の宣言  
 次のクエリでは、特定の製品モデルの製造ステップを取得します。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 結果の一部を次に示します。  
  
```  
<AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
...  
```  
  
 なお、**名前空間**キーワードを使用して、新しい名前空間プレフィックスの定義を"AWMI:"です。 このプレフィックスしする必要があるため、クエリでその名前空間のスコープ内にあるすべての要素。  
  
### <a name="b-declaring-a-default-namespace"></a>B. 既定の名前空間を宣言します。  
 前のクエリでは、新しい名前空間プレフィックスが定義されました。 そのプレフィックスは、目的の XML 構造を選択するクエリで使用する必要があります。 または、次の変更のクエリで示すように、既定の名前空間と名前空間を宣言できます。  
  
```  
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 結果  
  
```  
<step xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
...  
```  
  
 この例で、定義されている名前空間、`"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"` は、既定または空の名前空間をオーバーライドするように作成されています。 このため、不要になったがある名前空間プレフィックスを使用するパス式でのクエリにします。 また、結果に表示される要素名にも、名前空間プレフィックスはありません。 既定の名前空間は、すべての要素に適用されますが、属性には適用されません。  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. XML 構築時の名前空間の使用  
 新しい名前空間を定義するときに、スコープだけでなく、クエリが構築するために起動するようにします。 たとえば、XML の構築に定義できます、新しい名前空間を使用して、"`declare namespace ...`"宣言し、その名前空間を使用して、任意の要素と属性をクエリ結果内に表示されるように構築することで。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 代わりに、次のクエリのように、XML 構築の一部として、名前空間を使用する各所で明示的に定義することもできます。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. 既定の名前空間を使用した構築  
 構築後の XML で既定の名前空間が使用されるように定義することもできます。 次のクエリが、既定の名前空間"uri:SomeNamespace"を指定する方法を示しますたとえば、\\など、構築されるローカル名前付き要素の既定値として使用する、`<Result>`要素。  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 既定の要素の名前空間または空の名前空間をオーバーライドして、構築される XML 内のすべてのローカルの名前付き要素は、その後にバインドされているオーバーライドする側の既定の名前空間に注意してください。 したがって、空の名前空間を利用して XML を柔軟に構築する必要がある場合は、要素の既定の名前空間をオーバーライドしないようにします。  
  
## <a name="see-also"></a>関連項目  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
