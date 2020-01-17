---
title: タスク 10:重複を識別するために、あいまいグループ化変換の追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 48e233c6f2c7a55bf2420825b9fb3064db6e89e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481250"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>タスク 10:あいまいグループ化変換を追加して重複を識別する
  ここでは、あいまいグループ化変換をデータ フローに追加します。 あいまいグループ化変換は、変換元データの重複を識別する際に役立ちます。 参照してください[Fuzzy Grouping Transformation](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)の詳細。  
  
1.  ドラッグ アンド ドロップ**あいまいグループ化**変換**その他の変換**上、 **SSIS ツールボックス**を**データ フロー**タブ**正しいと修正済みレコードを結合**します。  
  
2.  右クリックして**あいまいグループ化**変換を実行、**データ フロー**タブをクリックし、をクリックして**の名前を変更**します。 型**Id と一致するグループ仕入先**キーを押します**ENTER**します。  
  
3.  接続**Combine Correct and Corrected Records**に**Id と一致するグループ仕入先**青色コネクタを使用します。  
  
     ![Id と一致するグループ仕入先への接続を](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Id と一致するグループ仕入先への接続")  
  
4.  ダブルクリック**Id と一致するグループ仕入先**します。  
  
5.  **あいまいグループ化変換エディター**、 をクリックして**新規**横に**OLE DB 接続マネージャーの一覧から**を起動する**OLE DB 接続の構成Manager**  ダイアログ ボックス。  
  
6.  ダイアログ ボックスで、次のようにクリックします。**新規**を起動する**接続マネージャー**  ダイアログ ボックス。  
  
7.  型 **(local)** または**期間**(.) のサーバー名。  
  
8.  選択**MDS**の**を選択するか、データベース名を入力**フィールド。 MDS データベースの一時的なストレージとして使用する、**あいまいグループ化変換**します。 **あいまいグループ化**変換、変換アルゴリズムがその作業を行う必要がある一時テーブルを SQL Server を作成する SQL Server のインスタンスへの接続が必要です。 これを行うには、データベースを作成するか、別の既存のデータベースを使用します。  
  
9. をクリックして**接続のテスト**接続をテストし、をクリックする**OK**メッセージ ボックス。  
  
10. **接続マネージャー**ダイアログ ボックスで、をクリックして**OK**します。  
  
11. 選択 **(ローカル)。MDS** (または**localhost です。MDS**) から、**データ接続の一覧**クリック**OK**。  
  
12. **あいまいグループ化変換エディター**、ことを確認します **(ローカル)。MDS**または**localhost です。MDS**が選択されている、 **OLE DB 接続マネージャー**します。  
  
13. 切り替えて、**列**タブ。  
  
14. 選択 (チェック ボックス) **SupplierID_Output**の一覧から**使用できる入力列**します。 変換を構成するには、重複部分を識別する際に使用する入力列を選択します。 わかりやすくするために、この手順では SupplierID のみを使用します。  
  
     ![あいまいグループ化変換エディター](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "あいまいグループ化変換エディター")  
  
15. をクリックして**OK**を閉じる、**あいまいグループ化変換エディター**します。  
  
## <a name="next-step"></a>次の手順  
 [タスク 11:フィルターに条件分割変換を追加して重複. します。](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
