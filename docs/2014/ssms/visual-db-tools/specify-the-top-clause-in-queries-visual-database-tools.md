---
title: クエリでの TOP 句の指定 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f9587a5e653d2df8cbe169fe5030542b86d8aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194964"
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>クエリでの TOP 句の指定 (Visual Database Tools)
  TOP 句は、クエリから最初の *n* 行または *n %* 行だけを返します。 TOP 句は、すべてのクエリ結果を返すために必要なリソースを使用する前に、結果の一部を検査して、必要なクエリが実行されるかどうかを確認する場合に便利です。  
  
### <a name="to-specify-the-top-clause-in-queries"></a>クエリで TOP 句を指定するには  
  
1.  ソリューション エクスプローラーでクエリを開くか、新しいクエリを作成します。  
  
2.  **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。  
  
3.  **[プロパティ ウィンドウ]** で、 **[Top の指定]** プロパティを検索して展開します。  
  
4.  **[(Top)]** 子プロパティをクリックして、 **[はい]** に設定します。  
  
5.  **[式]** 子プロパティで、数値の結果を返す式を入力します ("10"、"2*5" など)。  
  
6.  **[PERCENT]** 子プロパティをクリックして、 **[式]** プロパティを、返されるすべての行のパーセントとして処理するか (はい)、返される行の絶対数として処理するか (いいえ) を指定します。  
  
7.  クエリで ORDER BY 句が使用される場合は、 **[WITH TIES 使用]** 子プロパティをクリックして、グループの一部だけが含まれる場合にグループ内のすべての行を表示するときは **[はい]** 、行を切り捨てるときは **[いいえ]** を選択します。  
  
 上記の手順を実行していくと、TOP 句が SQL ペインに表示され、プロパティの現在の設定を反映するように変更されます。  
  
> [!NOTE]  
>  SQL ペインで TOP 句を編集することで、 **[Top の指定]** の子プロパティの値を変更することもできます。  
  
## <a name="see-also"></a>関連項目  
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [クエリのプロパティ (Visual Database Tools)](query-properties-visual-database-tools.md)  
  
  
