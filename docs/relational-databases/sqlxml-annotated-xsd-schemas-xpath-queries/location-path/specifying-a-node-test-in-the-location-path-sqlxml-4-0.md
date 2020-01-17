---
title: ロケーションパスでのノードテストの指定 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f94f155ee86df6daf0c039a18f27c30e294d57df
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254739"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>ロケーション パスでのノード テストの指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  ノード テストによって、ロケーション ステップで選択されるノードの型が決まります。 すべての軸 (**子**、**親**、**属性**、または**自己**) には、主ノード型があります。 **属性**軸の場合、プリンシパルノード型は** \<属性>** です。 **親**、**子**、および**自己**軸の場合、主ノード型は** \<要素>** になります。  
  
> [!NOTE]  
>  ワイルドカード (*) のノード テスト (たとえば `child::*`) は、サポートされていません。  
  
## <a name="node-test-example-1"></a>ノードテスト: 例1  
 ロケーションパス`child::Customer`は、コンテキストノードの** \<Customer>** 要素の子を選択します。  
  
 この例では、`child` は軸で、`Customer` はノード テストです。 **子**軸の主ノード型は** \<、要素>** です。 したがって、 ** \<Customer>** ノードが** \<要素>** ノードの場合、ノードテストは TRUE になります。 コンテキストノードに** \<顧客>** 子がない場合は、空のノードセットが返されます。  
  
## <a name="node-test-example-2"></a>ノード テスト : 例 2  
 ロケーションパス`attribute::CustomerID`によって、コンテキストノードの**CustomerID**属性が選択されます。  
  
 この例では`attribute` 、は軸で`CustomerID` 、はノードテストです。 **属性**軸の主ノード型は** \<属性>** です。 このため、 **CustomerID**が** \<属性>** ノードの場合、ノードテストは TRUE になります。 コンテキストノードに**CustomerID**がない場合は、空のノードセットが返されます。  
  
> [!NOTE]  
>  この XPath の実装では、ロケーションステップが、スキーマで宣言されていない** \<要素>** または** \<属性>** 型を参照している場合、エラーが生成されます。 これは、空のノード セットを返す MSXML の XPath の実装とは異なります。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸の省略構文  
 ロケーション パスでは、次の省略構文がサポートされています。  
  
-   
  `attribute::` は `@` で省略できます。  
  
     ロケーション パス `Customer[@CustomerID="ALFKI"]` は、`child::Customer[attribute::CustomerID="ALFKI"]` と同じです。  
  
-   ロケーション ステップから `child::` を省略できます。  
  
     したがって、**子**は既定の軸です。 ロケーション パス `Customer/Order` は、`child::Customer/child::Order` と同じです。  
  
-   
  `self::node()` は 1 つのピリオド (.) で省略できます。また、`parent::node()` は 2 つのピリオド (..) で省略できます。  
  
  
