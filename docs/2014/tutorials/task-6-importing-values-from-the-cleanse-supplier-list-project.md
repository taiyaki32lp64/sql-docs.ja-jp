---
title: タスク 6:値をインポート、Cleanse Supplier List プロジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f6b90a36238cd4a02e86d49125ee662f07d32882
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489095"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>タスク 6:Cleanse Supplier List プロジェクトから値をインポートする
  ここでは、クレンジング プロセスで収集したデータ品質ナレッジをインポートします。 参照してください[クレンジング プロジェクトの値をドメインにインポート](https://msdn.microsoft.com/library/hh479581.aspx)詳細についてはトピック。 エクスポートすることも、ナレッジ ベースを DQS ファイルに、更新を発行する前に**Suppliers**ナレッジ ベース。  
  
1.  メイン ページで**DQS クライアント**、] をクリックして**右矢印**横に**Suppliers** [**最近使用したナレッジ ベース**をクリックします **。ドメイン管理**します。  
  
2.  クリックして**Contact Email**に切り替えると、ドメインの一覧で、**ドメイン値**右ペインでタブ。  
  
3.  クリックして**下向きの矢印**横に、**値のインポート**アイコンをクリックし、ツールバー**プロジェクト値のインポート**します。  
  
     ![プロジェクトのインポートがツール バー ボタンを値](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "プロジェクト値のツール バー ボタンのインポート")  
  
4.  **プロジェクト値のインポート**ダイアログ ボックスで、 **Cleanse Supplier List**プロジェクト、およびクリックして **[ok]** します。  
  
5.  すべての電子メールが、インタラクティブなクレンジングで行った 2 つの修正と共にインポートされることに注意してください。 スクロールして 2 つの修正を確認します。  
  
    |値|次に修正|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  プロジェクト値のインポートの前の手順を繰り返して、**国**ドメインおよび修正するための新しいエントリが追加されたことに注意してください**United State**に**米国**(で '%s ')。  
  
    |値|次に修正|  
    |-----------|----------------|  
    |United State|米国|  
  
7.  古いドメイン値を表示するには、オフ**新規のみ表示**チェック ボックスをオンします。  
  
8.  プロジェクト値のインポートの前の手順を繰り返して、 **Supplier Name**ドメイン。 インポート後は、既定で新しい値だけが表示されます。 すべての値を表示するには、オフ**新規のみ表示**チェック ボックスをオンします。 情報を追加した、 **Suppliers**クレンジングのアクティビティから学習した内容をナレッジ ベース。 ナレッジ ベースが充実するほど、クレンジング結果が向上します。  
  
    > [!NOTE]  
    >  複合ドメインの値をインポートすることはできません。  
  
9. クリックして**ナレッジ ベースのエクスポート**アイコンをクリックし、ツールバーで**ナレッジ ベースのエクスポート**します。  
  
     ![ナレッジ ベース メニューのエクスポート](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg " メニューのサポート技術情報のエクスポート")  
  
10. 型、Tutorial フォルダーに移動**Suppliers.dqs**の**ファイル名**、 をクリック**保存**します。 この DQS ファイルを使用して、これに基づく新しいナレッジ ベースを作成できます。  
  
11. をクリックして**OK**を閉じる、**ナレッジ ベースのエクスポート - サプライヤー**メッセージ ボックス。  
  
12. クリックして**完了**してアクティビティを終了します。  
  
13. **[パブリッシュ]** をクリックします。  
  
14. クリックして**OK**メッセージ ボックス。  
  
## <a name="next-step"></a>次の手順  
 [レッスン 3:削除するデータを照合して仕入先の一覧から重複します。](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
