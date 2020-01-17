---
title: URL でデバイス情報設定を指定する | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 906a21de49d562d788f9a1384b31e080616c67c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578440"
---
# <a name="specify-device-information-settings-in-a-url"></a>URL でデバイス情報設定を指定する
  デバイス情報設定は、表示拡張機能に渡すパラメーターのことです。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] レポート サーバー Web サービスのメソッドを使用してレポートを表示する場合は、 **DeviceInfo** XML 要素を入力パラメーターとして渡す必要があります。 **DeviceInfo** 要素の子要素は、各種表示拡張機能のデバイス情報設定に固有です。 *rc:tag=value* パラメーターの文字列を使用することによって、デバイス情報設定を URL に含めることができます。ここでは、 *tag* はアクセス先デバイス情報設定要素の名前です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]デバイス情報設定の詳細については、「表 [示拡張機能にデバイス情報設定を渡す](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、画像表示拡張機能の *OutputFormat* デバイス情報設定を使用して、指定されたレポートの形式を JPEG に設定します。読みやすいように改行しています。  
  
```  
https://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>参照  
 [URL アクセス &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)  
  
  
