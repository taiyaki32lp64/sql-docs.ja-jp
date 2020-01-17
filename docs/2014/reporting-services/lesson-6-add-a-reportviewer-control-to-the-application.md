---
title: 'レッスン 6: アプリケーションに ReportViewer コントロールの追加 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfce5e2bdf71dfb58481fedf05794d3603285449
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108422"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>レッスン 6: アプリケーションに ReportViewer コントロールを追加する
  レポート ウィザードを使用して子レポートを設計した後は、Web サイト アプリケーションに ReportViewer コントロールを追加します。  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>アプリケーションに ReportViewer コントロールを追加するには  
  
1.  **ソリューション エクスプローラー**で、 **Default.aspx**を右クリックし、 **[ビュー デザイナー]** をクリックします。  
  
2.  **AJAX Extensions**グループにおいて、**ツールボックス**ウィンドウで、ドラッグ、 **ScriptManager**コントロールをデザイン画面。  
  
3.  **[レポート]** から **ReportViewer** コントロールをデザイン画面の **ScriptManager** コントロールの下にドラッグします。  
  
4.  **ReportViewer** コントロールの右上にある矢印をクリックして、 **[ReportViewer タスク]** ウィンドウを開きます。  
  
5.  **レポートの選択**ボックスで、作成した親レポートを選択します。  
  
     レポートを選択すると、レポートで使用されているデータ ソースのインスタンスが自動的に作成されます。 それぞれの DataTable (とその [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) コンテナーを) をインスタンス化するためのコードが生成されます。 レポートで使用されているそれぞれのデータ ソースに対応する [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) コントロールがデザイン画面に追加されます。 このデータ ソース コントロールは自動的に構成されます。  
  
     Microsoft Visual Studio 2012 を使用している場合は、完全修飾名が表示されている場合、プロジェクトの名前空間で完全修飾 DataSet1 に ObjectDataSource コントロールがバインドされていることを確認してください、 **ビジネスオブジェクトの選択**ドロップダウン リスト ボックス (たとえば、Projectnamespace.DataSet1TableAdapters.ProductTableAdapter)。 リスト ボックスにアクセスするには、ObjectDataSource を右クリックし、をクリックして**データ ソースの構成**します。  
  
6.  [ビルド] メニューの [Web サイトのビルド] をクリックします。  
  
     レポートがコンパイルされ、レポート式の構文エラーなどのエラーが **[エラー一覧]** 領域に表示されます。 **[エラー一覧]** 領域を表示するには、Visual Studio ウィンドウの下部にある **[エラー一覧]** をクリックします。  
  
## <a name="next-task"></a>次の作業  
 これで、Web サイト アプリケーションに ReportViewer コントロールを追加できました。 次は、親レポートにドリルスルー アクションを追加します。  
  
  
