---
title: タスク 2:テストと一致するポリシーを公開 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a9957625e09bde8bb733eca6e564dfdcfbb0bd98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484737"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>タスク 2:照合ポリシーをテストおよびパブリッシュする
  このタスクでは、テスト、発行、 **Remove Duplicate Suppliers**照合ポリシー。  
  
1.  **照合結果**] ページで [**開始**全体のポリシーをテストします。 この場合は、ポリシーに存在するルールが 1 つだけであるため、ルールとポリシーのテスト結果が同じになります。  
  
2.  リスト ボックスのすべての一致レコードと照合スコアを確認します。 持つレコードを**緑**関連付けられているアイコンはその前にあるピボット レコードと重複しています。 いくつかの例を次に示します。  
  
    1.  レコードを**レコード ID:1000005**のレコードを一致**レコード Id:1000004**で**スコア。100%** 、両方のレコードの同じ値があるため、 **SupplierID (前提条件)** 、 **Supplier Name**、および**ContactEmailAddress 列**します。 DQS はクラスターのピボット レコードとしてレコードをランダムに選択します。  
  
    2.  レコード**1000023**一致するレコードの**1000022**と照合スコア。93% であるため、2 つのレコードが同じ値を持つこと**SupplierID (前提条件)** と**Supplier Name** 、列の値が異なる、 **ContactEmailAddress**列です。  
  
    3.  2 つのレコードとレコード Id を表示するリストの一番下までスクロールします。**1000051**と**1000052**します。 レコード**1000052**照合スコアとの一致と見なされます**91%** 2 つのレコードの同じ値があるため、 **SupplierID**と**ContactEmailAddress** 、列の値が異なる、 **Supplier Name**列。  
  
     ![ポリシー定義 - ポリシーの結果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "ポリシー定義 - ポリシーの結果")  
  
3.  任意の一致するレコード (緑色のアイコン) を右クリックし、をクリックして**詳細を表示する**各フィールドのスコアを照合スコア全体に与える影響などの照合に関する詳細情報を確認します。  
  
     ![照合スコアの詳細 ダイアログ ボックス](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "照合スコアの詳細 ダイアログ ボックス")  
  
4.  クリックして**閉じます**を閉じる、**照合スコアの詳細** ダイアログ ボックス。  
  
5.  クリックして**照合結果**ページの下部にあるタブ。 このタブには、一致レコードの数、不一致レコードの数、一致レコードを持つクラスターの数、平均クラスター サイズ、最小クラスター サイズ、最大クラスター サイズなどの詳細が示されます。 参照してください[照合ポリシーの作成](https://msdn.microsoft.com/library/hh270290.aspx)の詳細。 このアクティビティの結果をエクスポートすることはできません。 サンプル データに対してルールおよびポリシーをテストするためにサンプル データを使用することで、照合ポリシーを定義するだけです。  
  
     ![[結果] タブに一致する](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "照合結果 タブ")  
  
6.  をクリックして**完了**照合ポリシーの作成を完了します。  
  
    > [!NOTE]  
    >  ここでは、照合ポリシーを定義しました。したがって、結果を出力ファイルにエクスポートすることはできません。 基本的には、ポリシーを定義する目的でサンプル入力ファイルを使用し、ルールを作成し、サンプル データに対してルールおよびポリシーをテストしました。  
  
7.  SQL Server Data Quality Services ダイアログ ボックスで、**発行** をクリック**OK**メッセージ ボックス。 定義した照合ポリシーを公開するようになりました、 **Suppliers**ナレッジ ベース。 このナレッジ ベースを使用して、入力ファイルに対して照合プロセスを実行し、重複を特定および削除できます。  
  
## <a name="next-step"></a>次の手順  
 [タスク 3: 作成と一致するデータ品質プロジェクトを実行](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
