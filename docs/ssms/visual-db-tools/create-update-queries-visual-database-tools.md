---
title: 更新クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6f2f2102008976bd997ffae729907fb0d0e0f58
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266923"
---
# <a name="create-update-queries-visual-database-tools"></a>更新クエリの作成 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
更新クエリを使用すると、複数行の内容を一度に変更できます。 たとえば、 `titles` テーブルで更新クエリを使用すると、特定の出版社から出版されているすべての本の価格に、10% 加算するような処理を行うことができます。  
  
更新クエリを作成するときは、次の項目を指定します。  
  
-   更新するテーブル  
  
-   内容を更新する列  
  
-   各列の更新に使用する値または式  
  
-   更新する行を指定する検索条件  
  
たとえば、次のクエリは、特定の出版社から出版されているすべての本の価格に 10% 加算して `titles` テーブルを更新します。  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
> 更新クエリの実行アクションを元に戻すことはできません。 念のため、クエリを実行する前にデータをバックアップしてください。  
  
### <a name="to-create-an-update-query"></a>更新クエリを作成するには  
  
1.  更新するテーブルをダイアグラム ペインに追加します。  
  
2.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[更新]** をクリックします。  
  
    > [!NOTE]  
    > 更新クエリを開始した時点でダイアグラム ペインに複数のテーブルが表示されている場合、更新するテーブルの名前を要求する [[値の挿入先のテーブル選択] ダイアログ ボックス](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) が表示されます。  
  
3.  ダイアグラム ペインで、新しい値を指定する各列のチェック ボックスをオンにします。 クリックした列が抽出条件ペインに表示されます。 クエリに追加された列だけが更新されます。  
  
4.  抽出条件ペインの **[新しい値]** 列に列の更新値を入力します。 リテラル値、列名、または式を入力できます。 更新する列のデータ型と一致する値か、互換性のある値を入力してください。  
  
    > [!CAUTION]  
    > クエリおよびビュー デザイナーは、値の長さが更新する列の長さの範囲内であるかどうかをチェックできません。 指定した値が長すぎる場合、予告なしに切り捨てられることがあります。 たとえば、 `name` 列の長さが 20 文字である場合に 25 文字の更新値を指定すると、最後の 5 文字は切り捨てられることがあります。  
  
5.  更新する行を定義するために、 **[フィルター]** 列に検索条件を入力します。 詳細については、「[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)」を参照してください。  
  
    検索条件を指定しない場合は、指定されたテーブルのすべての行が更新されます。  
  
    > [!NOTE]  
    > 検索条件に使用する列を抽出条件ペインに追加すると、更新される列のリストにこの列も追加されます。 検索条件としては使用するが更新しない場合は、テーブルまたはテーブル値オブジェクトを示す四角形内の列名の横のチェック ボックスをオフにします。  
  
更新クエリを実行しても、 [結果ペイン](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)には結果が表示されません。 代わりに、変更された行数を示すメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[サポートされるクエリの種類 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
