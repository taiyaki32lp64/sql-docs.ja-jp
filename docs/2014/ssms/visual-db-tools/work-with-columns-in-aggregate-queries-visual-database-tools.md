---
title: 集計クエリにおける列の使用 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c14608a34c2df5a0e93fea985d8135a37d5ffa53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273277"
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>集計クエリにおける列の使用 (Visual Database Tools)
  集計クエリを作成する場合、 [クエリおよびビュー デザイナー](visual-database-tools.md) は有効なクエリを構築できるように一定の仮説に基づいた処理を行います。 たとえば、集計クエリを作成するときに、あるデータ列を出力するように指定した場合、その列は自動的に GROUP BY 句に含められ、個別の行の内容が誤って要約に表示されるのを防ぎます。  
  
## <a name="using-group-by"></a>GROUP BY の使用  
 クエリおよびビュー デザイナーは、次のガイドラインに従って列を処理します。  
  
-   [グループ化] オプションを選択したり、クエリに集計関数を追加したりすると、出力が指定されている列または並べ替えの対象となる列はすべて、自動的に GROUP BY 句に追加されます。 既に集計関数の一部になっている列は、自動的に GROUP BY 句に追加されることはありません。  
  
     特定の列を GROUP BY 句に含めないようにするには、抽出条件ペインの [グループ化] 列で別のオプションを選択し、手動で変更する必要があります。 ただし、オプションを選択した結果、クエリが実行できなくなる場合もあります。クエリおよびビュー デザイナーでは、これが回避されません。  
  
-   抽出条件ペインまたは SQL ペインで集計関数にクエリ出力列を手動で追加した場合でも、他の出力列がクエリから自動的に削除されることはありません。 したがって、残りの列をクエリ出力から削除するか、GROUP BY 句または集計関数の一部にする必要があります。  
  
 抽出条件ペインの [フィルター] 列に検索条件を入力すると、クエリおよびビュー デザイナーは次の規則に従います。  
  
-   集計クエリを指定していないためにグリッドの **[グループ化]** 列が表示されていない場合、検索条件は WHERE 句に配置されます。  
  
-   既に集計クエリを指定していて、 **[グループ化]** 列の **[Where]** オプションを選択している場合、検索条件は WHERE 句に配置されます。  
  
-   **[グループ化]** 列に **[Where]** 以外の値が指定されている場合、検索条件は HAVING 句に配置されます。  
  
## <a name="using-the-having-and-where-clauses"></a>HAVING 句と WHERE 句の使用  
 次の原則は、検索条件で集計クエリの列を参照する方法を説明したものです。 通常、検索条件に列を使用すると、集約する行をフィルターで選択したり (WHERE 句)、最終出力に表示されるグループ化の結果を決定したり (HAVING 句) できます。  
  
-   個別のデータ列は、クエリ内の他の場所でどのように使われているかよって、WHERE 句または HAVING 句に含めることができます。  
  
-   WHERE 句は、集計およびグループ化する行のサブセットを選択するために使用されるので、グループ化の前に適用されます。 したがって、データ列が GROUP BY 句の一部でない場合や、集計関数に含まれていない場合でも、WHERE 句で使用できます。 たとえば、次のステートメントでは、価格が $10.00 を超えるすべての書名を選択し、平均価格を計算します。  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   GROUP BY 句または集計関数で使われている列を含めて検索条件を作成する場合、検索条件は WHERE 句または HAVING 句として使用できます。どちらを使用するはその条件の作成時に決定できます。 たとえば、次のステートメントでは、出版社ごとに本の平均価格を計算し、$10.00 を超える出版社の平均価格を表示します。  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   検索条件の中で集計関数を使う場合は、条件に集計を含むことになるため、HAVING 句に入れる必要があります。  
  
## <a name="see-also"></a>参照  
 [クエリ結果の要約&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
  
