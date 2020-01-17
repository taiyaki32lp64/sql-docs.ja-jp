---
title: Reporting Services における例外処理の概要 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012326"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Reporting Services における例外処理の概要
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションが要求をレポート サーバー Web サービスに送信し、サービスが要求を処理できない場合、サービスは SOAP 例外をクライアントに返します。 レポート サーバー Web サービスによってスローされた例外の処理は、開発するアプリケーションの重要な部分です。エラーが発生した場合にユーザーに有益な情報を返すことができるからです。  
  
 ここでは、例外の処理、無効なユーザー入力の回避、およびユーザーへの有意義なエラー情報の送信について説明します。 例外処理の一般的な情報については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントの「例外の処理とスロー」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Reporting Services での例外を処理](handling-exceptions-in-reporting-services.md)|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] における例外および Web サービスからエラーを返すときの SOAP の役割について説明します。|  
|[Reporting Services 例外処理のベスト プラクティス](best-practices/best-practices-for-reporting-services-exception-handling.md)|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] での例外処理に関する推奨事項が記載されています。|  
|[Reporting Services SoapException クラス](soapexception-class/reporting-services-soapexception-class.md)|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の **SoapException** クラスについて説明します。|  
  
## <a name="see-also"></a>関連項目  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
