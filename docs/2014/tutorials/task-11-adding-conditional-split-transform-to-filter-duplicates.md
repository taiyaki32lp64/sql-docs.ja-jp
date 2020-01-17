---
title: タスク 11:重複をフィルター処理する変換を分割する条件を追加する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65476752"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>タスク 11:条件分割変換を追加して重複をフィルターする
  ここでは、データ フローに条件分割変換を追加します。 この変換は、受信するレコード セットから重複をフィルターする際に役立ちます。 あいまいグループ化変換では、一致として検出したレコードがグループ化され、ピボット レコードとしてレコードのいずれかが選択されます。 グループ内のすべてのレコードは、同じ _key_out 値を持ちます。 グループ内のピボット レコードは _key_out 値と同じ _key_in 値を持ちます。 グループ内のその他のレコードでは、_key_in と _key_out の値が異なります。 そのため、条件の _key_in==_key_out を使用してフィルターすると、グループ内のピボット行のみが取得されます。  
  
1.  ドラッグ アンド ドロップ**条件分割**から変換**共通**セクション、 **SSIS ツールボックス**を**データ フロー**タブ。  
  
2.  右クリックして**条件分割変換**で、**データ フロー**タブをクリックし、をクリックして**の名前を変更**します。 型**Filter Duplicates**キーを押します**ENTER**します。  
  
3.  接続**グループの Id と一致するサプライヤー**に**重複をフィルター**します。  
  
4.  ダブルクリック**Filter Duplicates**を起動する、**条件分割変換エディター**  ダイアログ ボックス。  
  
5.  展開**列**左ペインでします。  
  
6.  ドラッグ アンド ドロップ **_key_in**を**条件**列。  
  
7.  型 (等しい) を横に = = **_key_in**ドラッグ アンド ドロップ **_key_out**します。  
  
8.  クリックして**ケース 1**で、**出力名**列に「**一意のレコード**、キーを押します **」と入力**します。  
  
     ![条件分割変換エディター](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "条件分割変換エディター")  
  
9. クリックして**OK**を閉じる、**条件分割変換エディター**  ダイアログ ボックス。  
  
## <a name="next-step"></a>次の手順  
 [タスク 12:派生列変換を MDS で必要な列を追加するには](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
