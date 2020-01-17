---
title: フィルター Web パーツまたはドキュメント Web パーツを Reporting Services レポート ビューアー Web パーツと接続する | Microsoft Docs
ms.date: 11/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d833e0b42a6bfdaf9754525740f9bb58df794fdb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580027"
---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>フィルター Web パーツまたはドキュメント Web パーツを Reporting Services レポート ビューアー Web パーツと接続する

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint 製品を使用している場合、フィルター Web パーツまたはドキュメント Web パーツとレポート ビューアー Web パーツを含むダッシュボードや Web パーツ ページを作成できます。 サポートされているバージョンは [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] または [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]です。 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] または [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 もサポートされています。 フィルター Web パーツを接続することによって、フィルター値をフィルター Web パーツで選択するユーザーは、同じページでパラメーター化されたレポートに値を送信できるようになります。 ドキュメント Web パーツを接続することによって、ドキュメント ライブラリでレポートをクリックするユーザーは、隣接するレポート ビューアー Web パーツでレポートを表示できるようになります。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

 フィルター Web パーツは、レポートで値を 1 つ以上のパラメーターに値を送信するために使用します。 フィルター Web パーツを使用するには、フィルター Web パーツによって送信される値、データ型、形式との互換性があるパラメーターをレポートに定義しておく必要があります。  
  
 ドキュメント Web パーツは、ホーム サイトのドキュメント ライブラリに関連付けられます。 ドキュメント ライブラリからアイテムを表示、追加、または削除するには、 **[すべてのサイト コンテンツの表示]** をクリックします。 ライブラリで、 **[ドキュメント]** をクリックします。 **[新規]** 、 **[アップロード]** 、および **[アクション]** メニューを使用してドキュメント ライブラリのアイテムを管理できます。  
  
## <a name="connect-a-filter-web-part"></a>フィルター Web パーツを接続する
  
1.  Web パーツ ページまたはダッシュボードを開くか、作成します。  
  
2.  **[サイトの操作]** メニューの **[ページの編集]** をクリックします。  
  
3.  **[Web パーツの追加]** をクリックします。  
  
4.  **[すべての Web パーツ]** の **[その他]** カテゴリで、 **[SQL Server Reporting Services レポート ビューアー]** を選びます。  
  
5.  **[追加]** をクリックします。 Web パーツがゾーンの一番上に追加されます。  
  
6.  同一の Web パーツ ページまたはダッシュボードの別の領域で、 **[Web パーツの追加]** をクリックします。  
  
7.  **[すべての Web パーツ]** の **[フィルター]** セクションで、Web パーツを選びます。  
  
8.  **[追加]** をクリックします。 Web パーツがゾーンの一番上に追加されます。  
  
9. Web パーツを含むゾーンで、Web パーツの **[編集]** メニューの **[接続]** をクリックし、 **[フィルター値の送信先]** をポイントして [**レポート ビューアー** - *レポート名*] を選びます。  
  
10. 変更をチェックインし、ページを保存します。  
  
## <a name="connect-a-documents-web-part"></a>ドキュメント Web パーツを接続する  
  
1.  Web パーツ ページまたはダッシュボードを開くか、作成します。  
  
2.  **[サイトの操作]** メニューの **[ページの編集]** をクリックします。  
  
3.  **[Web パーツの追加]** をクリックします。  
  
4.  **[すべての Web パーツ]** の **[リストまたはライブラリ]** セクションで **[ドキュメント]** を選びます。  
  
5.  **[追加]** をクリックします。 Web パーツがゾーンの一番上に追加されます。  
  
6.  ツール ペインの下部で **[適用]** をクリックし、 **[OK]** をクリックしてペインを閉じます。  
  
7.  同一の Web パーツ ページまたはダッシュボードの別の領域で、 **[Web パーツの追加]** をクリックします。  
  
8.  **[すべての Web パーツ]** の **[その他]** カテゴリで、 **[SQL Server Reporting Services レポート ビューアー]** を選びます。  
  
9. **[追加]** をクリックします。 Web パーツがゾーンの一番上に追加されます。  
  
10. Web パーツを含むゾーンで、Web パーツの **[編集]** メニューをクリックし、 **[接続]** をポイントし、 **[レポート定義の取得元]** をポイントして **[ドキュメント]** を選びます。  
  
11. 変更をチェックインし、ページを保存します。  
  
## <a name="see-also"></a>参照

 [レポート ビューアー Web パーツを Web ページに追加する](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [SharePoint サイトのレポート ビューアー Web パーツ](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [レポート ビューアー Web パーツのカスタマイズ](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
