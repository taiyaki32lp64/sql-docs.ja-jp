---
title: 1 つの列に対して複数の検索条件を指定する方法 | Microsoft Docs
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
ms.assetid: 2c006e36-56b1-4992-89b4-c6c0b19808f3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 519dbfa8d8ce0d3e80df9abe1532813dca63f0e9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263615"
---
# <a name="specify-multiple-search-conditions-for-one-column-visual-database-tools"></a>1 つの列に対して複数の検索条件を指定する方法 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
場合によっては、同じデータ列に複数の検索条件を適用する必要があります。 たとえば、次の場合です。  
  
-   `employee` テーブルから複数の従業員名を検索したり、異なる給与範囲の従業員を検索したりする場合。 この種の検索には OR 条件を使用します。  
  
-   "The" で始まり、"Cook" を含む書名を検索する場合。 この種の検索には AND 条件を使用します。  
  
> [!NOTE]  
> このトピックの内容は、クエリの WHERE 句および HAVING 句の検索条件に該当します。 例では WHERE 句の作成を取り扱いますが、どちらの句の検索条件にも同じ原則が当てはまります。  
  
同じデータ列で代替値を検索するには、OR 条件を指定します。 複数の条件を満たす値を検索するには、AND 条件を指定します。  
  
## <a name="specifying-an-or-condition"></a>OR 条件の指定  
OR 条件を使用すると、1 つの列に対して複数の代替値を検索条件として指定できます。 この方法では検索範囲が広くなるため、1 つの値を検索した場合に比べて、検索結果として返される行数が多くなります。  
  
> [!TIP]  
> 同じデータ列で複数の値を検索する代わりに、IN 演算子を使用する方法もあります。  
  
#### <a name="to-specify-an-or-condition"></a>OR 条件を指定するには  
  
1.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)に検索する列を追加します。  
  
2.  追加したデータ列の **[フィルター]** 列に最初の条件を指定します。  
  
3.  同じデータ列の **[または...]** 列に、2 番目の条件を指定します。  
  
クエリおよびビュー デザイナーは、OR 条件を含む WHERE 句を次のように作成します。  
  
```  
SELECT fname, lname  
FROM employees  
WHERE (salary < 30000) OR (salary > 100000)  
```  
  
## <a name="specifying-an-and-condition"></a>AND 条件の指定  
AND 条件を使用すると、複数の条件を満たす列の値だけが、結果セットの行に含まれるように指定できます。 この方法では検索範囲が狭くなるため、通常は、1 つの値を検索した場合よりも、検索結果として返される行数が少なくなります。  
  
> [!TIP]  
> 一定の範囲の値を検索する場合は、2 つの条件を AND で結合する代わりに、BETWEEN 演算子を使用する方法があります。  
  
#### <a name="to-specify-an-and-condition"></a>AND 条件を指定するには  
  
1.  抽出条件ペインに検索する列を追加します。  
  
2.  追加したデータ列の **[フィルター]** 列に最初の条件を指定します。  
  
3.  抽出条件ペインのグリッドの空白行に再度同じデータ列を追加します。  
  
4.  2 番目のデータ列の **[フィルター]** 列に 2 番目の条件を指定します。  
  
クエリ デザイナーは、AND 条件を含む WHERE 句を次のように作成します。  
  
```  
SELECT title_id, title  
FROM titles  
WHERE (title LIKE '%Cook%') AND   
  (title LIKE '%Recipe%')  
```  
  
## <a name="see-also"></a>参照  
[抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
