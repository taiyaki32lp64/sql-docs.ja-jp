---
title: 値の一致しない行を選択する方法 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b664c5a99e362ca09096e745cb1fae49799ef81e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266869"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>値の一致しない行を選択する方法 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
値の一致しない行を検索するには、NOT 演算子を使用します。  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>値の一致しない行を検索するには  
  
1.  検索条件で使用する列または式を追加していない場合は、列または式を [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)に追加します。  
  
2.  検索するデータ列または式を含む行を見つけ、 **[フィルター]** グリッド列に NOT 演算子とそれに続く検索値を入力します。  
  
たとえば、 `products` テーブルから、製品コード列の値が "A" 以外の文字で始まるすべての行を検索するには、検索条件を次のようにします。  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>参照  
[検索値を入力するときの規則 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
