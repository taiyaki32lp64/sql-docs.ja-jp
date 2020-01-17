---
title: 重複する行の除外 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63ec11b8575017ffbb3a1b1468ef3150a20326e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028353"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>重複する行の除外 (Visual Database Tools)
  結果セットに一意の値だけが必要な場合は、結果セットからの重複の削除を指定できます。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>結果セットから重複行を削除するには  
  
1.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[プロパティ]** を選択します。  
  
2.  プロパティ ウィンドウの **[一意の値]** をクリックし、値を **[はい]** に設定します。  
  
     SQL ステートメントの表示列の一覧の前にキーワード DISTINCT が挿入されます。  
  
    > [!NOTE]  
    >  DISTINCT キーワードを使用する場合、結果ペインで結果セットを変更できない場合があります。  
  
## <a name="see-also"></a>参照  
 [検索条件を指定&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
  
