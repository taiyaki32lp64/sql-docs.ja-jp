---
title: PDF デバイス情報設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 36def4705f6b2be9d5e1828f920ae41a51477272
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108088"
---
# <a name="pdf-device-information-settings"></a>PDF デバイス情報の設定
  次の表は、PDF 形式のレポートを表示するデバイス情報の設定を示しています。  
  
|設定|値|  
|-------------|-----------|  
|**[列]**|レポートに設定する列の数。 この値により、レポートの元の設定はオーバーライドされます。|  
|**ColumnSpacing**|レポートに設定する列の間隔。 この値により、レポートの元の設定はオーバーライドされます。|  
|**DpiX**|出力デバイスの x 方向の解像度。|  
|**DpiY**|出力デバイスの y 方向の解像度。|  
|**EndPage**|表示するレポートの最後のページ。 既定値は `StartPage` の値です。|  
|`HumanReadablePDF`|PDF を圧縮するかどうかを示します。圧縮することにより、ソースをより見やすくすることができます。 既定値は `false.`|  
|**MarginBottom**|レポートに設定する下余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginLeft**|レポートに設定する左余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginRight**|レポートに設定する右余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginTop**|レポートに設定する上余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PageHeight**|レポートに設定するページの高さ (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、11in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PageWidth**|レポートに設定するページの幅 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、8.5in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|`StartPage`|表示するレポートの最初のページ。 値 `0` はすべてのページを表示することを示します。 既定値は `1` です。|  
  
## <a name="see-also"></a>関連項目  
 [表示拡張機能にデバイス情報設定を渡す](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
