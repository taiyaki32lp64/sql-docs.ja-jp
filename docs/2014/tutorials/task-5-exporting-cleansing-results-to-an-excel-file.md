---
title: タスク 5:クレンジングの結果を Excel ファイルにエクスポートする |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489126"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>タスク 5:Excel ファイルにクレンジングの結果をエクスポートする
  ここでは、クレンジング アクティビティから Excel ファイルに結果をエクスポートします。 参照してください[エクスポート ステージ](https://msdn.microsoft.com/library/hh213061.aspx#Export)詳細についてはトピック。  
  
1.  右側のウィンドウで次のように選択します。 **Excel**の、**変換先の型**します。  
  
2.  をクリックして**参照**、として出力ファイル名を指定**Cleansed Supplier List.xls**、順にクリックします**オープン**します。  
  
3.  選択**データのみ**の**出力**クレンジングされたデータのみをエクスポートする形式。 2 番目のオプションでは、**データとクレンジング情報**、クレンジングされたデータと共にクレンジング アクティビティの詳細をエクスポートすることができます。 **標準化形式**オプションを使用して、そのドメインの値のドメインで定義する出力形式を適用できます。 チュートリアルのドメインには、出力形式を定義していません。  
  
     ![エクスポートのクレンジング結果ページ](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "エクスポート クレンジングの結果 ページ")  
  
4.  クリックして**エクスポート**にデータをエクスポートします。 クリックしてしないでください**完了**まだします。  
  
5.  クリックして**閉じる**上、**エクスポート** ダイアログ ボックス。  
  
6.  クリックして**完了**してアクティビティを終了します。 クリックする前に結果をエクスポートすることを忘れた場合**完了**、 をクリックして**データ品質プロジェクトを開く**のメイン ページで**DQS クライアント**を選択します**Cleanse Supplierリスト**プロジェクト、およびクリックの一覧から**次**を取得するには、画面の下部にある、**エクスポート**クレンジング プロセスをもう一度のステージ。 切り替えることもできます**管理し、結果を表示する** タブをクリックして**戻る**ボタンをクリックします。  
  
7.  開く、 **Cleansed Supplier List.xls**次の操作を行います。  
  
    1.  Adventure-work.com で終わる電子メール アドレスがないことを確認します (文字のない ')、ワークシートで adventure-work.com を検索しています。  
  
    2.  あることを確認しない**USA**値、**国**列。  
  
    3.  検索**Los Angeles**ことを確認し、**状態**に設定されている**CA**します。  
  
    4.  条件がないことを確認します。 **co.** 、 **Corp.** 、と**Inc.** します。  
  
    5.  削除、 **Address Validation**列、スプレッドシートから、excel ファイルを保存します。 この追加列は Address Validation 複合ドメインに対応します。  
  
## <a name="next-step"></a>次の手順  
 [タスク 6:値をインポート、Cleanse Supplier List プロジェクト](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
