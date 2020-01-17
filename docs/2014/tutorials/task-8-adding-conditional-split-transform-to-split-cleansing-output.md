---
title: タスク 8:クレンジングの出力を分割する変換を分割する条件を追加する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489672"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>タスク 8:条件分割変換を追加してクレンジング出力を分割する
  この変換では、データ フローに条件分割変換を追加します。 条件分割変換では、データの内容に応じて別の出力に行をルートできます。 このチュートリアルでは、使用して、**レコードの状態**DQS クレンジング変換からの出力列です。 このチュートリアルでは、適切なレコードまたは修正されたレコードのみを MDS サーバーにアップロードします。 場合を確認するため、**レコードの状態**は**修正**または**Corrected**とレコードを MDS にアップロードする前に、レコードを結合します。  
  
1.  ドラッグ アンド ドロップ**条件分割変換**から**共通**セクション、 **SSIS ツールボックス**を**データ フロー** ] タブの [ **仕入先データ クレンジング**します。  
  
2.  右クリックして**条件分割**、 をクリック**の名前を変更**します。 型**Pick Correct and Corrected Records**キーを押します**ENTER**します。  
  
3.  接続**Cleanse Supplier Data**と**Pick Correct and Corrected Records**青色コネクタを使用します。  
  
     ![Cleanse Supplier Data に正しいと修正済みの選択](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Cleanse Supplier データが正しいと修正済みの選択")  
  
4.  ダブルクリック**Pick Correct and Corrected Records**で、**データ フロー**タブ。  
  
5.  変更、**既定の出力名**画面の下部にある**修正**します。  
  
6.  展開**列**で、**左上ペイン**します。  
  
     ![条件分割変換エディター](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "条件分割変換エディター")  
  
7.  ドラッグ アンド ドロップ**レコードの状態**を**条件**列。  
  
8.  型 **「修正済み」= =** 横に **[レコードの状態]** の**条件**列。  
  
9. クリックして**ケース 1**で、**出力名 列**、名を変更して、**修正済み**します。  
  
10. クリックして**OK**を閉じる、**条件分割変換エディター**  ダイアログ ボックス。  
  
## <a name="next-step"></a>次の手順  
 [タスク 9:結合を追加してレコードと修正のレコードを結合するすべての変換](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
