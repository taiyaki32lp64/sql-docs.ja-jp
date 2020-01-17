---
title: 配信拡張機能に対する IDeliveryExtension インターフェイスの実装 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a0f9ab0767a09016d4f4bc1158988965bfc13b27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181423"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>配信拡張機能に対する IDeliveryExtension インターフェイスの実装
  配信拡張機能のクラスは、通知のコンテンツに基づいてレポート通知をユーザーに配信する場合に使用します。 配信拡張機能のクラスは、配信拡張機能に渡すユーザー設定を検証するためのインフラストラクチャも提供します。 また、配信拡張機能のクラスには、クライアントが拡張機能の名前に関する情報を取得する場合に使用できる特定のプロパティ、拡張機能がサポートする設定、および配信拡張機能で使用できる表示形式が含まれている必要があります。  
  
 ![IDeliveryExtension インターフェイスの処理](../../media/bk-ext-02.gif "IDeliveryExtension インターフェイスの処理")  
IDeliveryExtension インターフェイスを使用すると、ユーザー データを検証できることに加えて、クライアントが必要な配信設定を学習することもできます。  
  
 配信拡張機能のクラスを作成するには、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> および <xref:Microsoft.ReportingServices.Interfaces.IExtension> を実装します。 **IDeliveryExtension** インターフェイスでは、配信拡張機能による <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> メソッドを使用したレポート通知の配信、および <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> メソッドを使用した受信済み拡張機能設定の検証が可能です。 **IExtension** インターフェイスでは、配信拡張機能によるローカライズされた拡張機能名の実装、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成ファイルに格納された拡張機能固有の構成情報の処理が可能です。 **IExtension** を実装すると、配信拡張機能に <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> プロパティが含まれます。 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 配信拡張機能で **LocalizedName** プロパティをサポートすることを強くお勧めします。これにより、レポート マネージャーなどのユーザー インターフェイスで使い慣れた拡張機能名がユーザーに表示されます。  
  
 配信拡張機能では **IDeliveryExtension** インターフェイスの **ExtensionSettings** プロパティも実装する必要があります。 レポート サーバーは、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> プロパティから返された値を使用して、配信拡張機能が必要とする設定を評価します。 配信拡張機能と対話するクライアントは、レポート サーバー Web サービスの <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> メソッドを使用して、配信拡張機能の設定一覧を返します。  
  
 配信拡張機能のクラスを使用すると、RSReportServer.config ファイルに格納されたカスタム構成データを取得および処理することもできます。 カスタム構成データの処理の詳細については、<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A> メソッドを参照してください。  
  
 **IDeliveryExtension** クラスの実装例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [配信拡張機能の実装](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
