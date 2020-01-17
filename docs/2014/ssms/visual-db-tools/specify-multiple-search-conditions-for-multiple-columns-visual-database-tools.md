---
title: 複数の列 (Visual Database Tools) に対して複数の検索条件の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3580f6365866ce752191e285b14f7d793be0cad0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204949"
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>複数の列に対して複数の検索条件を指定する (Visual Database Tools)
  検索条件に複数のデータ列を指定して、クエリの範囲を広くしたり狭くしたりできます。 たとえば、次の場合です。  
  
-   勤続年数が 5 年以上の従業員または特定の職務を担当している従業員を検索する場合  
  
-   特定の出版社によって出版された、料理に関する本を検索する場合  
  
 複数列のいずれかで値を検索するクエリを作成するには、OR 条件を指定します。 複数列ですべての条件を満たすクエリを作成するには、AND 条件を指定します。  
  
## <a name="specifying-an-or-condition"></a>OR 条件の指定  
 複数の条件を OR で結合するには、各条件を抽出条件ペインの個別の列で指定します。  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>2 つの異なる列に OR 条件を指定するには  
  
1.  [抽出条件ペイン](visual-database-tools.md)に検索する列を追加します。  
  
2.  最初に検索する列の **[フィルター]** 列に最初の条件を指定します。  
  
3.  2 番目に検索するデータ列の **[または...]** 列に 2 番目の条件を指定し、 **[フィルター]** 列は空白にしておきます。  
  
     クエリおよびビュー デザイナーは、OR 条件を含む WHERE 句を次のように作成します。  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  条件を追加するたびに、手順 2. および手順 3. を繰り返します。 新しい条件には、それぞれ別の **[または]** 列を使用します。  
  
## <a name="specifying-an-and-condition"></a>AND 条件の指定  
 条件を AND で結合して複数のデータ列を検索するには、グリッドの **[フィルター]** 列にすべての条件を指定します。  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>AND 条件を指定して 2 つの異なる列を検索するには  
  
1.  [抽出条件ペイン](visual-database-tools.md)に検索する列を追加します。  
  
2.  最初に検索するデータ列の **[フィルター]** 列に最初の条件を指定します。  
  
3.  2 番目のデータ列の **[フィルター]** 列に 2 番目の条件を指定します。  
  
     クエリおよびビュー デザイナーは、AND 条件を含む WHERE 句を次のように作成します。  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  条件を追加するたびに、手順 2. および手順 3. を繰り返します。  
  
## <a name="see-also"></a>参照  
 [AND が優先する場合の条件を結合&#40;Visual Database Tools&#41;](combine-conditions-when-and-has-precedence-visual-database-tools.md)   
 [OR が優先する場合の条件を結合&#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)   
 [抽出条件ペインで検索条件を結合するための規則&#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)   
 [検索基準の指定 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
