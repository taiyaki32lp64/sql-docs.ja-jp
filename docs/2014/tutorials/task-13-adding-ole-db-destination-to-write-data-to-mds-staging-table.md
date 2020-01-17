---
title: タスク 13:MDS ステージング テーブルにデータを書き込む OLE DB 変換先の追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7c5fc9d863c23c1cae08c04fef7810aeda446762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65476992"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>タスク 13:データを書き込む OLE DB 変換先を MDS ステージング テーブルに追加する
  これで、追加した**ImportType**と**BatchTag**を経由して送信を MDS ステージング用に準備ができたら、すべてのレコード値。 このタスクでデータを書き込む OLE DB Destination を使用する**stg.supplier_Leaf**ステージング テーブル。  
  
1.  ドラッグ**OLE DB 変換先**から**その他の変換先**セクション、 **SSIS ツールボックス**を**データ フロー**タブし、下にドロップします**MDS で必要な列を追加**します。  
  
2.  右クリックして**OLE DB 変換先**で、**データ フロー**タブをクリックし、をクリックして**の名前を変更**します。 型**MDS ステージング テーブルにサプライヤー データを書き込む**キーを押します**ENTER**します。  
  
3.  接続、 **Add Columns Required by MDS**に**MDS ステージング テーブルにサプライヤー データを書き込む**青色コネクタを使用します。  
  
4.  ダブルクリック**MDS ステージング テーブルにサプライヤー データを書き込む**で、**データ フロー**タブ。  
  
5.  **OLE DB 変換先エディター**  ダイアログ ボックスに、必ず **(ローカル)。MDS** (または**localhost です。MDS**) が選択されている、 **OLE DB 接続マネージャー**フィールド。  
  
6.  選択**stg.Supplier_Leaf**の一覧からテーブル **、テーブルまたはビューの名前**します。  
  
     ![OLEDB 変換先エディター](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 変換先エディター")  
  
7.  切り替えて、**マッピング**をクリックしてページ**マッピング**左側のメニュー上。  
  
8.  マップ**入力**と**先**列では、次の表に示すようにします。  
  
     ![OLEDB 変換先エディター - マッピング](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 変換先エディター - マッピング")  
  
9. 使用していることを確認します。 **(_o)** 列、入力列のない、 **_Status**または **_Source**列。 **_Output** DQS クレンジングの出力値を含む列。  
  
10. クリックして**OK**を閉じる、 **OLE DB 変換先エディター**  ダイアログ ボックス。  
  
11. データ フローは次の図のようになります。  
  
     ![データ フローを完了した](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "データ フローの完了")  
  
## <a name="next-step"></a>次の手順  
 [タスク 14:実行 SQL タスクは、MDS のストアド プロシージャを実行する制御フローを追加](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
