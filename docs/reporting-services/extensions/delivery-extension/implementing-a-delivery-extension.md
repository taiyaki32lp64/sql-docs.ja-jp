---
title: 配信拡張機能の実装 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4c0004f844d6914cea330d3a0c7332de783116c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193758"
---
# <a name="implementing-a-delivery-extension"></a>配信拡張機能の実装
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] により、ユーザーはレポートを作成し、パブリッシュできます。レポートは、作成しパブリッシュした後、さまざまな場所に配信できます。 さらに、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] には配信拡張機能と配信 API も用意されています。開発者は別の配信拡張機能を作成し、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の配信機能をさらに拡張することもできます。  
  
 配信拡張機能の実装例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [配信拡張機能の概要](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム配信拡張機能の記述方法について説明します。  
  
 [配信拡張機能を実装する準備](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能を実装する場合に使用できるインターフェイスとクラスに加え、実装前に考慮する問題についても説明します。  
  
 [配信拡張機能ライブラリの作成](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能の名前空間の割り当て、および配信拡張機能のライブラリ DLL へのコンパイルについて説明します。  
  
 [配信拡張機能に対する IDeliveryExtension インターフェイスの実装](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 配信拡張機能の属性、および独自の配信拡張機能クラスを実装する方法について説明します。  
  
 [配信拡張機能での Notification クラスの使用](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 **Notification** クラスの属性、および配信拡張機能の実装での使用方法について説明します。  
  
 [配信拡張機能に対する Setting クラスの使用](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 **Setting** クラスの属性、および配信拡張機能の実装での使用方法について説明します。  
  
 [配信拡張機能での Report クラスの使用](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 **Report** クラスの属性、および配信拡張機能の実装での使用方法について説明します。  
  
 [配信拡張機能での RenderedOutputFile クラスの使用](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 **RenderedOutputFile** クラスの属性、および配信拡張機能の実装での使用方法について説明します。  
  
 [配信拡張機能の配置](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 配信拡張機能の配置方法について説明します。  
  
 [配信拡張機能のコードのデバッグ](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 配信拡張機能でのコードのデバッグ方法について説明します。  
  
 [配信拡張機能の削除](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 レポート サーバーから配信拡張機能を削除する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
