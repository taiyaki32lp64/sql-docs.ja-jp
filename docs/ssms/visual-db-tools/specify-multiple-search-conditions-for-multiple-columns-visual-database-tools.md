---
title: 複数の列に対して複数の検索条件を指定する | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1110e4ae1ca4268af611cbb039af2b148694b552
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265500"
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>複数の列に対して複数の検索条件を指定する (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
検索条件に複数のデータ列を指定して、クエリの範囲を広くしたり狭くしたりできます。 たとえば、次の場合です。  
  
-   勤続年数が 5 年以上の従業員または特定の職務を担当している従業員を検索する場合  
  
-   特定の出版社によって出版された、料理に関する本を検索する場合  
  
複数列のいずれかで値を検索するクエリを作成するには、OR 条件を指定します。 複数列ですべての条件を満たすクエリを作成するには、AND 条件を指定します。  
  
## <a name="specifying-an-or-condition"></a>OR 条件の指定  
複数の条件を OR で結合するには、各条件を抽出条件ペインの個別の列で指定します。  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>2 つの異なる列に OR 条件を指定するには  
  
1.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)に検索する列を追加します。  
  
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
  
1.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)に検索する列を追加します。  
  
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
[AND が優先する場合の条件を結合する (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[OR が優先される場合の条件の結合 (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
