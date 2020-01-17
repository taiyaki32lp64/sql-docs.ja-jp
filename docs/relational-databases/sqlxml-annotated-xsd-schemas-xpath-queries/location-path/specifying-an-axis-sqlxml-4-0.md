---
title: 軸の指定 (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a219c2093832b979171584d5559da359b574552e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253063"
---
# <a name="specifying-an-axis-sqlxml-40"></a>軸の指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   軸によって、ロケーション ステップで選択されるノードと、コンテキスト ノードの間のツリー リレーションシップが指定されます。 次の軸がサポートされています: **child**  
  
     コンテキスト ノードの子を含みます。  
  
     次の XPath 式 (ロケーションパス) は、現在のコンテキストノードからすべての** \<顧客>** 子を選択します。  
  
    ```  
    child::Customer  
    ```  
  
     この XPath クエリでは、`child` は軸で、 
  `Customer` はノード テストです。  
  
-   **parent**  
  
     コンテキスト ノードの親を含みます。  
  
     次の XPath 式では、すべての** \<顧客>** 子** \<>順序**の親を選択します。  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     これは、`child::Customer` を指定した場合と同じです。 この XPath クエリでは、`child` と `parent` は軸で、 
  `Customer` と `Order` はノード テストです。  
  
-   **属性**  
  
     コンテキスト ノードの属性を含みます。  
  
     次の XPath 式では、コンテキストノードの**CustomerID**属性が選択されます。  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **自身**  
  
     コンテキスト ノードそのものを含みます。  
  
     次の XPath 式は、現在のノードが** \<Order>** ノードである場合、そのノードを選択します。  
  
    ```  
    self::Order  
    ```  
  
     この XPath クエリでは、`self` は軸で、`Order` はノード テストです。  
  
  
