---
title: クエリへのテーブルの追加 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3be181b428645226cf6e3d675fbab06b9bf4ca11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263712"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>クエリへのテーブルの追加 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
クエリを作成するとき、データを取得する基となるのは、テーブルまたはテーブル構造オブジェクト (ビューおよび特定のユーザー定義関数など) です。 クエリでこれらのオブジェクトを処理するには、 **ダイアグラム ペイン**にオブジェクトを追加します。  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>テーブルまたはテーブル値オブジェクトをクエリに追加するには  
  
1.  クエリおよびビュー デザイナーの **ダイアグラム ペイン** で、背景を右クリックして、ショートカット メニューの **[テーブルの追加]** をクリックします。  
  
2.  **[テーブルの追加]** ダイアログ ボックスで、クエリに追加するオブジェクトの種類に相当するタブを選択します。  
  
3.  アイテムのリストで、追加する各アイテムをダブルクリックします。  
  
4.  アイテムの追加が完了したら、 **[閉じる]** をクリックします。  
  
    クエリおよびビュー デザイナーによって、 **ダイアグラム ペイン**、 **抽出条件ペイン**、および **SQL ペイン** が適宜更新されます。  
  
SQL ペインのステートメントでテーブルおよびビューを参照すると、テーブルおよびビューはクエリに自動的に追加されます。  
  
テーブルまたはテーブル値オブジェクトに対して十分なアクセス権がない場合、またはプロバイダーがこれらのオブジェクトに関する情報を返すことができない場合、クエリおよびビュー デザイナーにはこれらのオブジェクトのデータ列が表示されません。 この場合、テーブルまたはテーブル値オブジェクトのタイトル バーおよび [* (すべての列)] チェック ボックスだけが表示されます。  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>新しいクエリに既存のクエリを追加するには  
  
1.  作成する新しいクエリに **SQL ペイン** が表示されていることを確認します。  
  
2.  **SQL ペイン**で、FROM の後に () (かっこ) を入力します。  
  
3.  既存のクエリをクエリ デザイナーで開きます。 この時点で 2 つのクエリ デザイナーが開いています。  
  
4.  新しい外部クエリに含める既存のクエリ、つまり内部クエリの **SQL ペイン** を表示します。  
  
5.  **SQL ペイン**のすべてのテキストを選択し、クリップボードにコピーします。  
  
6.  新しいクエリの **SQL ペイン** の中をクリックし、追加したかっこの間にカーソルを移動し、クリップボードの内容を貼り付けます。  
  
7.  **SQL ペイン**の中で、右かっこの後に別名を追加します。  
  
## <a name="see-also"></a>参照  
[テーブルの別名の作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[クエリからのテーブルの削除 (Visual Database Tools)](../../ssms/visual-db-tools/remove-tables-from-queries-visual-database-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
