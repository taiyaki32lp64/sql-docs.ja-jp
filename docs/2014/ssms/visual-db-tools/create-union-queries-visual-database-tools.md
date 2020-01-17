---
title: UNION クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34e06960274c7e16ef4f6efc31f1b7ca55a7d48c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270588"
---
# <a name="create-union-queries-visual-database-tools"></a>UNION クエリの作成 (Visual Database Tools)
  UNION キーワードを使用すると、2 つの SELECT ステートメントの結果を、1 つのテーブルに表示できます。 いずれかの SELECT ステートメントから返された行がすべて組み合わされて、UNION 式の結果として表示されます。 例については、次を参照してください。 [SELECT の例&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql)します。  
  
> [!NOTE]  
>  ダイアグラム ペインに表示できるのは、1 つの SELECT 句だけです。 したがって、UNION クエリを使用している場合、クエリ デザイナーにはテーブル操作ペインは表示されません。  
  
### <a name="to-create-a-merged-select-query"></a>マージされた選択クエリを作成するには  
  
1.  クエリを開くか、新規作成します。  
  
2.  SQL ペインに有効な UNION 式を入力します。  
  
     次の例は、有効な UNION 式です。  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  **[クエリ デザイナー]** メニューの **[SQL の実行]** をクリックして、クエリを実行します。  
  
     UNION クエリがクエリ デザイナーによって書式化されます。  
  
## <a name="see-also"></a>参照  
 [クエリの種類がサポートされている&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [クエリに関する基本操作を実行&#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [共用体&#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/set-operators-union-transact-sql)  
  
  
