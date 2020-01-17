---
title: ORDER BY 句での並べ替え (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7d14acc5485bb3037f769784ee4daf012a5944e2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263596"
---
# <a name="sort-with-order-by-visual-database-tools"></a>ORDER BY 句での並べ替え (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
ORDER BY 句を使用すると、返される行内のクエリの結果を、1 つまたは複数の列を使用して並べ替えることができます。 ORDER BY 句は、抽出条件ペインでオプションを選択することによって定義できます。  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>ORDER BY 句を使用してクエリを並べ替えるには  
  
1.  クエリを開くか、新規作成します。  
  
2.  [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)で、クエリ結果の並べ替えに使用する列に対応する行の **[並べ替えの種類]** 列をクリックします。  
  
3.  ドロップダウン リストから、 *[昇順]* または *[降順]* を選択します。  
  
> [!NOTE]  
> 列の **[並べ替えの種類]** のエントリを削除すると、その列が ORDER BY 句から削除されます。  
  
抽出条件ペインで操作を行うと、最後に行った操作に合わせてクエリの UNION 句が変化します。  
  
> [!NOTE]  
> 複数の列を使用して結果を並べ替えるときは、 **[並べ替え順序]** 列を使用して、列を検索する順序を互いの列を基準にして指定します。 詳細については、「**ソフト NUMA を使用するようにクエリ内の複数の列の並べ替え**に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
