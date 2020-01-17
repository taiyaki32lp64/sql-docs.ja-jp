---
title: 配信拡張機能に対する Setting クラスの使用 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 118f116de516e912b78b7467450b44116b432271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193598"
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>配信拡張機能に対する Setting クラスの使用
  <xref:Microsoft.ReportingServices.Interfaces.Setting> クラスは <xref:Microsoft.ReportingServices.Interfaces> 名前空間にあり、配信拡張機能の拡張機能設定に関する情報を表します。 <xref:Microsoft.ReportingServices.Interfaces.Setting> クラスは、配信拡張機能が正しく機能するために必要な設定に関する情報を格納するインフラストラクチャを提供します。 たとえば、レポート サーバーの電子メール配信では、ユーザーは受信者のアドレス、送信者のアドレス、電子メールの件名など、電子メール配信に固有の設定を入力する必要があります。 カスタム配信プロバイダーの場合にも、通知とレポートを配信する配信拡張機能のために、特定の設定を入力するようにユーザーに求めます。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Setting> クラスは、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> インターフェイスの <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> プロパティを実装する場合に使用します。 サブスクリプションまたは通知が作成された場合にユーザーが指定した拡張機能設定データを処理するためにも、<xref:Microsoft.ReportingServices.Interfaces.Setting> クラスを使用します。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Setting> クラスの使用例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [配信拡張機能の実装](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
