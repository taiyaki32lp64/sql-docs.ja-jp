---
title: ATOM デバイス情報設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b20d11ac8a07632e9105c3963d19f7936832aec4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020650"
---
# <a name="atom-device-information-settings"></a>ATOM デバイス情報の設定
  ATOM 表示拡張機能のデバイス情報設定では、ATOM フィードの名前および使用する文字エンコードの送信がサポートされています。  
  
 次の表は、データ サービス ドキュメントに表示するためのデバイス情報設定を示しています。  
  
|設定|値|  
|-------------|-----------|  
|`DataFeed`|指定した場合、この設定で指定されたフィード名に対応する ATOM フィードが表示されます。 指定しない場合は、レポートの ATOM サービス ドキュメントが表示されます。 データ フィード固有の自動生成された識別子です。 これは内部で使用される値であり、変更はしないでください。|  
|**[エンコード]**|.NET Framework でサポートされている文字エンコードの Internet Assigned Numbers Authority (IANA) 名。 既定値は `UTF-8` です。 他の値には、ASCII、UTF-7、UTF-16 などがあります。|  
  
## <a name="see-also"></a>参照  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [表示拡張機能にデバイス情報設定を渡す](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
