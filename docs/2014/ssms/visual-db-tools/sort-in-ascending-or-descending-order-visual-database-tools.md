---
title: 昇順または降順の並べ替え (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdf37ab5b61e74ab04b9b58162325b580675c493
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63070782"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>昇順または降順の並べ替え (Visual Database Tools)
  `ASC` 句で `DESC` または `ORDER BY` キーワードを使用すると、結果セットの 1 つ以上の列を基準に、クエリ結果を昇順または降順に並べ替えることができます。  
  
> [!NOTE]  
>  並べ替え順序を決定する要素として列の照合順序があります。 この照合順序は、 [[照合順序] ダイアログ ボックス](visual-database-tools.md)で変更できます。  
  
 次の手順は、ORDER BY 句を使用して 1 つ以上の列を並べ替えるクエリを、クエリおよびビュー デザイナーで開いていると想定しています。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>結果の並べ替え順序を指定または変更するには  
  
1.  [抽出条件ペイン](criteria-pane-visual-database-tools.md)で、並べ替えを行う列の **[並べ替えの種類]** フィールドをクリックします。  
  
2.  **[昇順]** または **[降順]** を選択して、列の並べ替え順序を指定します。  
  
 抽出条件ペインで操作を行うと、最後に行った操作に合わせてクエリの UNION 句が変化します。  
  
> [!NOTE]  
>  複数の列を使用して結果を並べ替えるときは、[並べ替え順序] 列を使用して、列を検索する順序を互いの列を基準にして指定します。 詳細については、「[クエリ内の複数の列の並べ替え (Visual Database Tools)](sort-multiple-columns-in-queries-visual-database-tools.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [クエリ結果の並べ替えとグループ化&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [クエリ結果の要約&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
