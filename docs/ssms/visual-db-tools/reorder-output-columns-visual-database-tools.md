---
title: 列の出力順の変更 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reordering output columns [SQL Server]
- output columns [SQL Server]
ms.assetid: 76462885-de4a-4290-a26b-90696d3671f4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8ea54ee09a6e2c03548779e591aed5d260b54d49
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255892"
---
# <a name="reorder-output-columns-visual-database-tools"></a>列の出力順の変更 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
選択クエリにデータ列を追加する順序によって、結果での列の表示順序が決まります。 最初にクエリに追加した列は結果の左端に表示され、次に追加した列はその右隣に表示されます。  
  
また、更新クエリや挿入クエリを作成する場合、追加した列の順序は、データの処理順序に反映されます。  
  
そのため、データ列を並べ替えると、結果セットの列が表示される順序や処理される順序を変更できます。  
  
### <a name="to-reorder-columns-for-output"></a>列の出力順を変更するには  
  
1.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)で、対象の列を含む行の左側にある行セレクター ボタンをクリックして、行を選択します。  
  
2.  行セレクター ボタンにポインターを置き、行を新しい場所にドラッグします。  
  
    \- または -  
  
    [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)で列名の順序を編集します。  
  
> [!TIP]  
> 抽出条件ペインの特定の場所にデータ行を追加するには、抽出条件ペインの該当する場所に空白行を挿入し、その行に挿入するデータ列を指定します。 詳しくは、「[クエリに列を追加する方法 (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
