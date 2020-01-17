---
title: 'レッスン 3: レポート ウィザードを使用して親レポートを設計する | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ad06a5a76344348c71838873edcc490c75b7b2e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651278"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>レッスン 3: レポート ウィザードを使用して親レポートを設計する
親レポートのデータ接続とデータ テーブルを作成した後は、レポート デザイナーのレポート ウィザードを使用して親レポートを設計します。 レポート デザイナーの詳細については、「[レポート デザイナーを使用してレポートをデザインする &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)」を参照してください。  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>レポート ウィザードを使用して親レポートを設計するには  
  
1.  **ソリューション エクスプローラー**でトップレベル Web サイトが選択されていることを確認します。  
  
2.  Web サイトを右クリックし、 **[新しい項目の追加]** を選択します。  
  
3.  **[新しい項目の追加]** ダイアログ ボックスで、 **[レポート ウィザード]** を選択します。レポート ファイルの名前を入力し、 **[追加]** を選択します。  
  
    これにより、レポート ウィザードが起動します。  
  
4.  **[データセットのプロパティ]** ページの **[データ ソース]** ボックスで、「 **レッスン 2: 親レポートのデータ接続とデータ テーブルを定義する** 」で作成した [DataSet1](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)を選択します。  
  
    上の手順で作成した **DataTable** で **[使用できるデータセット]** ボックスが自動的に更新されます。  
  
5.  **[次へ]** を選択します。  
  
6.  **[フィールドの配置]** ページで、次の操作を行います。  
  
    1.  **[ProductID]** 、 **[Name]** 、 **[ProductNumber]** 、 **[SafetyStockLevel]** 、および **[ReorderLevel]** を、 **[使用できるフィールド]** から **&gt;[値]** ボックスにドラッグします。  
  
    2.  **[Sum(ProductID)]** 、 **[Sum(SafetyStockLevel)]** 、 **[Sum(ReorderLevel)]** の横の矢印を選択して、 **[Sum]** の選択を解除します。  
  
7.  **[次へ]** を 2 回選択し、 **[完了]** を選択して **レポート ウィザード**を閉じます。  
  
    これで .rdlc ファイルが作成されました。 このファイルはレポート デザイナーで開くことができます。 設計した Tablix がデザイン画面に表示されます。  
  
8.  .rdlc ファイルを保存します。  
  
## <a name="next-task"></a>次の作業  
これで、レポート ウィザードを使用して親レポートを設計できました。 次は、子レポートのデータ接続とデータ テーブルを作成します。 「 [レッスン 4: 子レポートのデータ接続とデータ テーブルを定義する](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)」を参照してください。  
  
  
  

