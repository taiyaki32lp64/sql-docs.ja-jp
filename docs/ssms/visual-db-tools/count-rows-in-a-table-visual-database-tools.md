---
title: テーブルの行数のカウント (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21f0b7becfae6c2656fd9a5f416decd32787e165
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266971"
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>テーブルの行数のカウント (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
テーブルの行数をカウントすることにより、次の内容を確認できます。  
  
-   テーブルの行の総数。たとえば、 `titles` テーブルの本の総数を確認できます。  
  
-   テーブルで特定の条件を満たす行の数。たとえば、 `titles` テーブルの本のうち、ある出版社の本の数を確認できます。  
  
-   特定の列の値の数。  
  
列の値をカウントするとき、NULL はカウントされません。 たとえば、 `titles` テーブルの本のうち、 `advance` 列に値のある本の数をカウントできます。 既定では、一意の値だけでなく、すべての値がカウントされます。  
  
上記の 3 種類のカウント手順はほぼ同じです。  
  
### <a name="to-count-all-the-rows-in-a-table"></a>テーブルの行の総数をカウントするには  
  
1.  集計するテーブルが、既にダイアグラム ペインに存在していることを確認します。  
  
2.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[グループ化を追加]** を選択します。 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) により、抽出条件ペインのグリッドに **[グループ化]** 列が追加されます。  
  
3.  テーブルまたはテーブル値オブジェクトを示す四角形の中で、 **[&#42; (すべての列)]** を選択します。  
  
    クエリおよびビュー デザイナーにより、抽出条件ペインの **[グループ化]** 列に **[カウント]** という語句が自動的に入力され、集計する列に列の別名が割り当てられます。 この自動的に割り当てられた別名は、わかりやすい名前に変更することができます。 詳細については、「[列の別名の作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)」を参照してください。  
  
4.  クエリを実行します。  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>条件を満たす行の総数をカウントするには  
  
1.  集計するテーブルが、既にダイアグラム ペインに存在していることを確認します。  
  
2.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[グループ化を追加]** を選択します。 クエリおよびビュー デザイナーにより、抽出条件ペインのグリッドに **[グループ化]** 列が追加されます。  
  
3.  テーブルまたはテーブル構造オブジェクトを示す四角形の中で、 **[&#42;(すべての列)]** を選択します。  
  
    クエリおよびビュー デザイナーにより、抽出条件ペインの **[グループ化]** 列に **[カウント]** という語句が自動的に入力され、集計する列に列の別名が割り当てられます。 クエリ出力に表示する列ヘッダーをわかりやすくするには、「[列の別名の作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)」を参照してください。  
  
4.  検索するデータ列を追加し、 **[出力]** 列のチェック ボックスをオフにします。  
  
    クエリおよびビュー デザイナーにより、グリッドの **[グループ化]** 列に **[グループ化]** という語句が自動的に入力されます。  
  
5.  **[グループ化]** 列の **[グループ化]** を **[Where 条件]** に変更します。  
  
6.  検索するデータ列の **[フィルター]** 列に検索条件を入力します。  
  
7.  クエリを実行します。  
  
### <a name="to-count-the-values-in-a-column"></a>列の値をカウントするには  
  
1.  集計するテーブルが、既にダイアグラム ペインに存在していることを確認します。  
  
2.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[グループ化を追加]** を選択します。 クエリおよびビュー デザイナーにより、抽出条件ペインのグリッドに **[グループ化]** 列が追加されます。  
  
3.  カウントする列を抽出条件ペインに追加します。  
  
    クエリおよびビュー デザイナーにより、グリッドの **[グループ化]** 列に **[グループ化]** という語句が自動的に入力されます。  
  
4.  **[グループ化]** 列の **[グループ化]** を **[カウント]** に変更します。  
  
    > [!NOTE]  
    > 一意の値だけをカウントする場合は、 **[個別のカウント]** を選択します。  
  
5.  クエリを実行します。  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
