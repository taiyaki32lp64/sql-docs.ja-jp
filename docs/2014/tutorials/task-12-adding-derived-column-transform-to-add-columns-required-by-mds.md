---
title: タスク 12:派生列変換を MDS で必要な列を追加する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18789f5bc1d97e1531588d50e2430829f95912b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65485239"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>タスク 12:派生列変換を追加して MDS で必要な列を追加する
  ここでは、派生列変換をデータ フローに追加します。 2 つの派生列を追加する**ImportType**と**BatchTag**レコードは、この変換に渡されます。 MDS のステージング テーブルにデータをアップロードする前に、これらの列を追加する必要があります。 これら 2 つは、MDS のステージング テーブルに必要な列です。 参照してください[リーフ メンバー ステージング テーブル](../master-data-services/leaf-member-staging-table-master-data-services.md)の詳細。  
  
1.  ドラッグ アンド ドロップ**派生列変換**から**共通**セクション、 **SSIS ツールボックス**を**データ フロー**タブ。  
  
2.  右クリックして**派生列**変換を実行、**データ フロー**タブをクリックし、をクリックして**の名前を変更**します。 型**Add Columns Required by MDS**キーを押します**ENTER**します。  
  
3.  接続**Filter Duplicates**に**Add Columns Required by MDS**青色コネクタを使用します。 表示する必要があります、**入出力の選択** ダイアログ ボックス。  
  
4.  **入出力の選択**ダイアログ ボックスで、**一意のレコード**、 をクリック**OK**します。  
  
     ![出力の選択 ダイアログ ボックスの入力](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "出力の選択 ダイアログ ボックスの入力")  
  
5.  クリックして**SSIS**をクリックし、メニュー バー**変数**します。  
  
6.  **変数**ウィンドウで、をクリックして**変数の追加**ツールバーのボタンをクリックします。  
  
     ![SSIS 変数 ウィンドウ](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 変数 ウィンドウ")  
  
7.  型**ImportType**の**名前**と**2**の**値**します。 MDS のエンティティに新しいメンバーを追加するため、値には 2 を指定します。 詳細については、このパラメーターは、次を参照してください。[リーフ メンバー ステージング テーブル](../master-data-services/leaf-member-staging-table-master-data-services.md)します。  
  
8.  クリックして**変数の追加**ツール バー ボタンをもう一度です。  
  
9. 型**BatchTag**の**名前**を選択します**文字列**の**データ型**、および**EIMBatch**用、**値**します。 **BatchTag**を MDS に送信されるバッチの一意名です。  
  
10. **データ フロー**  タブで、ダブルクリックして**Add Columns Required by MDS**します。  
  
11. **派生列変換エディター**  ダイアログ ボックスで、**下部のペインで、リスト ボックス**、型**ImportType**の**派生列名**.  
  
12. 展開**変数とパラメーター** 、左ペインにドラッグ アンド ドロップ**user::importtype**を**式**列。  
  
     ![派生列変換エディター](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "派生列変換エディター")  
  
13. 型**BatchTag**の次の行で、**派生列名**します。  
  
14. ドラッグ アンド ドロップ**user::batchtag**から**変数とパラメーター**を**式**列。  
  
15. クリックして**OK**を閉じる、**派生列変換** ダイアログ ボックス。  
  
## <a name="next-step"></a>次の手順  
 [タスク 13:MDS ステージング テーブルにデータを書き込む OLE DB 変換先を追加します。](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
