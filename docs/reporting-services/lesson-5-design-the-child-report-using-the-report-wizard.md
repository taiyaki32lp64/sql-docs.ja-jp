---
title: 'レッスン 5: レポート ウィザードを使用して子レポートを設計する | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: da9f07cf60a2ec42e23416b52cbfebab78802247
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512646"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>レッスン 5: レポート ウィザードを使用して子レポートを設計する
子レポートのデータ接続とデータ テーブルを作成した後は、レポート デザイナーのレポート ウィザードを使用して子レポートを設計します。 レポート デザイナーの詳細については、「[レポート デザイナーを使用してレポートをデザインする &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)」を参照してください。  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>レポート ウィザードを使用して子レポートを設計するには  
  
1.  **ソリューション エクスプローラー**でトップレベル Web サイトが選択されていることを確認します。  
  
2.  Web サイトを右クリックし、 **[新しい項目の追加]** を選択します。  
  
3.  **[新しい項目の追加]** ダイアログ ボックスで、 **[レポート ウィザード]** をクリックします。レポート ファイルの名前を入力し、 **[追加]** を選択します。  
  
    これにより、レポート ウィザードが起動します。  
  
4.  **[データセットのプロパティ]** ページで、 **[データ ソース]** ボックスの **[DataSet2]** を選択します。  
  
    作成した DataTable で **[使用できるデータセット]** ボックスが自動的に更新されます。  
  
5.  **[次へ]** を選択します。  
  
6.  **[フィールドの配置]** ページで、次の操作を行います。  
  
    1.  **[ProductID]** 、 **[PurchaseOrderID]** 、 **[PurchaseOrderDetailID]** 、 **[OrderQty]** 、 **[ReceivedQty]** 、 **[RejectedQty]** 、および **[StockedQty]** を、 **[使用できるフィールド]** から **[値]** ボックスにドラッグします。  
  
    2.  **[Sum(ProductID)]** 、 **[Sum(PurchaseOrderID)]** 、 **[Sum(PurchaseOrderDetailID)]** 、 **[Sum(OrderQty)]** 、 **[Sum(ReceivedQty)]** 、 **[Sum(RejectedQty)]** 、および **[Sum(StockedQty)]** の横の矢印を選択して、 **[Sum]** の選択を解除します。  
  
7.  **[次へ]** を 2 回選択し、 **[完了]** を選択して **レポート ウィザード**を閉じます。  
  
    これで .rdlc ファイルが作成されました。 このファイルはレポート デザイナーで開くことができます。 設計した Tablix がデザイン画面に表示されます。  
  
8.  .rdlc ファイルが開かれた状態で、次の手順を実行してパラメーターを追加します。  
  
    1.  **レポート データ** ペインの **[パラメーター]** を右クリックし、 **[パラメーターの追加]** を選択します。  
  
    2.  **[名前]** ボックスに **productid** を入力します。  
  
    3.  **[データ型]** リスト ボックスで **[整数]** が選択されていることを確認します。  
  
    4.  **[OK]** をクリックします。  
  
9. .rdlc ファイルを保存します。  
  
## <a name="next-task"></a>次の作業  
これで、レポート ウィザードを使用して子レポートを設計できました。 次は、Web サイト アプリケーションに ReportViewer コントロールを追加します。 [「レッスン 6: アプリケーションに ReportViewer コントロールを追加する」](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)を参照してください。  
  
  
  

