---
title: 抽出条件ペイン (Visual Database Tools) で検索条件を組み合わせる場合の規則 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- multiple OR clauses
- combining search conditions
- OR operator
- AND, Criteria pane
- multiple AND clauses
ms.assetid: d4859be5-ff5b-48b2-a101-ad40c6dbcc68
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a1022770526386640f0ad2aa114a2161ba16dc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63140379"
---
# <a name="conventions-for-combining-search-conditions-in-the-criteria-pane-visual-database-tools"></a>抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)
  クエリを作成する際には、任意の数の AND および OR 演算子で結合して任意の数の検索条件を含めることができます。 AND 句と OR 句を組み合わせたクエリは複雑になる場合があるため、そのようなクエリを実行したときにどのように解釈されるのか、およびそのようなクエリが[抽出条件ペイン](visual-database-tools.md)と [SQL ペイン](sql-pane-visual-database-tools.md)でどのように表現されるのかについて理解しておくと役に立ちます。  
  
> [!NOTE]  
>  AND 演算子または OR 演算子を 1 つだけ含む検索条件の詳細については、「[1 つの列に対して複数の検索条件を指定する (Visual Database Tools)](specify-multiple-search-conditions-for-one-column-visual-database-tools.md)」および「[複数の列に対して複数の検索条件を指定する (Visual Database Tools)](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)」を参照してください。  
  
 ここでは、以下について説明します。  
  
-   AND と OR の両方を含むクエリでの AND と OR の優先順位。  
  
-   AND 句と OR 句の条件の論理的な関係。  
  
-   クエリおよびビュー デザイナーの抽出条件ペインで、AND と OR の両方を含むクエリがどのように表現されるか。  
  
 以降の説明を理解しやすくするために、 `employee` テーブルに `hire_date`、 `job_lvl`、および `status`という列が含まれる場合を考えます。 以降の例では、各従業員がどのくらい長く会社に勤めているか (つまり、従業員が雇用された日付)、どのような種類の仕事をしているか (仕事のレベル)、従業員のステータス (退職など) などの情報が必要であると仮定しています。  
  
## <a name="precedence-of-and-and-or"></a>AND と OR の優先順位  
 クエリが実行されると、AND で結合された句が最初に評価され、次に OR で結合された句が評価されます。  
  
> [!NOTE]  
>  NOT 演算子は AND と OR のいずれよりも優先されます。  
  
 たとえば、初級レベルの仕事に 5 年以上勤務している従業員か、雇用された日付に関係なく中級レベルの仕事をしている従業員のいずれかを検索する場合は、次のような WHERE 句を作成できます。  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   job_lvl = 100 OR  
   job_lvl = 200  
  
```  
  
 AND が OR に優先する既定の優先順位をオーバーライドする場合は、SQL ペインで特定の条件をかっこで囲みます。 かっこで囲まれた条件は常に最初に評価されます。 たとえば、初級レベルまたは中級レベルの仕事に 5 年以上勤務している従業員をすべて検索する場合は、次のような WHERE 句を作成できます。  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
> [!TIP]  
>  わかりやすくするために、AND 句と OR 句を組み合わせるときは既定の優先順位を利用する代わりに、常にかっこを使用することをお勧めします。  
  
## <a name="how-and-works-with-multiple-or-clauses"></a>複数の OR 句に対する AND の解釈  
 AND 句と OR 句を組み合わせたときのそれぞれの関係について把握すると、クエリおよびビュー デザイナーで複雑なクエリを作成し、それを理解するのに役立ちます。  
  
 AND を使用して複数の条件を結合した場合、AND で結合された最初の条件のセットは、2 番目のセットの条件すべてに適用されます。 つまり、AND によって他の条件に結合された条件は、2 番目のセット内のすべての条件に分配されます。 たとえば、次の概略表現は、OR 条件のセットに結合された AND 条件を示しています。  
  
```  
A AND (B OR C)  
```  
  
 この表現は、次の概略表現と論理的に等価です。ここでは、AND 条件が 2 番目の条件のセットにどのように分配されるかが示されています。  
  
```  
(A AND B) OR (A AND C)  
```  
  
 この分散法則は、クエリおよびビュー デザイナーの使用方法に影響します。 たとえば、初級レベルまたは中級レベルの仕事に 5 年以上勤務している従業員をすべて検索する場合を考えます。 SQL ペインで次の WHERE 句をステートメントに入力します。  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
 AND で結合されている句は、OR で結合されている両方の句に適用されます。 これを明確に表現する方法は、OR 句の各条件に対して 1 回ずつ AND 条件を繰り返すことです。 次のステートメントは上記のステートメントよりも明確であると同時に長くなっていますが、論理的には等価です。  
  
```  
WHERE    (hire_date < '01/01/95' ) AND  
  (job_lvl = 100) OR   
  (hire_date < '01/01/95' ) AND   
  (job_lvl = 200)  
