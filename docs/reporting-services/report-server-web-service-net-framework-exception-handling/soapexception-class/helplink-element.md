---
title: HelpLink 要素 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ed62c34095adc2e9c039d1780f616530679b601
ms.sourcegitcommit: 3be14342afd792ff201166e6daccc529c767f02b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68307577"
---
# <a name="helplink-element"></a>HelpLink 要素
  **Detail** プロパティの **HelpLink** 要素は、レポート サーバーで生成される URL 文字列です。 この URL は [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ヘルプとサポートで管理されている Web ページを指し、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] で発生する特定のエラーに関するヘルプとサポート技術情報の記事を提供します。 URL の構文は、次のようになっています。  
  
 **https://** www\.microsoft.com **/** products **/** ee **/** transform.aspx **?EvtSrc**=v_alue_ **&EvtID**=_value_ **&ProdName**=_value_ **&ProdVer**=*value*  
  
 次の表は、**HelpLink** URL の引数を示しています。  
  
|引数|[値]|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|レポート サーバー エラー コード。たとえば、rsReservedItem。|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services"。 製品名の値は URL エンコードされています。|  
|**ProdVer**|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のバージョン番号。 "8.00" の値は、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を示します。|  
  
 次の例は、エラー コード **rsReservedItem** に返された **HelpLink** URL を示しています。 このエラーは、ユーザーが [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の予約アイテムの変更または削除を試みたときに発生します。  
  
```  
https://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 コードで **HelpLink** 要素にアクセスするには、**SoapException** クラスを使用します。  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>参照  
 [Reporting Services における例外処理の概要](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException クラス](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail プロパティを使用したエラー処理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
