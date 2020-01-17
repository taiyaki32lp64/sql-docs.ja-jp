---
title: SharePoint 統合でのレポート ビューアー Web パーツのプログラミング | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a0bc7e2d99190e142647ab8732e2d2d48b3ea2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255127"
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 統合でのレポート ビューアー Web パーツのプログラミング
  レポート ビューアー Web パーツは、`T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart` サーバー コントロールです。このサーバー コントロールには、開発者がカスタム SharePoint アプリケーションを作成するためのパブリック アプリケーション プログラミング インターフェイス (API) のセットが含まれています。 Web パーツ接続を使用し、レポート ビューアー Web パーツにレポートのパスとパラメーターを指定するカスタム Web パーツを作成できます。 Web パーツをカスタム SharePoint Web パーツ ページに埋め込み、パブリック API を使用してカスタマイズすることもできます。  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>レポート ビューアー Web パーツとカスタム Web パーツとの接続  
 レポート ビューアー Web パーツは、<xref:System.Web.UI.WebControls.WebParts.IWebPartRow> または `T:Microsoft.SharePoint.WebPartPages.IFilterValues` を実装する SharePoint Web パーツに接続するコンシューマーです。 **ドキュメント** Web パーツなどの <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツを同じ Web パーツ ページにレポート ビューアー Web パーツとして配置すると、レポート ビューアー Web パーツにレポート パスを指定できます。 同様に、 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` Web パーツなど、**テキスト フィルター**または**フィルターの選択**、レポート ビューアー Web パーツ、レポート ビューアー Web と同じ Web パーツ ページに配置する場合にレポート パラメーターを指定することができます部分。  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>レポート パス プロバイダーと IWebPartRow の実装  
 Web パーツ接続を通じてレポート ビューアー Web パーツにレポートのパスを指定するには、次の手順に従います。  
  
1.  <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> インターフェイスを実装する Web パーツを作成します。  
  
2.  Web パーツを同じ Web パーツ ページにレポート ビューアー Web パーツとして追加します。  
  
3.  Web ベースの Web パーツ デザイン ユーザー インターフェイスで Web パーツをレポート ビューアー Web パーツに接続します。  
  
    > [!NOTE]  
    >  レポート ビューアー Web パーツに一度に接続できる <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツは 1 つだけです。レポート ビューアー Web パーツに <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツおよび `T:Microsoft.SharePoint.WebPartPages.IFilterValues` Web パーツの両方を同時に接続することはできません。  
  
 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツが `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart` で適切に機能するようにするには、<xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> メソッドで次の操作を行う必要があります。  
  
-   <xref:System.Data.DataRowView> オブジェクトを入力パラメーターとして使用してコールバック メソッドを呼び出します。  
  
-   <xref:System.Data.DataRowView> オブジェクトに、レポート パスを含む "DocUrl" という列が含まれるようにします。  
  
    > [!NOTE]  
    >  [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 用アドインのレポート ビューアー Web パーツでは、"FileRef" 列を使用するレポート パスを受信することもできます。  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>レポート パラメーター プロバイダーと IFilterValues の実装  
 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` を実装する Web パーツは、レポート ビューアー Web パーツに 1 つのパラメーター値を指定できます。 レポート ビューアー Web パーツに送信されるパラメーター値には、レポート定義で指定された、レポート パラメーターに対する制限と同じ制限 (データ型、有効な値など) が課されます。  
  
 レポート ビューアー Web パーツにレポート パラメーターを指定するには、次の手順に従います。  
  
1.  `T:Microsoft.SharePoint.WebPartPages.IFilterValues` インターフェイスを実装する Web パーツを作成します。  
  
2.  Web パーツを同じ Web パーツ ページに `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart` として追加します。  
  
3.  Web ベースの Web パーツ デザイン ユーザー インターフェイスで `T:Microsoft.SharePoint.WebPartPages.IFilterValues` Web パーツをレポート ビューアー Web パーツに接続します。  
  
    > [!NOTE]  
    >  一度に複数の `T:Microsoft.SharePoint.WebPartPages.IFilterValues` Web パーツをレポート ビューアー Web パーツに接続できます。 ただし、レポート ビューアー Web パーツに <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web パーツと `T:Microsoft.SharePoint.WebPartPages.IFilterValues` Web パーツの両方を同時に接続することはできません。  
  
## <a name="see-also"></a>参照  
 [IFilterValues インターフェイス](https://msdn.microsoft.com/library/office/microsoft.sharepoint.webpartpages.ifiltervalues\(v=office.15\).aspx)  
  
  
