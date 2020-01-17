---
title: Web サービスと .NET Framework を使用してのアプリケーションの構築 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application building
- .NET Framework [Reporting Services]
- XML Web service [Reporting Services], client creation
- reports [Reporting Services], building
- Web service [Reporting Services], application building
- Report Server Web service, client creation
- client configuration [Reporting Services]
- XML Web service [Reporting Services], application building
- Web service [Reporting Services], client creation
ms.assetid: 92a9678c-bc4f-4d7a-ba44-85989bfe27ca
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5136c67077ff90e7bbbd66ae72fed891267ba7a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62520348"
---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Web サービスと .NET Framework を使用したアプリケーションの構築
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] により、メソッド、プリミティブ型、およびユーザー定義の複合型などの、Web サービスと連動する、おなじみのプログラミング構成要素を使用できます。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] により、W3C (World Wide Web Consortium) の標準に準拠した任意の Web サービスを呼び出すことができる、Web サービス クライアントを作成するためのインフラストラクチャとツールが提供されます。  
  
 レポート サーバー Web サービス クライアントとは、Simple Object Access Protocol (SOAP) メッセージを使用して、レポート サーバーと通信をする任意のコンポーネントまたはアプリケーションのことです。  
  
 **.NET Framework を使用してレポート サーバー Web サービス クライアントを作成するには、以下の基本手順に従います。**  
  
1.  Web サービスのプロキシ クラスを作成します。  
  
     そのためには、プロキシ クラスまたは Web 参照を開発プロジェクトに追加し、クライアント コードでそのプロキシ クラスを参照します。次に、そのプロキシのインスタンスを生成します。 詳細については、「[Web サービス プロキシの作成](creating-the-web-service-proxy.md)」を参照してください。  
  
2.  レポート サーバーで Web サービス クライアントを認証します。  
  
     そのためには、サービス オブジェクトの <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> プロパティを、レポート サーバーで認証されるユーザーの資格情報と同じに設定します。 詳細については、「[Web サービス認証](web-service-authentication.md)」を参照してください。  
  
3.  呼び出す Web サービス操作に対応したプロキシ クラスのメソッドを呼び出します。  
  
     そのためには、Web サービス メソッドを呼び出し、必要な引数を指定します。 Web サービス メソッドの詳細については、「[レポート サーバー Web サービス メソッド](../methods/report-server-web-service-methods.md)」を参照してください。 呼び出しの詳細については、「[Web サービス メソッドの呼び出し](calling-web-service-methods.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Web サービス プロキシの作成](creating-the-web-service-proxy.md)|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] を使用してプロジェクトにプロキシ クラスを追加する方法を説明します。|  
|[Web サービス認証](web-service-authentication.md)|レポート サーバー Web サービスに対する呼び出しの認証方法について説明します。|  
|[Web サービス メソッドの呼び出し](calling-web-service-methods.md)|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] を使用して、Web サービス メソッドを呼び出すための SOAP API の使用法を説明します。|  
|[Web サービスの Url プロパティを設定](setting-the-url-property-of-the-web-service.md)|Web 参照の作成後に新しいサーバーの URL を Web サービス プロキシに知らせるためのプログラミング方法について説明します。|  
|[Web サービス メソッドの引数の指定](supplying-web-service-method-arguments.md)|Web サービス メソッドを呼び出す方法およびメソッドの引数の指定方法を説明します。|  
|[省略可能な Web サービス オブジェクトの値を省略](omitting-values-for-optional-web-service-objects.md)|省略可能な Web サービス オブジェクトの値の省略方法を説明します。|  
|[セキュリティで保護された Web サービス メソッドの使用](using-secure-web-service-methods.md)|**SecureConnectionLevel** の設定、およびそれが Reporting Services SOAP API の使用にどのように影響するのかを説明します。|  
|[表示拡張機能にデバイス情報設定を渡す](passing-device-information-settings-to-rendering-extensions.md)|異なる形式でレポートを表示するための、デバイス情報の設定について説明します。|  
|[Reporting Services 配信拡張機能の設定](reporting-services-delivery-extension-settings.md)|レポート サーバーの電子メールを使用してレポートを配信するための設定について説明します。|  
|[Reporting Services SOAP ヘッダーの使用](../../report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の SOAP ヘッダーの使用について説明します。|  
|[Reporting Services における例外処理の概要](../../report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のエラー処理方法に関する情報を提供します。|  
  
## <a name="see-also"></a>参照  
 [レポート サーバー Web サービス](../report-server-web-service.md)   
 [テクニカル リファレンス (SSRS)](../../technical-reference-ssrs.md)  
  
  
