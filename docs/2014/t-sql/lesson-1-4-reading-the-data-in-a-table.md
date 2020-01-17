---
title: テーブルのデータの読み取り (チュートリアル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0649e167ebaa90267422594ccd193ba468838e6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68187296"
---
# <a name="reading-the-data-in-a-table-tutorial"></a>テーブルのデータの読み取り (チュートリアル)
  テーブルのデータを読み取るには、SELECT ステートメントを使用します。 SELECT ステートメントは最も重要な [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの 1 つで、構文には多くのバリエーションがあります。 このチュートリアルでは、5 つの単純なバージョンを使用します。  
  
### <a name="to-read-the-data-in-a-table"></a>テーブルのデータを読み取るには  
  
1.  次のステートメントを入力して実行し、 `Products` テーブルのデータを読み取ります。  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  アスタリスクを使用すると、テーブルの列をすべて選択できます。 これはアドホック クエリでよく使用されます。 永続的なコード内では列一覧を指定して、新しい列が後からテーブルに追加された場合でも、予測された列がステートメントによって返されるようにしてください。  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  返す必要のない列は省略できます。 列は、一覧内の順序で返されます。  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  ユーザーに返される行を制限するには、 `WHERE` 句を使用します。  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  列内の値は、列が返されたときに操作できます。 次の例では、 `Price` 列に対して数学的演算を実行します。 このようにして変更された列には、 `AS` キーワードを使用して名前を指定しない限り、名前が付けられません。  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>SELECT ステートメント内で役に立つ関数  
 SELECT ステートメント内のデータの操作に使用できる関数の詳細については、次のトピックを参照してください。  
  
|||  
|-|-|  
|[文字列関数 (Transact-SQL)](/sql/t-sql/functions/string-functions-transact-sql)|[日付と時刻のデータ型および関数 (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|  
|[数学関数 (Transact-SQL)](/sql/t-sql/functions/mathematical-functions-transact-sql)|[テキスト関数とイメージ関数 (Transact-SQL)](/sql/t-sql/functions/text-and-image-functions-textptr-transact-sql)|  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [概要:データベース オブジェクトの作成](lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>関連項目  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
  
