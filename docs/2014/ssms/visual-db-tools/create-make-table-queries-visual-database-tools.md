---
title: テーブルの作成クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f53a0cdb7ccc30afb425197d12dad2b9ca5fa345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676307"
---
# <a name="create-make-table-queries-visual-database-tools"></a>テーブルの作成クエリの作成 (Visual Database Tools)
  テーブルの作成クエリを使用すると、新しいテーブルに行をコピーできます。これは、処理するデータのサブセットを作成したり、データベース間でテーブルの内容をコピーしたりするのに役立ちます。 テーブルの作成クエリは結果の挿入クエリと似ていますが、新しいテーブルを作成してそこに行をコピーする点で異なります。  
  
 テーブルの作成クエリを作成するときは、次の項目を指定します。  
  
-   新しいデータベース テーブル (コピー先テーブル) の名前。  
  
-   行のコピー元として使用するテーブル (コピー元テーブル)。 1 つのテーブルまたは結合テーブルのいずれからでもコピーできます。  
  
-   内容をコピーするコピー元テーブルの列。  
  
-   行を特定の順序でコピーする場合は、並べ替え順序。  
  
-   コピーする行を定義する検索条件。  
  
-   集計情報だけをコピーする場合は、[グループ化] オプション。  
  
 たとえば、次のクエリでは、新しく作成した `uk`_`customers` というテーブルに `customers` テーブルの情報をコピーします。  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
 テーブルの作成クエリを正しく使用するには、次の条件を満たす必要があります。  
  
-   データベースが SELECT...INTO 構文をサポートしている。  
  
-   目的のデータベースにテーブルを作成する権限がある。  
  
### <a name="to-create-a-make-table-query"></a>テーブルの作成クエリを作成するには  
  
1.  ダイアグラム ペインにコピー元テーブルを追加します。  
  
2.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[テーブルの作成]** をクリックします。  
  
3.  **[テーブルの作成]** ダイアログ ボックスで、コピー先テーブルの名前を入力します。 クエリおよびビュー デザイナーでは、名前が既に使用されているかどうかや、テーブルを作成する権限があるかどうかなどの確認は行われません。  
  
     他のデータベースにコピー先テーブルを作成するには、目的のデータベース名、所有者 (必要な場合)、およびテーブル名を含む完全なテーブル名を指定します。  
  
4.  コピーする列を指定するために、クエリに列を追加します。 詳しくは、「[クエリに列を追加する方法 (Visual Database Tools)](visual-database-tools.md)」をご覧ください。 クエリに追加した列だけがコピーされます。 行全体をコピーする **\* (すべての列)** します。  
  
     クエリおよびビュー デザイナーにより、選択した列が、抽出条件ペインの **[列]** 列に追加されます。  
  
5.  特定の順序で行をコピーする場合は、並べ替え順序を指定します。 詳しくは、「 **クエリ結果の並べ替えおよびグループ化**」をご覧ください。  
  
6.  コピーする行を指定するために、検索条件を入力します。 詳細については、「[検索基準の指定 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)」を参照してください。  
  
     検索条件を指定しなかった場合は、コピー元テーブルのすべての行がコピー先テーブルにコピーされます。  
  
    > [!NOTE]  
    >  検索する列を抽出条件ペインに追加すると、コピーする列の一覧にその列も追加されます。 検索に使用する列をコピーしない場合は、テーブルまたはテーブル構造オブジェクトを示す四角形内の列名の横のチェック ボックスをオフにします。  
  
7.  集計情報をコピーする場合は、[グループ化] オプションを指定します。 詳細については、「[クエリ結果の要約 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)」を参照してください。  
  
 テーブルの作成クエリを実行しても、 [結果ペイン](results-pane-visual-database-tools.md)には結果が表示されません。 代わりに、コピーされた行数を示すメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [クエリの種類 (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
