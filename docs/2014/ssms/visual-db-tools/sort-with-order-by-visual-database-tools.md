---
title: ORDER BY 句での並べ替え (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30a2fca3dd0f2fcc6f22f2330c37fb8e333d9994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049161"
---
# <a name="sort-with-order-by-visual-database-tools"></a>ORDER BY 句での並べ替え (Visual Database Tools)
  ORDER BY 句を使用すると、返される行内のクエリの結果を、1 つまたは複数の列を使用して並べ替えることができます。 ORDER BY 句は、抽出条件ペインでオプションを選択することによって定義できます。  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>ORDER BY 句を使用してクエリを並べ替えるには  
  
1.  クエリを開くか、新規作成します。  
  
2.  [抽出条件ペイン](visual-database-tools.md)で、クエリ結果の並べ替えに使用する列に対応する行の **[並べ替えの種類]** 列をクリックします。  
  
3.  ドロップダウン リストから、 *[昇順]* または *[降順]* を選択します。  
  
> [!NOTE]  
>  列の **[並べ替えの種類]** のエントリを削除すると、その列が ORDER BY 句から削除されます。  
  
 抽出条件ペインで操作を行うと、最後に行った操作に合わせてクエリの UNION 句が変化します。  
  
> [!NOTE]  
>  複数の列を使用して結果を並べ替えるときは、 **[並べ替え順序]** 列を使用して、列を検索する順序を互いの列を基準にして指定します。 詳細については、「**方法 :クエリ内の複数の列の並べ替え**に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [クエリ結果の並べ替えとグループ化&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [クエリ結果の要約&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
