---
title: 選択述語の指定 (SQLXML 4.0) の場所のパスに |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d35b70c157dc5285355fcd15b38739757f0be9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012579"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>ロケーション パスでの選択述語の指定 (SQLXML 4.0)
  述語は、SELECT ステートメントの WHERE 句と同様に、軸についてノード セットをフィルター選択するものです。 述語はかっこで囲みます。 フィルター選択されたノード セットの各ノードに対し、ノードをコンテキスト ノード、ノード セット内のノード数をコンテキストのサイズとして、述語式が評価されます。 述語式が TRUE と評価された場合、そのノードは結果のノード セットに含められます。  
  
 XPath では、位置に基づくフィルター選択を行うこともできます。 数値として評価される述語式を使用すると、その序数に対応するノードが選択されます。 たとえば、ロケーション パス `Customer[3]` では、3 番目の顧客が返されますが、 このような数値述語はサポートされていません。 サポートされているのは、ブール値の結果を返す述語式のみです。  
  
> [!NOTE]  
>  XPath の場合は、この XPath 実装の制限についての情報とそのと W3C 仕様の違いは、次を参照してください。[を使用して XPath クエリの概要&#40;SQLXML 4.0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md)します。  
  
## <a name="selection-predicate-example-1"></a>選択述語。例 1  
 すべての現在のコンテキスト ノードから次の XPath 式 (ロケーション パス) を選択、 **\<顧客 >** 子要素が、 **CustomerID** ALFKI の値を持つ属性。  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 この XPath クエリでは、`child` と `attribute` は軸名で、 `Customer` ノード テストです (場合は TRUE`Customer`は、 **\<要素ノード >** ため、 **\<要素 >** のプリンシパル ノード型には、`child`軸) です。 `attribute::CustomerID="ALFKI"` は述語です。 述語では、`attribute`は、軸と`CustomerID`はノード テストです (TRUE の場合**CustomerID**ため、コンテキスト ノードの属性は、 **\<属性 >** プリンシパルは、ノード タイプの`attribute`軸) です。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>選択述語。例 2  
 すべての現在のコンテキスト ノードから次の XPath 式 (ロケーション パス) を選択、 **\<順序 >** 孫要素が、 **SalesOrderID**値 1 を持つ属性。  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 この XPath 式では、`child` と `attribute` は軸名で、 `Customer`、`Order`、および `SalesOrderID` はノード テストです。 `attribute::OrderID="1"` は述語です。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>選択述語。例 3  
 すべての現在のコンテキスト ノードから次の XPath 式 (ロケーション パス) を選択、 **\<顧客 >** 子が 1 つまたは複数 **\<ContactName >** 子:  
  
```  
child::Customer[child::ContactName]  
```  
  
 この例では、  **\<ContactName >** の子要素には、 **\<顧客 >** と呼ばれる XML ドキュメント内の要素*要素中心のマッピング*注釈付き XSD スキーマです。  
  
 この XPath 式では、`child` が軸名で、 `Customer` ノード テストです (場合に TRUE を`Customer`は、 **\<要素 >** ノード、ため **\<要素 >** のプリンシパル ノード型は、`child`軸) です。 `child::ContactName` は述語です。 述語では、`child`は、軸と`ContactName`はノード テストです (TRUE の場合`ContactName`は、 **\<要素 >** ノード)。  
  
 この式だけを返す、 **\<顧客 >** を持つコンテキスト ノードの要素の子 **\<ContactName >** 子要素。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>選択述語。例 4  
 次の XPath 式を選択します **\<顧客 >** がない、コンテキスト ノードの要素の子 **\<ContactName >** 子要素。  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 この例では、  **\<ContactName >** の子要素には、 **\<顧客 >** 内の要素、XML ドキュメント、および、ContactName フィールドは必須でない、データベース。  
  
 この例では、`child` は軸で、 `Customer` ノード テストです (場合に TRUE を`Customer`は、\<要素 > ノード)。 `not(child::ContactName)` は述語です。 述語では、`child`は、軸と`ContactName`はノード テストです (TRUE の場合`ContactName`は、\<要素 > ノード)。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>選択述語。例 5  
 すべての現在のコンテキスト ノードから次の XPath 式を選択、 **\<顧客 >** 子を持つ、 **CustomerID**属性。  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 この例で`child`は、軸と`Customer`はノード テストです (場合は TRUE`Customer`は、\<要素 > ノード)。 `attribute::CustomerID` は述語です。 述語では、`attribute`軸と`CustomerID`述語である (TRUE の場合`CustomerID`は、 **\<属性 >** ノード)。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>選択述語。例 6  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 では、次の例に示すように、述語にクロス積を含む XPath クエリがサポートされています。  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 このクエリでは、`Order` の `OrderDate` が任意の `ShipDate` の `Order` と等しいすべての顧客が選択されます。  
  
## <a name="see-also"></a>参照  
 [注釈付き XSD スキーマの概要&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定&#40;SQLXML 4.0&#41;](../../sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
