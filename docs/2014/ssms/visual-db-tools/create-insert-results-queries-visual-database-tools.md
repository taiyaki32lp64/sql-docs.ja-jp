---
title: 結果の挿入クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebffc2246f0940c4643af2267086e727882a0633
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63031973"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>結果の挿入クエリの作成 (Visual Database Tools)
  結果の挿入クエリを使用すると、テーブル間またはテーブル内で行をコピーできます。 たとえば、 `titles` テーブルで結果の挿入クエリを使用すると、特定の出版社のすべての書名に関する情報を別のテーブルにコピーして、その出版社に提供できます。 結果の挿入クエリは、テーブルの作成と似ていますが、既存のテーブルに行をコピーする点が異なります。  
  
> [!TIP]  
>  テーブル間の行のコピーは、カット アンド ペーストを使用して行うこともできます。 これにはまず、各テーブルに対するクエリを作成して実行します。 次に、必要な行を結果グリッドから別の結果グリッドにコピーします。  
  
 結果の挿入クエリを作成するときは、次の項目を指定します。  
  
-   行のコピー先のデータベース テーブル (コピー先テーブル)。  
  
-   行のコピー元として使用するテーブル (コピー元テーブル)。 コピー元テーブルはサブクエリの一部となります。 同じテーブル内にコピーする場合、コピー元とコピー先は同じテーブルです。  
  
-   内容をコピーするコピー元テーブルの列。  
  
-   データのコピー先となるコピー先テーブルの列。  
  
-   コピーする行を定義する検索条件。  
  
-   行を特定の順序でコピーする場合は、並べ替え順序。  
  
-   集計情報だけをコピーする場合は、[グループ化] オプション。  
  
 たとえば、次のクエリでは、 `titles` テーブルの書名情報を `archivetitles`というアーカイブ テーブルにコピーします。 このクエリでは、特定の出版社のすべての書名に関する 4 つの列の内容をコピーします。  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  新しい行に値を挿入するには、値挿入クエリを使用します。  
  
 行の特定の列の内容をコピーする方法と、行のすべての列の内容をコピーする方法があります。 どちらの方法でも、コピー元のデータには、コピー先の行の列との互換性が必要です。 たとえば、 `price`などの列の内容をコピーする場合、コピー先の行の列には、小数点を含む数値データを入力できる必要があります。 行全体をコピーする場合、コピー先テーブルには、互換性のある列がコピー元テーブルと同じ順序で存在する必要があります。  
  
 結果の挿入クエリを作成すると、データのコピーに使用できるオプションが抽出条件ペインに表示されます。 また、データのコピー先となる列を指定できるように、[追加] 列が追加されます。  
  
> [!CAUTION]  
>  結果の挿入クエリの実行アクションを元に戻すことはできません。 念のため、クエリを実行する前にデータをバックアップしてください。  
  
### <a name="to-create-an-insert-results-query"></a>結果の挿入クエリを作成するには  
  
1.  新しいクエリを作成して、行のコピー元となるテーブル (コピー元テーブル) を追加します。 同じテーブル内で行をコピーする場合は、コピー先テーブルと同じコピー元テーブルを追加します。  
  
2.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[結果の挿入]** をクリックします。  
  
3.  [[挿入先のテーブル選択] ダイアログ ボックス](visual-database-tools.md)で、行のコピー先となるテーブル (コピー先テーブル) を選択します。  
  
    > [!NOTE]  
    >  クエリおよびビュー デザイナーは、更新できるテーブルおよびビューを事前に判別できません。 そのため、 **[挿入先のテーブル選択]** ダイアログ ボックスの **[テーブル名]** ボックスには、クエリを実行するデータ接続で使用できるテーブルおよびビューがすべて表示されます。行をコピーできないテーブルおよびビューも表示されます。  
  
4.  テーブルまたはテーブル値オブジェクトを示す四角形で、内容をコピーする列の名前を選択します。 行全体をコピーする **\* (すべての列)** します。  
  
     選択した列が、抽出条件ペインの **[列]** 列に追加されます。  
  
5.  抽出条件ペインの **[追加]** 列で、コピーする各列に対してコピー先テーブルの目的の列を選択します。 選択*tablename\* 。* 行全体をコピーする場合。 コピー先テーブルの列は、コピー元テーブルの列と同じデータ型か、互換性のあるデータ型である必要があります。  
  
6.  特定の順序で行をコピーする場合は、並べ替え順序を指定します。 詳細については、「[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)」を参照してください。  
  
7.  コピーする行を指定するために、 **[フィルター]** 列に検索条件を入力します。 詳細については、「[検索基準の指定 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)」を参照してください。  
  
     検索条件を指定しなかった場合は、コピー元テーブルのすべての行がコピー先テーブルにコピーされます。  
  
    > [!NOTE]  
    >  検索する列を抽出条件ペインに追加すると、コピーする列の一覧にその列も追加されます。 検索に使用する列をコピーしない場合は、テーブルまたはテーブル値オブジェクトを示す四角形内の列名の横のチェック ボックスをオフにします。  
  
8.  集計情報をコピーする場合は、[グループ化] オプションを指定します。 詳細については、「[クエリ結果の要約 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)」を参照してください。  
  
 結果の挿入クエリを実行しても、[結果ペイン](results-pane-visual-database-tools.md)に結果は表示されません。 代わりに、コピーされた行数を示すメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
 [クエリの種類&#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
