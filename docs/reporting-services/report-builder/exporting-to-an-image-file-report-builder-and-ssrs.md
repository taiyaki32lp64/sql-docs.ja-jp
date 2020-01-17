---
title: 画像ファイルへのエクスポート (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b7f94d9e8fcb1fa7ae2c3034286515e51c7fdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581216"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>画像ファイルへのエクスポート (レポート ビルダーおよび SSRS)
  画像表示拡張機能では、改ページ調整されたレポートがビットマップまたはメタファイルとして表示されます。 画像表示拡張機能では、既定でレポートの TIFF ファイルが生成されます。このファイルは、複数のページに表示することもできます。 クライアントは、受信した画像をイメージ ビューアーで表示したり、印刷したりできます。 ここでは、画像レンダラー固有の情報を提供し、また表示規則の例外について説明します。  
  
 画像表示拡張機能では、 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]でサポートされている形式 (BMP、EMF、EMFPlus、GIF、JPEG、PNG、TIFF) でファイルを生成できます。 TIFF 形式の場合、プライマリ ストリームのファイル名は *ReportName*.tif です。 その他の形式の場合は、1 ファイルが 1 ページに表示されます。ファイル名は *ReportName_Page.ext* (*ext* は選択した形式のファイル拡張子) です。 画像としてサポートされている別の形式でファイルを作成するには、上記の文字列のいずれかを **OutputFormatDeviceInfo** 設定で指定します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> サポートされている画像形式  
 次の表は、各画像レンダラー形式のファイルの拡張子と MimeType を示しています。  
  
|**型**|**拡張子**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|PNG|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> 複数ページの表示  
 1 つのファイルで複数のページのドキュメントをサポートしているファイル形式は TIFF だけです。 JPG や PNG などの他の形式では、一度に出力できるのは 1 ページで、ページごとに表示拡張機能を個別に呼び出す必要があります。  
  
  
##  <a name="Interactivity"></a> 対話性  
 このレンダラーで生成されたすべての画像形式では、対話機能がサポートされていません。 次の対話型要素は表示されません。  
  
-   ハイパーリンク  
  
-   表示/非表示  
  
-   ドキュメント マップ  
  
-   ドリルスルー リンクまたはクリックスルー リンク  
  
-   エンド ユーザー並べ替え  
  
-   固定ヘッダー  
  
-   ブックマーク  
  
  
##  <a name="DeviceInfo"></a> デバイス情報設定  
 デバイス情報設定を変更することによって、このレンダラーの既定の設定の一部を変更することができます。 詳細については、「 [画像デバイス情報設定](../../reporting-services/image-device-information-settings.md)」を参照してください。  
  
  
## <a name="see-also"></a>参照  
 [Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [さまざまなレポート表示拡張機能の対話機能 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [レポート アイテムのレンダリング &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
