---
title: SharePoint 統合でのレポート ビューアー Web パーツのプログラミング | Microsoft Docs
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: reference
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 990dba53ca575e09bcfefead21b5e37c82754c40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187299"
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 統合でのレポート ビューアー Web パーツのプログラミング
  レポート ビューアー Web パーツは、開発者がカスタム SharePoint アプリケーションを作成するためのパブリック アプリケーション プログラミング インターフェイス (API) のセットが含まれているサーバー コントロールです。 Web パーツ接続を使用し、レポート ビューアー Web パーツにレポートのパスとパラメーターを指定するカスタム Web パーツを作成できます。 Web パーツをカスタム SharePoint Web パーツ ページに埋め込み、パブリック API を使用してカスタマイズすることもできます。  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>レポート ビューアー Web パーツとカスタム Web パーツとの接続  
 レポート ビューアー Web パーツは、<xref:System.Web.UI.WebControls.WebParts.IWebPartRow> または T:Microsoft.SharePoint.WebPartPages.IFilterValues を実装する SharePoint Web パーツに接続するコンシューマーです。 **ドキュメント** Web パーツなどの <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツを同じ Web パーツ ページにレポート ビューアー Web パーツとして配置すると、レポート ビューアー Web パーツにレポート パスを指定できます。 同様に、**テキスト フィルター** Web パーツや**フィルターの選択** Web パーツなどの T:Microsoft.SharePoint.WebPartPages.IFilterValues Web パーツを同じ Web パーツ ページにレポート ビューアー Web パーツとして配置すると、レポート ビューアー Web パーツにレポート パラメーターを指定できます。  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>レポート パス プロバイダーと IWebPartRow の実装  
 Web パーツ接続を通じてレポート ビューアー Web パーツにレポートのパスを指定するには、次の手順に従います。  
  
1.  <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> インターフェイスを実装する Web パーツを作成します。  
  
2.  Web パーツを同じ Web パーツ ページにレポート ビューアー Web パーツとして追加します。  
  
3.  Web ベースの Web パーツ デザイン ユーザー インターフェイスで Web パーツをレポート ビューアー Web パーツに接続します。  
  
    > [!NOTE]  
    >  レポート ビューアー Web パーツに一度に接続できる <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツは 1 つだけです。レポート ビューアー Web パーツに <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツと T:Microsoft.SharePoint.WebPartPages.IFilterValues Web パーツの両方を同時に接続することはできません。  
  
 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart と <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツを正しく連動させるには、<xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> メソッドで次を行う必要があります。  
  
-   <xref:System.Data.DataRowView> オブジェクトを入力パラメーターとして使用してコールバック メソッドを呼び出します。  
  
-   <xref:System.Data.DataRowView> オブジェクトに、レポート パスを含む "DocUrl" という列が含まれるようにします。  
  
    > [!NOTE]  
    >  [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 用アドインのレポート ビューアー Web パーツでは、"FileRef" 列を使用するレポート パスを受信することもできます。  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>レポート パラメーター プロバイダーと IFilterValues の実装  
 T:Microsoft.SharePoint.WebPartPages.IFilterValues を実装する Web パーツは、レポート ビューアー Web パーツに 1 つのパラメーター値を指定できます。 レポート ビューアー Web パーツに送信されるパラメーター値には、レポート定義で指定された、レポート パラメーターに対する制限と同じ制限 (データ型、有効な値など) が課されます。  
  
 レポート ビューアー Web パーツにレポート パラメーターを指定するには、次の手順に従います。  
  
1.  T:Microsoft.SharePoint.WebPartPages.IFilterValues インターフェイスを実装する Web パーツを作成します。  
  
2.  T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart と同じページに Web パーツを追加します。  
  
3.  Web ベースの Web パーツ デザイン ユーザー インターフェイスで T:Microsoft.SharePoint.WebPartPages.IFilterValues Web パーツをレポート ビューアー Web パーツに接続します。  
  
    > [!NOTE]  
    >  複数の T:Microsoft.SharePoint.WebPartPages.IFilterValues Web パーツをレポート ビューアー Web パーツに一度に接続できます。 ただし、<xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツと T:Microsoft.SharePoint.WebPartPages.IFilterValues Web パーツの両方をレポート ビューアー Web パーツに同時に接続することはできません。  
  
  
