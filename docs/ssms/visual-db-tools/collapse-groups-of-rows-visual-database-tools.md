---
title: 行グループの集約 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea7a38c8030323b85c7198f0c6a12165b9d843d5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262574"
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>行グループの集約 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
基になるデータの行グループ全体に結果の各行が対応するようなクエリ結果を作成することができます。 行を集約するときは、次の点に注意してください。  
  
-   **重複する行を除外する** クエリによっては、同じ行が複数出現する結果セットが作成されます。 たとえば、著者の居住地の市町村名と州名を各行に含む結果セットを作成するとします。この場合、複数の著者が住む市町村があると、同じ行が複数作成されます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
    前のクエリで生成される結果セットは、あまり役に立ちません。 たとえば、ある市に 4 人の著者が住んでいる場合、結果セットには同じ行が 4 つ含まれることになります。 結果セットには市町村名と州名以外の列は含まれていないので、同じ行を相互に区別する方法はありません。 重複する行の生成を防ぐ 1 つの方法は、各行を区別する列を追加することです。 たとえば、著者の名前の列を加えると、同じ市内に同じ名前の著者が 2 人いない限り、各行を区別できるようになります。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
    ```  
  
    上記のクエリを使用すると問題の状況は回避できますが、この方法では、問題を根本的に解決することはできません。 つまり、結果セットから重複が除去される代わりに、結果セットが市町村に関するものではなくなってしまいます。 元の結果セットにあった重複を除去し、その上で各行が市町村の情報を示すようにするには、異なる行だけを返すクエリを作成します。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
    ```  
  
    重複除去の詳細については、「[重複する行の除外 (Visual Database Tools)](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md)」を参照してください。  
  
-   **行グループに対して計算を行う** 行グループの情報をまとめることができます。 たとえば、著者の居住する市と州の名前、およびその市に居住する著者の人数を各行に格納した結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ```  
  
    行グループに対する計算については、「[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)」と「[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)」を参照してください。  
  
-   **行グループを含む選択条件を使用する** たとえば、複数の著者が住んでいる市と州の名前、およびその市に住んでいる著者の数が各行に格納された結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
    ```  
  
    行グループに選択条件を適用する方法については、「[グループの条件を指定する方法 (Visual Database Tools)](../../ssms/visual-db-tools/specify-conditions-for-groups-visual-database-tools.md)」と「[同一クエリ内で HAVING 句および WHERE 句を使用する (Visual Database Tools)](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
