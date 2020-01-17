---
title: タスク 9:Union All を追加するレコードと修正のレコードを結合する変換 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489647"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>タスク 9:全体結合変換を追加して適切なレコードと修正済みレコードを結合する
  ここでは、全体結合変換をデータ フローに追加します。 全体結合変換は、複数の入力を 1 つの出力に結合します。 このシナリオでは、1 つのストリームに適切なレコードと修正済みレコードを結合します。  
  
1.  ドラッグ アンド ドロップ**全体結合**から変換**共通**のセクション、 **SSIS ツールボックス**を**データ フロー**タブし、下に配置**レコードと修正のレコードを選択**します。  
  
2.  右クリックして**全体結合**変換を実行、**データ フロー**タブをクリックし、をクリックして**の名前を変更**します。 型**Combine Correct and Corrected Records**、キーを押します**ENTER**します。  
  
     ![結合レコードと修正 Reocrds](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "レコードと修正 Reocrds の結合")  
  
3.  接続**Pick Correct and Corrected Records**に**Combine Correct and Corrected Records**で、**データ フロー**青色コネクタを使用してタブ。 表示する必要があります、**入出力の選択** ダイアログ ボックス。  
  
4.  **入出力**ダイアログ ボックスで、**修正**の**出力** をクリック**OK**。  
  
     ![出力の選択 ダイアログ ボックスの入力](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "出力の選択 ダイアログ ボックスの入力")  
  
5.  というタイトル**修正**ドラッグ アンド ドロップ左へのコネクタの末尾のドットを左にします。  
  
     ![レコードと修正に結合するために正しい接続](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "レコードと修正に結合するための適切な接続")  
  
6.  選択した場合**Pick Correct and Corrected Records**変換、別の青色コネクタを表示する必要があります。 その青色コネクタをドラッグして**Combine Correct and Corrected Records**します。  
  
     ![接続レコードと修正に結合するための修正された](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "レコードと修正に結合するための修正された接続")  
  
7.  これは、**コネクタ**というが**Corrected**します。 2 つの条件があるため**修正**と**修正済み**、し、1 つの条件が既に使用されて、**入出力の選択** ダイアログ ボックスではこの時間は表示されません。 コネクタが重複する場合は、左側のコネクタを右側のコネクタに、または右側のコネクタを左側のコネクタにドラッグ アンド ドロップします。  
  
## <a name="next-step"></a>次の手順  
 [タスク 10:重複を識別するために、あいまいグループ化変換を追加します。](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
