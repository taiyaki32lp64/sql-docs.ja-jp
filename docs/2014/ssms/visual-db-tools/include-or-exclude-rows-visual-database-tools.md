---
title: 行を含めるまたは除外する (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785a777571ef7659b1ae21a693e6754659a80e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298591"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>行を含めるまたは除外する (Visual Database Tools)
  選択クエリによって返される行の数を制限するには、検索条件またはフィルター条件を作成します。 SQL では、ステートメントの WHERE 句、または集計クエリの作成中に HAVING 句で検索条件が表示されます。  
  
> [!NOTE]  
>  検索条件を使用して、更新クエリ、結果の挿入クエリ、値の挿入クエリ、削除クエリ、およびテーブルの作成クエリの対象となる行を表すこともできます。  
  
 クエリを実行すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] により検索条件が調べられ、検索中のテーブルの各行に適用されます。 条件を満たす行は、クエリに加えられます。 たとえば、特定の地域の全従業員を検索する検索条件は、次のようになります。  
  
```  
region = 'UK'  
```  
  
 結果に行を含めるための条件を設定する場合は、複数の検索条件を使用できます。 たとえば、次の検索条件は、2 つの検索条件で構成されています。 両方の条件を満たす行だけが、クエリの結果セットに含められます。  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
 検索条件は AND または OR で結合できます。 前の例では AND を使用しています。 一方、次に示す条件では OR が使われています。 結果セットには、いずれか一方または両方の検索条件を満たす行が含まれます。  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
 1 つの列に対する複数の検索条件を結合することもできます。 たとえば、次の検索条件では、region 列に対する 2 つの条件が結合されています。  
  
```  
region = 'UK' OR region = 'US'  
```  
  
 検索条件の結合方法の詳細については、次の各トピックを参照してください。  
  
-   [抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [1 つの列に対して複数の検索条件を指定する (Visual Database Tools)](visual-database-tools.md)  
  
-   [複数の列に対して複数の検索条件を指定する (Visual Database Tools)](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [AND が優先する場合の条件を結合する (Visual Database Tools)](combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [OR が優先する場合の条件を結合する (Visual Database Tools)](combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>使用例  
 次に、さまざまな演算子と行抽出条件を使用したクエリの例を示します。  
  
-   **リテラル** 単独のテキスト、数値、日付、または論理値です。 次の例では、リテラルを使って、イギリス内の従業員に関する行をすべて検索します。  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **列参照** ある列の値と別の列の値を比較します。 次の例では、 `products` テーブルで製造費が輸送費より少ないすべての行を検索します。  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **関数** 関数を参照して、データベースのバックエンドで検索する値を計算します。 データベース サーバーで定義されている関数、またはスカラー値を返すユーザー定義関数を指定できます。 次の例では、今日発生した注文を検索します。GETDATE( ) 関数は今日の日付を返します。  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** 次の例では、 `authors` テーブルでファイルに名前のデータがあるすべての著者を検索します。  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **計算式** 計算結果がリテラル、列参照、または他の式になります。 次の例では、 `products` テーブルで小売り価格が製造費の 2 倍を超えるすべての行を検索します。  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>参照  
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [検索条件を指定&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [パラメーターを使用したクエリ (Visual Database Tools)](query-with-parameters-visual-database-tools.md)  
  
  
