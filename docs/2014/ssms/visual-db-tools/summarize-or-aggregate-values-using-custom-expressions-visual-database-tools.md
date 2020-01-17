---
title: 要約またはカスタム式 (Visual Database Tools) を使用して値を集計する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b679eac51bf6fd51d10a88816017f2b767a69041
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204642"
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>カスタム式を使用して値を要約または集計する (Visual Database Tools)
  集計関数を使用してデータを集計するだけでなく、カスタム式を作成して集計値を求めることもできます。 カスタム式は、集計クエリのどこでも集計関数の代わりに使用できます。  
  
 たとえば、 `titles` テーブルでは、平均価格を表示するだけでなく、値下げした場合の平均価格を表示するクエリも作成できます。  
  
 テーブルの一部の行だけに関連する計算を式で使用することはできません。式の計算時には集計値だけを使用できるため、集計値に基づく式を指定する必要があります。  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>集計値にカスタム式を指定するには  
  
1.  検索するグループを指定します。 詳しくは、「[クエリ結果内の行のグループ化 (Visual Database Tools)](visual-database-tools.md)」をご覧ください。  
  
2.  抽出条件ペインの空白行に移動し、**[列]** 列に式を入力します。  
  
     クエリ出力にわかりやすい列ヘッダーを作成できるように、[クエリおよびビュー デザイナー](query-and-view-designer-tools-visual-database-tools.md)により、式に列の別名が自動的に割り当てられます。 詳細については、「[列の別名の作成 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)」を参照してください。  
  
3.  式の **[グループ化]** 列で、**[式]** をクリックします。  
  
4.  クエリを実行します。  
  
## <a name="see-also"></a>参照  
 [クエリ結果の並べ替えとグループ化&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [クエリ結果の要約 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)  
  
  
