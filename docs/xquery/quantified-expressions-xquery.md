---
title: 量化式 (XQuery) |Microsoft Docs
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
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
author: rothja
ms.author: jroth
ms.openlocfilehash: 1cdbff23d2158dec00b6b8d050d6a4a90341bd23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946376"
---
# <a name="quantified-expressions-xquery"></a>量化式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  存在量化子と全称量化子により、2 つのシーケンスに適用されるブール演算子に異なるセマンティクスが指定されます。 これを次の表に示します。  
  
 *存在量化子*  
 最初のシーケンスの任意の項目に一致するものがある場合を使用する比較演算子に基づいて、2 番目のシーケンスは、2 つのシーケンスを与え、True が返されます。  
  
 *ユニバーサル量指定子*  
 2 つのシーケンスがあるときに、最初のシーケンスのすべてのアイテムが 2 番目のシーケンスと一致する場合、True が返されます。  
  
 XQuery には、次の形式の量化式がサポートされています。  
  
```  
( some | every ) <variable> in <Expression> (,...) satisfies <Expression>  
```  
  
 クエリでこれらの式を使用すると、1 つまたは複数のシーケンスを式に存在量化またはユニバーサル量化を明示的に適用します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、内の式、`satisfies`句は、次のいずれかが発生する必要があります: ノード シーケンス、空のシーケンスまたはブール値。 この式の結果の有効なブール値が、量化に使用されます。 使用する存在量化**一部**真の結果を式では、量化子によりバインドされた値の少なくとも 1 つの場合は True を返します。 使用する全称**すべて**量化子によりバインドされたすべての値の True である必要があります。  
  
 たとえば、次のクエリのチェックすべて\<場所 > 要素に LocationID 属性があるかどうかを参照してください。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 LocationID はの必須の属性があるため、\<場所 > 要素、期待される結果が表示されます。  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 使用する代わりに、 [query() メソッド](../t-sql/xml/query-method-xml-data-type.md)、使用することができます、 [value() メソッド](../t-sql/xml/value-method-xml-data-type.md)にリレーショナルの世界では、次のクエリで示すように結果を返します。 クエリは、すべてのワーク センターの場所に LocationID 属性がある場合に True を返します。 それ以外の場合は False が返されます。  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 次のクエリでは、製品の写真の中に小さいサイズの写真があるかどうかを確認します。 製品カタログ XML には、さまざまな角度で撮影されたサイズの異なる製品の写真が格納されています。 各製品カタログ XML にサイズの小さい写真が少なくとも 1 枚含まれているようにすることができます。 これを行うには、次のクエリを実行します。  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 これは、結果の一部です。  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   量化式の変数をバインドする操作の一部として、型のアサーションはサポートされません。  
  
## <a name="see-also"></a>関連項目  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
