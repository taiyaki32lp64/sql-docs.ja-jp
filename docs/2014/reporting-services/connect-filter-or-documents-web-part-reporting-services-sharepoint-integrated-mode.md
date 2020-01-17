---
title: 接続のフィルターまたはドキュメント Web パーツ (SharePoint 統合モードで Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 062733f1ee68cd90ccc1b9a15d0cadc06b7e6f89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109715"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>フィルター Web パーツまたはドキュメント Web パーツの接続 (Reporting Services の SharePoint 統合モード)
  SharePoint 製品を使用している場合、フィルター Web パーツまたはドキュメント Web パーツとレポート ビューアー Web パーツを含む、ダッシュボードや Web パーツ ページを作成できます。 サポートされているバージョンは [!INCLUDE[SPF2010](../includes/spf2010-md.md)] または [!INCLUDE[SPS2010](../includes/sps2010-md.md)]です。 [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] または [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 もサポートされています。 フィルター Web パーツを接続することによって、フィルター値をフィルター Web パーツで選択するユーザーは、同じページでパラメーター化されたレポートに値を送信できるようになります。 ドキュメント Web パーツを接続することによって、ドキュメント ライブラリでレポートをクリックするユーザーは、隣接するレポート ビューアー Web パーツでレポートを表示できるようになります。  
  
 フィルター Web パーツは、レポートで値を 1 つ以上のパラメーターに送信するために使用します。 フィルター Web パーツを使用するには、この Web パーツによって送信される値、データ型、および形式との互換性がある、この Web パーツ用のパラメーターをレポートに定義しておく必要があります。  
  
 ドキュメント Web パーツは、ホーム サイトのドキュメント ライブラリに関連付けられます。 ドキュメント ライブラリからアイテムを表示、追加、または削除するには、 **[すべてのサイト コンテンツの表示]** をクリックします。 ライブラリで、 **[ドキュメント]** をクリックします。 **[新規]** 、 **[アップロード]** 、および **[アクション]** メニューを使用してドキュメント ライブラリのアイテムを管理できます。  
  
### <a name="to-connect-a-filter-web-part"></a>フィルター Web パーツを接続するには  
  
1.  Web パーツ ページまたはダッシュボードを開くか、作成します。  
  
2.  **[サイトの操作]** メニューの **[ページの編集]** をクリックします。  
  
3.  **[Web パーツの追加]** をクリックします。  
  
4.  **[すべての Web パーツ]** の **[その他]** カテゴリで、 **[SQL Server Reporting Services レポート ビューアー]** をクリックします。  
  
5.  **[追加]** をクリックします。 Web パーツが、ゾーンの一番上に追加されます。  
  
6.  同一の Web パーツ ページまたはダッシュボードの別の領域で、 **[Web パーツの追加]** をクリックします。  
  
7.  **[すべての Web パーツ]** の **[フィルター]** セクションで、Web パーツを選択します。  
  
8.  **[追加]** をクリックします。 Web パーツが、ゾーンの一番上に追加されます。  
  
9. Web パーツを含むゾーンで、Web パーツの **[編集]** メニューの **[接続]** をポイントし、 **[フィルター値の送信先]** をポイントして [ **レポート ビューアー** - *レポート名*] をクリックします。  
  
10. 変更をチェックインし、ページを保存します。  
  
### <a name="to-connect-a-documents-web-part"></a>ドキュメント Web パーツを接続するには  
  
1.  Web パーツ ページまたはダッシュボードを開くか、作成します。  
  
2.  **[サイトの操作]** メニューの **[ページの編集]** をクリックします。  
  
3.  **[Web パーツの追加]** をクリックします。  
  
4.  **[すべての Web パーツ]** の **[リストまたはライブラリ]** セクションで **[ドキュメント]** をクリックします。  
  
5.  **[追加]** をクリックします。 Web パーツが、ゾーンの一番上に追加されます。  
  
6.  ツール ペインの下部で **[適用]** をクリックし、 **[OK]** をクリックしてペインを閉じます。  
  
7.  同一の Web パーツ ページまたはダッシュボードの別の領域で、 **[Web パーツの追加]** をクリックします。  
  
8.  **[すべての Web パーツ]** の **[その他]** カテゴリで、 **[SQL Server Reporting Services レポート ビューアー].**  
  
9. **[追加]** をクリックします。 Web パーツが、ゾーンの一番上に追加されます。  
  
10. Web パーツを含むゾーンで、Web パーツの **[編集]** メニューの **[接続]** をポイントし、 **[レポート定義の取得元]** をポイントして **[ドキュメント]** をクリックします。  
  
11. 変更をチェックインし、ページを保存します。  
  
## <a name="see-also"></a>参照  
 [レポート ビューアー Web パーツを Web ページに追加する (Reporting Services の SharePoint 統合モード)](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [SharePoint サイトのレポート ビューアー Web パーツ](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [レポート ビューアー Web パーツのカスタマイズ](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
