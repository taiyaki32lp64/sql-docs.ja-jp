---
title: 'レッスン 6: アプリケーションに ReportViewer コントロールを追加する | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b13a3653b19d4079a47941a0bb05faa2821c823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512537"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>レッスン 6: アプリケーションに ReportViewer コントロールを追加する
レポート ウィザードを使用して子レポートを設計した後は、Web サイト アプリケーションに ReportViewer コントロールを追加します。 ASP.NET レポート Web サイトを利用している場合、ReportViewer コントロールが default.aspx ページに追加されます。   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>アプリケーションに ReportViewer コントロールを追加するには  
  
1.  **ソリューション エクスプローラー**で、 **Default.aspx**を右クリックし、 **[ビュー デザイナー]** をクリックします。  
  
2.  default.aspx に ReportViewer コントロールが既に与えられている場合、 **手順 4**に進みます。 与えられていない場合、 **[ツールボックス]** ウィンドウの **[AJAX Extensions]** から **ScriptManager** コントロールをデザイン画面にドラッグします。  
  
3.  **[レポート]** から **ReportViewer** コントロールをデザイン画面の **ScriptManager** コントロールの下にドラッグします。  
  
4.  **ReportViewer** コントロールの右上にある矢印をクリックして、 **[ReportViewer タスク]** ウィンドウを開きます。  
  
5.  **[レポートの選択]** ボックスで、作成した親レポートを選択します。  
  
    レポートを選択すると、レポートで使用されているデータ ソースのインスタンスが自動的に作成されます。 それぞれの DataTable (とその [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) コンテナーを) をインスタンス化するためのコードが生成されます。 レポートで使用されているそれぞれのデータ ソースに対応する [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) コントロールがデザイン画面に追加されます。 このデータ ソース コントロールは自動的に構成されます。  
  
6.  [ビルド] メニューの [Web サイトのビルド] をクリックします。  
  
    レポートがコンパイルされ、レポート式の構文エラーなどのエラーが **[エラー一覧]** 領域に表示されます。 **[エラー一覧]** 領域を表示するには、Visual Studio ウィンドウの下部にある **[エラー一覧]** をクリックします。  
  
## <a name="next-task"></a>次の作業  
これで、Web サイト アプリケーションに ReportViewer コントロールを追加できました。 次は、親レポートにドリルスルー アクションを追加します。 「 [レッスン 7: 親レポートにドリルスルー アクションを追加する](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)」を参照してください。  
  

