---
title: サブクエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e68809c7551e3c6711fadd9973c472dcb4e90307
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270619"
---
# <a name="create-subqueries-visual-database-tools"></a>サブクエリの作成 (Visual Database Tools)
  クエリの結果は、他のクエリへの入力内容として使用できます。 IN( ) 関数、EXISTS 演算子、FROM 句などを使用するサブクエリの結果を、ステートメントとして再利用できます。  
  
 サブクエリは、SQL ペインに直接入力して作成することも、クエリをコピーおよび貼り付けして作成することもできます。  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>SQL ペインでサブクエリを定義するには  
  
1.  最初のクエリを作成します。  
  
2.  SQL ペインで SQL ステートメントを選択し、 **[コピー]** をクリックしてクリップボードにクエリを移動します。  
  
3.  新しいクエリの入力を開始し、WHERE 句または FROM 句に最初のクエリを **[貼り付け]** で貼り付けます。  
  
     たとえば、 `products` および `suppliers`という 2 つのテーブルがあり、スウェーデンの業者の製品をすべて表示するクエリを作成するとします。 まず、 `suppliers` からスウェーデンの業者を検索するクエリを作成します。  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
     [コピー] を使用してクリップボードにこのクエリをコピーします。 次に、 `products` テーブルから製品に関する情報を一覧表示する 2 番目のクエリを作成します。  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
     SQL ペインで、2 番目のクエリに WHERE 句を追加し、クリップボードにある最初のクエリを貼り付けます。 最初のクエリをかっこで囲むと、最終的に次のようになります。  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>参照  
 [クエリの種類がサポートされている&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [検索基準の指定 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