```  
  
 結合されている OR 句に AND 句を分配する法則は、含まれるそれぞれの条件の数に関係なく適用されます。 たとえば、5 年以上勤務しているか、または退職した上級レベルまたは中級レベルの従業員を検索する場合を考えます。 WHERE 句は次のようになります。  
  
```  
WHERE   
   (job_lvl = 200 OR job_lvl = 300) AND  
   (hire_date < '01/01/95' ) OR (status = 'R')  
```  
  
 AND で結合された条件を分配すると、WHERE 句は次のようになります。  
  
```  
WHERE   
   (job_lvl = 200 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 200 AND status = 'R') OR  
   (job_lvl = 300 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 300 AND status = 'R')   
```  
  
## <a name="how-multiple-and-and-or-clauses-are-represented-in-the-criteria-pane"></a>抽出条件ペインでの複数の AND 句および OR 句の表示  
 クエリおよびビュー デザイナーは、検索条件を [抽出条件ペイン](visual-database-tools.md)に表示します。 ただし、AND および OR で結合された複数の句が含まれていると、抽出条件ペインで期待どおりに表示されない場合があります。 また、抽出条件ペインや [ダイアグラム ペイン](diagram-pane-visual-database-tools.md)でクエリを変更すると、SQL ステートメントの入力時の内容も変更される場合があります。  
  
 一般に、AND 句と OR 句が抽出条件ペインでどのように表示されるかは、次の規則に基づいています。  
  
-   AND で結合された条件はすべて、 **[フィルター]** グリッド列または同じ **[または...]** 列に表示されます。  
  
-   OR で結合された条件はすべて、別の **[または...]** 列に表示されます。  
  
-   AND 句と OR 句の組み合わせの論理的結果として AND がいくつかの OR 句に分配される場合、抽出条件ペインでは、AND 句を必要な数だけ繰り返すことによりこれを明確に表します。  
  
 たとえば、SQL ペインで次のような検索条件を作成する場合を考えます。ここで、AND で結合された 2 つの句は OR で結合された 3 つ目の句よりも優先されます。  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  (job_lvl = 100) OR   
  (status = 'R')  
```  
  
 クエリおよびビュー デザイナーは、この WHERE 句を次のように抽出条件ペインに表示します。  
  
 ![抽出条件ペインで OR 句が優先される](../../database-engine/media//vs-criteriapane1.gif "抽出条件ペインで OR 句が優先される")  
  
 ただし、結合されている OR 句が AND 句よりも優先される場合は、各 OR 句に対して AND 句が繰り返されます。 その結果、AND 句が各 OR 句に分配されます。 たとえば、SQL ペインで次のような WHERE 句を作成したとします。  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ( (job_lvl = 100) OR   
  (status = 'R') )  
```  
  
 クエリおよびビュー デザイナーは、この WHERE 句を次のように抽出条件ペインに表示します。  
  
 ![抽出条件ペインの複数の AND 句と OR 句](../../database-engine/media//vs-criteriapane2.gif "抽出条件ペインの複数の AND 句と OR 句")  
  
 結合された OR 句にデータ列が 1 つしか含まれない場合、クエリおよびビュー デザイナーはその OR 句全体をグリッドの 1 つのセルに配置することができるため、AND 句を繰り返さずに済みます。 たとえば、SQL ペインで次のような WHERE 句を作成したとします。  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ((status = 'R') OR (status = 'A'))  
```  
  
 クエリおよびビュー デザイナーは、この WHERE 句を次のように抽出条件ペインに表示します。  
  
 ![抽出条件ペインで定義された、結合された OR 句](../../database-engine/media//vs-criteriapane3.gif "抽出条件ペインで定義された、結合された OR 句")  
  
 抽出条件ペインで値の 1 つを変更するなど、クエリに変更を加えると、クエリおよびビュー デザイナーによって SQL ペインの SQL ステートメントが再作成されます。 再作成された SQL ステートメントは、元のステートメントよりも抽出条件ペインの表示内容の方に近くなります。 たとえば、抽出条件ペインに分配された AND 句が含まれる場合、SQL ペインで再作成されるステートメントには明示的に分配された AND 句が含まれます。 詳細については、このトピックの前の方にある「複数の OR 句に対する AND の解釈」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [検索基準の指定 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
