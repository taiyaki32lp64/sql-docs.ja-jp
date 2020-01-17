---
title: XML デバイス情報設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee4e9f30dc190aae78e1e3e763451e42b3a52ecb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571013"
---
# <a name="xml-device-information-settings"></a>XML デバイス情報設定
  次の表は、XML 形式で表示するためのデバイス情報設定を示しています。  
  
|設定|値|詳細|  
|-------------|------------|-------------|  
|**XSLT (XSLT)**|XML ファイルに適用される XSLT のレポート サーバー名前空間のパス (例: **/Transforms/myxslt**)。|xsl ファイルはレポート サーバーのパブリッシュされたリソースであることが必要です。ファイルには、レポート サーバー アイテム パスを使用してアクセスする必要があります。 この設定の値は、レポートに指定された XSLT の後に適用されます。 **XSLT** 設定が適用されると、 **OmitSchema** 設定は無視されます。|  
|**MIMEType**|XML ファイルの MIME (Multipurpose Internet Mail Extensions) の種類。||  
|**UseFormattedValues**|**true**<br /><br /> **false**|XML データを生成するときにテキスト ボックスの書式設定された値を表示するかどうかを示します。<br /><br /> false の値は、テキスト ボックスの基になる値を使用することを示します。|  
|**Indented**|**true**<br /><br /> **false**|インデントされた XML を生成するかどうかを示します。 既定値の **false** の場合、インデントなしの圧縮された XML が生成されます。|  
|**OmitNamespace**|**true**<br /><br /> **false**|XML から既定の名前空間を省略するかどうかを示します。<br /><br /> true の場合、XML で既定の名前空間が指定されません。<br /><br /> false の場合、XML ではレポートの DataSchema プロパティの値を使用して既定の名前空間が指定されます。 DataSchema プロパティは、既定でレポートの名前になります。<br /><br /> 既定値は**false**です。|  
|**OmitSchema**|**true**<br /><br /> **false**|XML からスキーマの場所を省略するかどうかを示します。 場所は SchemaLocation 属性です。<br /><br /> OmitSchema の既定値は OmitNamespace の値によって決まります。<br /><br /> OmitNamespace = False の場合、既定では、OmitSchema = **False** です。 ユーザーは OmitSchema = True を設定して既定値をオーバーライドできます。<br /><br /> OmitNamespace = True の場合、OmitShema に明示的に構成した値に関係なく、OmitSchema は **True** として機能します。|  
|**[エンコード]**|.NET Framework でサポートされている文字エンコードの Internet Assigned Numbers Authority (IANA) 名。|既定値は **UTF-8**です。 他の値には、ASCII、UTF-7、UTF-16 などがあります。|  
|**FileExtension**|生成されたファイルに使用するファイル拡張子。||  
|**[スキーマ]**|**true** の値は、XML スキーマを表示することを示します。 既定値は **false**です。|XML スキーマ定義 (XSD) を表示するか、実際の XML データを表示するかを示します。|  
  
## <a name="see-also"></a>参照  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [表示拡張機能にデバイス情報設定を渡す](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
