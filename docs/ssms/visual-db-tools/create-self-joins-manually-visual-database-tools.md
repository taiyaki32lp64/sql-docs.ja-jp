---
title: 自己結合の手動作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5ef290600a71b502df47dc873ef68c941ee833bd
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264279"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>自己結合の手動作成 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
データベースでテーブルに再帰リレーションシップが設定されていなくても、テーブルをテーブル自身に結合できます。 たとえば、自己結合を使用して、同じ市に住む著者の組を検索できます。  
  
他の結合と同様に、自己結合にも少なくとも 2 つのテーブルが必要です。 他の結合と異なる点は、クエリに他のテーブルを追加する代わりに、同じテーブルの 2 番目のインスタンスを追加する点です。 このように、テーブルの最初のインスタンスの列と 2 番目のインスタンスの同じ列を比較することによって、列の値を相互に比較できます。 テーブルの 2 番目のインスタンスには、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) によって別名が割り当てられます。  
  
たとえば、自己結合を作成してバークレイに住む著者の組み合わせをすべて検索する場合は、テーブルの最初のインスタンスの `city` 列と 2 番目のインスタンスの `city` 列とを比較します。 作成したクエリは次のようになります。  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
自己結合の作成には、複数の結合条件が必要になることがあります。 その理由を理解するために、上記のクエリの結果を検討してみます。  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
最初の行は、Cheryl Carson が Cheryl Carson と同じ市に住んでいることを示すため、意味がありません。 2 番目の行も同様に役に立ちません。 これらの無意味なデータを削除するために、2 つの著者名が違う著者を示す場合だけ結果行を残すように条件を追加します。 作成したクエリは次のようになります。  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
結果セットは、次のように改善されます。  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
しかしこの 2 つの結果行も冗長です。 最初の行は、Carson が Bennet と同じ市に住んでいることを示し、2 番目の行は、Bennet が Carson と同じ市に住んでいることを示しています。 このような冗長を避けるには、2 番目の結合条件を "等しくない" から "小なり" に変更します。 作成したクエリは次のようになります。  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
結果セットは次のようになります。  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>自己結合を手動作成するには  
  
1.  処理するテーブルまたはテーブル値オブジェクトを [ダイアグラム ペイン](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) に追加します。  
  
2.  同じテーブルを再度追加します。ダイアグラム ペインに同じテーブルまたはテーブル値オブジェクトが 2 つ表示されます。  
  
    2 番目のインスタンスには、テーブル名の後に順序番号が付加された別名が割り当てられます。 さらに、ダイアグラム ペインの中のテーブルまたはテーブル値オブジェクトの 2 つのインスタンスの間に結合線が表示されます。  
  
3.  結合線を右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
4.  [プロパティ] ウィンドウの **[結合条件と種類]** をクリックし、プロパティの右側の省略記号 **[...]** をクリックします。  
  
5.  [[結合]](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md) ダイアログ ボックスで、主キー間の比較演算子を必要に応じて変更します。 たとえば、演算子を小なり (<) に変更できます。  
  
6.  テーブルまたはテーブル値オブジェクトの最初のインスタンスにある最初の結合列の名前をドラッグし、2 番目のインスタンスの対応する列にドロップして、追加の結合条件 (たとえば、authors.zip = authors1.zip) を作成します。  
  
7.  出力列、検索条件、並べ替え順序など、クエリの他のオプションを指定します。  
  
## <a name="see-also"></a>参照  
[自己結合の自動作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
