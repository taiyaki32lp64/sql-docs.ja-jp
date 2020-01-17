---
title: Detail プロパティ | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 087f7f6da8882f181c55a187438d4493ec5b1a9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62991553"
---
# <a name="detail-property"></a>Detail プロパティ
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException** クラスの **Detail** プロパティには、次の XML 構造があります。  
  
## <a name="elements"></a>要素  
 **Detail**  
 他のすべてのエラー詳細要素を含む最上位要素。  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 固有のエラー コード。  
  
 **HttpStatus**  
 HTTP 状態コード。  
  
 **メッセージ**  
 レポート サーバーが割り当てたエラー メッセージとエラー コード。  
  
 **HelpLink**  
 エラーの詳細情報を参照できる Web サイトへのヘルプ リンクの URL。 詳細については、「[HelpLink 要素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)」を参照してください。  
  
 **LinkID**  
 リンクに割り当てられた ID です。  
  
 **ProductName**  
 製品の名前です。 既定値は **Microsoft SQL Server Reporting Services** です。  
  
 **ProductVersion**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のバージョン。 最大長は 15 文字です。 バージョン番号の形式は、8.00.0xxx.00 のようになります。  
  
 **ProductLocaleId**  
 アプリケーションの INTL DLL のロケール ID または言語 ID (0x41A など)。  
  
 **OperatingSystem**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インストール先のオペレーティング システム。 有効値は、依存しないオペレーティング システムの場合は **0**、[!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] の場合は **1**、Windows XP の場合は **16** です。  
  
 **CountryLocaleId**  
 オペレーティング システムのロケール ID または言語 ID。 たとえば、Windows のフランス語バージョンの値は 0x040c です。  
  
 **MoreInformation**  
 メソッド実行中に発生した入れ子にされた例外を含む XML 文字列です。  
  
 **ソース**  
 **MoreInformation** の子要素。 エラーのソースです。  
  
 **メッセージ**  
 **MoreInformation** の子要素。 入れ子にされた例外のエラー メッセージです。 この要素には、**ErrorCode** と **HelpLink** の XML 属性が含まれます。  
  
 **Warnings**  
 レポート処理から返された警告を含む XML 文字列です。  
  
## <a name="see-also"></a>参照  
 [Reporting Services における例外処理の概要](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException クラス](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail プロパティを使用したエラー処理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
