---
title: ロケーションパスでの選択述語の設定 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84a3eade8a706e95b3ddba72d96e37d8fabf1fd3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255996"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>ロケーション パスでの選択述語の指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  述語は、SELECT ステートメントの WHERE 句と同様に、軸についてノード セットをフィルター選択するものです。 述語はかっこで囲みます。 フィルター選択されたノード セットの各ノードに対し、ノードをコンテキスト ノード、ノード セット内のノード数をコンテキストのサイズとして、述語式が評価されます。 述語式が TRUE と評価された場合、そのノードは結果のノード セットに含められます。  
  
 XPath では、位置に基づくフィルター選択を行うこともできます。 数値として評価される述語式を使用すると、その序数に対応するノードが選択されます。 たとえば、ロケーション パス `Customer[3]` では、3 番目の顧客が返されますが、 このような数値述語はサポートされていません。 サポートされているのは、ブール値の結果を返す述語式のみです。  
  
> [!NOTE]  
>  Xpath のこの XPath 実装と W3C 仕様の違いについては、「 [Xpath クエリの使用の概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)」を参照してください。  
  
## <a name="selection-predicate-example-1"></a>選択述語: 例1  
 次の XPath 式 (ロケーションパス) では、現在のコンテキストノードから、 **CustomerID**属性が ALFKI という値が指定されているすべての** \<顧客>** 子要素が選択されます。  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 この XPath クエリでは、`child` と `attribute` は軸名で、 `Customer`はノードテストです。は、 `Customer`が** \<要素ノード>** である場合は TRUE になります。これは、 `child` ** \<要素>** が軸の主ノード型であるためです。 
  `attribute::CustomerID="ALFKI"` は述語です。 述語`attribute`では、は軸で、 `CustomerID`はノードテストです ( **CustomerID**がコンテキストノードの属性である場合は TRUE になります。これは、 ** \<属性>** が**属性**軸の主ノード型であるためです)。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>選択述語: 例2  
 次の XPath 式 (ロケーションパス) は、現在のコンテキストノードから、 **salesorderid**属性が値1であるすべての** \<順序>** 孫を選択します。  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 この XPath 式では、`child` と `attribute` は軸名で、 
  `Customer`、`Order`、および `SalesOrderID` はノード テストです。 
  `attribute::OrderID="1"` は述語です。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>選択述語: 例3  
 次の XPath 式 (ロケーションパス) は、現在のコンテキストノードから、すべての** \<顧客>** 子** \<>** 1 人以上のユーザーを持つ子を選択します。  
  
```  
child::Customer[child::ContactName]  
```  
  
 この例では、担当の** \<>** が、XML ドキュメント内** \<の Customer>** 要素の子要素であることを前提としています。これは、注釈付き XSD スキーマでは*要素中心のマッピング*と呼ばれています。  
  
 この XPath 式では、`child` が軸名で、 `Customer`ノードテストを示します。が`Customer` ** \<要素>** ノードの場合は TRUE になります。これは、 ** \<要素>** が軸の`child`主ノード型であるためです。 
  `child::ContactName` は述語です。 述語では、 `child`は軸`ContactName`で、はノードテストです。が`ContactName` ** \<要素>** ノードの場合は TRUE になります。  
  
 この式で返されるのは、 ** \<Customer>** 子要素** \<>** 子を持つコンテキストノードの子要素だけです。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>選択述語: 例4  
 次の XPath 式は、 ** \<Customer>** 要素の子要素** \<>** 子を持たないコンテキストノードの子要素を選択します。  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 この例では、 ** \<>** の** \<ユーザー**が XML ドキュメント内の Customer>要素の子要素であり、データベースでは [担当側] フィールドが必須ではないことを前提としています。  
  
 この例では、`child` は軸で、 `Customer`はノードテストです。が`Customer` \<要素> ノードの場合は TRUE です。 
  `not(child::ContactName)` は述語です。 述語では、 `child`は軸`ContactName`で、はノードテストです。が`ContactName` \<要素> ノードの場合は TRUE になります。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>選択述語: 例5  
 次の XPath 式は、現在のコンテキストノードから、 **CustomerID**属性が指定されているすべての** \<顧客>** 子を選択します。  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 この例では`child` 、は軸で`Customer` 、はノードテストです ( `Customer`が\<要素> ノードの場合は TRUE)。 
  `attribute::CustomerID` は述語です。 述語では、 `attribute`は軸で、 `CustomerID`は述語です (が`CustomerID` ** \<属性>** ノードの場合は TRUE)。  
  
 省略構文を使用した場合、XPath クエリは次のように指定できます。  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>選択述語 : 例 6  
 
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 では、次の例に示すように、述語にクロス積を含む XPath クエリがサポートされています。  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 このクエリでは、`Order` の `OrderDate` が任意の `ShipDate` の `Order` と等しいすべての顧客が選択されます。  
  
## <a name="see-also"></a>参照  
 [注釈付き XSD スキーマの概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
