---
title: 画像デバイス情報設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b59fcf947a283ef60f5dd34f60e2cf365092cfa7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738730"
---
# <a name="image-device-information-settings"></a>画像デバイス情報設定
  次の表は、IMAGE 形式で表示するためのデバイス情報設定を示しています。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|**[列]**|レポートに設定する列の数。 この値により、レポートの元の設定はオーバーライドされます。|  
|**ColumnSpacing**|レポートに設定する列の間隔。 この値により、レポートの元の設定はオーバーライドされます。|  
|**DpiX**|出力画像の水平方向の解像度。 既定値は **96**です。 **BMP**、 **GIF**、 **PNG**、 **TIFF** の各出力形式に適用されます。|  
|**DpiY**|出力画像の垂直方向の解像度。 既定値は **96**です。 **BMP**、 **GIF**、 **PNG**、 **TIFF** の各出力形式に適用されます。|  
|**EndPage**|表示するレポートの最後のページ。 既定値は **StartPage**の値です。|  
|**MarginBottom**|レポートに設定する下余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **1in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginLeft**|レポートに設定する左余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **1in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginRight**|レポートに設定する右余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **1in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginTop**|レポートに設定する上余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **1in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**OutputFormat**|[!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) でサポートされるいずれかの出力形式。 **BMP**、 **EMF**、 **GIF**、 **JPEG**、 **PNG**、または **TIFF**です。|  
|**PageHeight**|レポートに設定するページの高さ (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **11in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PageWidth**|レポートに設定するページの幅 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、 **8.5in**)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PrintDpiX**|出力画像の水平方向の解像度。 既定値は、 **300**です。 拡張メタファイル (**EMF**) 出力形式に適用されます。|  
|**PrintDpiY**|出力画像の垂直方向の解像度。 既定値は、 **300**です。 拡張メタファイル (**EMF**) 出力形式に適用されます。|  
|**StartPage**|表示するレポートの最初のページ。 値 **0** はすべてのページを表示することを示します。 既定値は **1**です。|  
  
## <a name="see-also"></a>参照  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [表示拡張機能にデバイス情報設定を渡す](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
