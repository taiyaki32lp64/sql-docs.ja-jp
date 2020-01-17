---
title: タスク 2:Excel 用 MDS アドインを使用して MDS に仕入先データのアップロード |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 57a5044ccee040ef1eba95925c689f48739c259f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484660"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>タスク 2:Excel 用 MDS アドインを使用して仕入先データを MDS にアップロードする
  このタスクで、クレンジングされた仕入先データを発行する**MDS**を使用して、 **MDS アドインの Excel**します。 という名前のエンティティを作成する**Supplier**で、 **Suppliers**前のレッスンで作成したモデル。 エンティティは、Excel ファイルの各列に属性を持ちます。 Supplier エンティティの Code および Name 属性に対応して、 **SupplierID**と**Supplier Name** Excel の列。  
  
1.  開いている**クレンジングおよび照合 Suppliers.xls**で**Excel**します。  
  
2.  キーを押して**CTRL + A**全体のデータを選択します。 **重要**スプレッドシートのデータ全体を選択します。  
  
3.  クリックして**マスター データ**メニュー バーでします。  
  
4.  クリックして**エンティティの作成**リボンのボタンをクリックします。  
  
     ![Excel - [マスター データ] タブ - エンティティ ボタンを作成する](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - [マスター データ] タブ - エンティティ ボタンを作成します。")  
  
5.  **接続の管理**] ダイアログ ボックスへの接続が表示されない場合**ローカル MDS サーバー** [**既存の接続**次の操作を行います。  
  
    1.  選択**新しい接続を作成**、 をクリック**新規**ボタンをクリックします。  
  
    2.  **新しい接続の追加**ダイアログ ボックスに「**ローカル MDS サーバー**の**説明**と **http://localhost/MDS** の**MDS サーバー アドレス**、 をクリック**OK**ダイアログ ボックスを閉じます。  
  
6.  **接続の管理**ダイアログ ボックスで、**ローカル MDS サーバー** (http://localhost/MDS) 、 をクリックして**テスト**接続をテストします。 クリックして**OK**メッセージ ボックス。  
  
7.  クリックして**Connect** MDS サーバーに接続します。  
  
8.  **エンティティの作成**ダイアログ ボックスで、 **Suppliers**の**モデル**します。  
  
9. いることを確認**VERSION_1**が選択されている**バージョン**します。  
  
10. 入力**Supplier**の**新しいエンティティ名**します。  
  
11. 選択**SupplierID**の**一意の識別子を含む列**フィールド (してもコードを自動的に生成できます)。 本質的にマップする、 **SupplierID**列**Excel**を**コード**属性の**Supplier**エンティティ。  
  
12. 選択**Supplier Name**の**名前を含む列**フィールド。 本質的にマップする、 **Supplier Name**列**Excel**を**名前**の属性、**サプライヤー**エンティティ。 **コード**と**名前**属性は、MDS のエンティティの必須属性。  
  
     ![エンティティのダイアログ ボックスを作成する](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "エンティティ ダイアログ ボックスの作成")  
  
13. クリックして**OK**を MDS にエンティティを作成するエンティティにマスター データを発行して閉じます**エンティティの作成** ダイアログ ボックス。  
  
14. これで、タイトルの新しいシートを表示する必要があります**Supplier**、これは、Excel スプレッドシートに追加するエンティティの名前と、ワークシートの上部にあるワークシートが MDS サーバーに接続されていることを確認する必要があります。 注意して元のワークシート (「 **Sheet1**) がまだ存在します。  
  
     ![Excel に仕入先と Sheet1 タブ](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel に仕入先と Sheet1 タブ")  
  
     ![Excel - MDS 接続の詳細を示す](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - MDS 接続の詳細を表示")  
  
15. 保持**Excel**を開きます。  
  
## <a name="next-task"></a>次の作業  
 [タスク 3: マスター データ マネージャーでデータを検証します。](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
