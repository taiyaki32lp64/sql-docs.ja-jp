---
title: 値の挿入クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1512d4a0ad9c3e48b93e7fdf6b993adb3fc4f9fd
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264910"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>値の挿入クエリの作成 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
値の挿入クエリを使用すると、現在のテーブルに新しい行を作成できます。 値の挿入クエリを作成するときは、次の項目を指定します。  
  
-   行を追加するデータベース テーブル  
  
-   内容を追加する列  
  
-   各列に挿入する値または式  
  
たとえば、次のクエリでは、書名、種類、出版社、価格の値を指定した行を `titles` テーブルに追加します。  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
値の挿入クエリを作成すると、新しい行の挿入に使用できるオプション (列名および挿入値) だけが抽出条件ペインに表示されます。  
  
> [!CAUTION]  
> 値の挿入クエリの実行アクションを元に戻すことはできません。 念のため、クエリを実行する前にデータをバックアップしてください。  
  
### <a name="to-create-an-insert-values-query"></a>値の挿入クエリを作成するには  
  
1.  更新するテーブルをダイアグラム ペインに追加します。  
  
2.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[値の挿入]** をクリックします。  
  
    > [!NOTE]  
    > 値の挿入クエリを開始した時点でダイアグラム ペインに複数のテーブルが表示されている場合、更新するテーブルの名前を要求する [[値の挿入先のテーブル選択] ダイアログ ボックス](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) が表示されます。  
  
3.  ダイアグラム ペインで、新しい値を指定する各列のチェック ボックスをオンにします。 クリックした列が抽出条件ペインに表示されます。 クエリに追加された列だけが更新されます。  
  
4.  抽出条件ペインの **[新しい値]** 列に列の新しい値を入力します。 リテラル値、列名、または式を入力できます。 更新する列のデータ型と一致する値か、互換性のある値を入力してください。  
  
    > [!CAUTION]  
    > クエリおよびビュー デザイナーは、値の長さが挿入する列の長さの範囲内であるかどうかをチェックできません。 指定した値が長すぎる場合、予告なしに切り捨てられることがあります。 たとえば、 `name` 列の長さが 20 文字である場合に 25 文字の挿入値を指定すると、最後の 5 文字は切り捨てられることがあります。  
  
値の挿入クエリを実行しても、 [結果ペイン](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)には結果が表示されません。 代わりに、変更された行数を示すメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[サポートされるクエリの種類 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
