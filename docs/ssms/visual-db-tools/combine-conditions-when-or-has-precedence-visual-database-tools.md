---
title: OR が優先する場合の条件の結合 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 13b64b2310f3ac29855dc4356fb842f86ef25dbc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262501"
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>OR が優先する場合の条件の結合 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
AND で結合した条件よりも OR で結合した条件を優先させるには、各 OR 条件に対して AND 条件を繰り返す必要があります。  
  
たとえば、5 年以上前に入社した従業員のうち、初級レベルの仕事に従事している従業員または退職した従業員を検索すると仮定します。 このクエリには、次の 3 つの条件が必要であり、その中の 2 つの条件に対して 1 つの条件を AND で結合する必要があります。  
  
-   入社日が 5 年以上前の従業員であり、  
  
-   職務レベルが 100 または状態が "R" (退職者を示す) の従業員  
  
抽出条件ペインでこの種のクエリを作成する方法を次の手順で説明します。  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>OR が優先する場合に条件を結合するには  
  
1.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)に検索するデータ列を追加します。 AND で結合された複数の条件を使用して同じ列を検索する場合は、検索する値ごとにデータ列名をグリッドに追加する必要があります。  
  
2.  複数の条件を OR で結合するには、最初の条件を **[フィルター]** グリッド列に、2 番目の条件を別の **[または...]** 列に入力します。3 番目以降の条件も同様に入力します。 たとえば、 `job_lvl` 列の条件と `status` 列の条件を OR で結合して検索するには、 `= 100` の **[フィルター]** 列に「 `job_lvl` 」、 `= 'R'` の **[または...]** 列に「 `status`」のように値を入力します。  
  
    グリッドに値を入力すると、SQL ペインでステートメントの WHERE 句が次のように作成されます。  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  各 OR 条件に 1 つずつ AND 条件を作成します。 該当する OR 条件と同じグリッド列に各 AND 条件を入力します。 たとえば、 `hire_date` 列を検索し、両方の OR 条件に適用される AND 条件を追加するには、[条件] 列と `< '1/1/91'` [または...] **列の両方に「** 」と入力します。  
  
    グリッドに値を入力すると、SQL ペインでステートメントの WHERE 句が次のように作成されます。  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > AND 条件を 1 回追加した後で、 **[編集]** メニューの **[切り取り]** および **[貼り付け]** をクリックすると、他の OR 条件に対しても同じ AND 条件を繰り返すことができます。  
  
クエリおよびビュー デザイナーによって作成される WHERE 句は、かっこを使用して OR が AND より優先することを示す次の WHERE 句と同じです。  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)に上の形式で検索条件を入力した後でダイアグラム ペインまたは抽出条件ペインでクエリを変更した場合、クエリおよびビュー デザイナーで再度作成される SQL ステートメントの形式は、両方の OR 条件に AND 条件が明示的に適用される形式になります。  
  
## <a name="see-also"></a>参照  
[抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
