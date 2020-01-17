---
title: PDF デバイス情報設定 | Microsoft Docs
ms.date: 03/16/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5442980dd2f67cf72e301a82ae3730f90a173116
ms.sourcegitcommit: 75fe364317a518fcf31381ce6b7bb72ff6b2b93f
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "70911329"
---
# <a name="pdf-device-information-settings"></a>PDF デバイス情報の設定
  次の表は、PDF 形式のレポートを表示するデバイス情報の設定を示しています。  
  
|設定|[値]|  
|-------------|-----------|  
| **AccessiblePDF** | サイズは大きいが、読み上げと移動のためのスクリーン リーダーやその他の支援技術で使いやすい、アクセシブル/タグ付き PDF をレンダリングするかどうかを示します。 既定値は **false**です。 [Power BI Report Server (2018 年 3 月) 以降で使用可能です] |
|**[列]**|レポートに設定する列の数。 この値により、レポートの元の設定はオーバーライドされます。|  
|**ColumnSpacing**|レポートに設定する列の間隔。 この値により、レポートの元の設定はオーバーライドされます。|  
|**DpiX**|出力デバイスの x 方向の解像度。|  
|**DpiY**|出力デバイスの y 方向の解像度。|  
|**EmbedFonts**|PDF ファイルにフォントを埋め込むかどうかを示します。サイズは大きくなりますが、レポートフォントはすべてのクライアントに対して正しく表示されます。 値が**None**の場合、フォントの埋め込みは無効になります。|  
|**EndPage**|表示するレポートの最後のページ。 既定値は **StartPage**の値です。|  
|**HumanReadablePDF**|サイズは大きいが、プレーンテキスト エディターで人間が読みやすい、未圧縮の PDF ファイルをレンダリングするかどうかを示します。 既定値は **false**です。|  
|**MarginBottom**|レポートに設定する下余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginLeft**|レポートに設定する左余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginRight**|レポートに設定する右余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**MarginTop**|レポートに設定する上余白の値 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、1in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PageHeight**|レポートに設定するページの高さ (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、11in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**PageWidth**|レポートに設定するページの幅 (インチ単位)。 整数または小数の値の後に "in" を付ける必要があります (たとえば、8.5in)。 この値により、レポートの元の設定はオーバーライドされます。|  
|**StartPage**|表示するレポートの最初のページ。 値 **0** はすべてのページを表示することを示します。 既定値は **1**です。|  
  
## <a name="see-also"></a>参照  
 [表示拡張機能にデバイス情報設定を渡す](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
