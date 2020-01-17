---
title: テーブルのデータの挿入と更新 (チュートリアル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 19e6683baeb0a82c77a858b04f18695ba7120b15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250131"
---
# <a name="inserting-and-updating-data-in-a-table-tutorial"></a>テーブルのデータの挿入と更新 (チュートリアル)
  **Products** テーブルを作成したので、INSERT ステートメントを使用してデータをテーブルに挿入する準備ができました。 データを挿入した後は、UPDATE ステートメントを使用して行の内容を変更します。 更新を 1 つの行に制限するには、UPDATE ステートメントの WHERE 句を使用します。 4 つのステートメントによって、次のデータが入力されます。  
  
|ProductID|ProductName|Price|ProductDescription|  
|---------------|-----------------|-----------|------------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires|  
|3000|3mm Bracket|.52||  
  
 基本構文は次のとおりです。INSERT、テーブル名、列リスト、値、およびし、値のリストを挿入します。 行の先頭にある 2 つのハイフンは、その行がコメントであることを示します。この行のテキストはコンパイラによって無視されます。 この場合、コメントは構文に許可されているバリエーションを記述します。  
  
### <a name="to-insert-data-into-a-table"></a>データをテーブルに挿入するには  
  
1.  次のステートメントを実行し、前のタスクで作成した `Products` テーブルに行を挿入します。 これは基本構文です。  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  次のステートメントは、フィールド一覧 (かっこ内) と値一覧の両方にある `ProductID` と `ProductName` の配置を交換することで、パラメーターの順序を変更する方法を示しています。  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  次のステートメントは、値が正しい順序で示されている限り、列の名前はオプションであることを示しています。 この構文は一般的ですが、他のユーザーがコードを理解しにくいため、推奨されません。 `NULL` が `Price` 列に指定されているのは、この製品の価格が不明ためです。  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  スキーマ名は、既定のスキーマ内のテーブルにアクセスし、変更している場合にはオプションです。 `ProductDescription` 列では NULL 値が許可されており、値が提供されていないため、 `ProductDescription` 列の名前と値はステートメントから完全に省略できます。  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>Products テーブルを更新するには  
  
1.  次の `UPDATE` ステートメントを入力して実行し、2 番目の製品の `ProductName` を `Screwdriver`から `Flat Head Screwdriver`に変更します。  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [テーブルのデータの読み取り (チュートリアル)](lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>参照  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  
