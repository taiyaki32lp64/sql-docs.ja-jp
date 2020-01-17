---
title: Web アプリケーションでの URL アクセスの使用 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9f2a3c9db568d6c6cddc71ec221f68306acb7f22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741695"
---
# <a name="integrating-reporting-services-using-url-access---web-application"></a>URL アクセスを使用した Reporting Services の統合 - Web アプリケーション
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL アクセスは、ネットワークを介して各レポートにアクセスできるように特別に設計されています。 この種類のアクセスは、レポートの表示およびナビゲーションをカスタム Web アプリケーションに統合するのに最適です。 Web アプリケーションで URL アクセスを使用するには、次の方法があります。  
  
-   Web サイトまたはポータルから特定のレポート サーバーへの URL を指定する。  
  
-   フォームの POST メソッドを使用する。さらに、フォーム フィールドを使用してクエリ文字列パラメーターをレポート サーバーの URL に渡す。  
  
## <a name="url-access-through-direct-addressing"></a>直接アドレス指定による URL アクセス  
 URL を使用してレポート サーバーまたはレポート サーバー データベースのアイテムにアクセスする場合は、Web ブラウザーまたはアプリケーション内から URL アドレスを指定するだけです。 また、アクセス中のレポートまたはリソースの外観に影響を与える可能性がある URL にパラメーターを指定することもできます。 Web ブラウザーのアドレス バーで URL を指定してレポート サーバーを対象としたり、URL を大規模な Web アプリケーションまたはポータルの一部である **IFrame** のソースにしたりすることができます。 レポートの特定のフレームを対象としたり、その過程で新しいブラウザー ウィンドウを開いたりするだけでなく、ポータルの Web ページでレポートのハイパーリンクを含めることもできます。  
  
 次の例では、ハイパーリンクは "main" という名前のフレームを対象とし、ハイパーリンクを含むハイパーリンクとは異なります。 ハイパーリンクは、Web ポータルの一部となる場合もあります。  
  
```  
<a href="https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 前の例では、URL のクエリ文字列の "main" の値を使用して、デバイス情報設定 **LinkTarget** が渡されます。 これにより、レポートのドリルスルー ハイパーリンクも確実に "main" という名前のフレームを対象とします。  
  
 デバイス情報設定の詳細については、「[表示拡張機能にデバイス情報設定を渡す](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)」を参照してください。  
  
 多くのサーバーおよびブラウザーでは、URL に使用可能な文字数が制限されているので注意してください。 場合によっては、256 文字の制限が適用されます。 この制限を回避するには、フォーム送信による POST 要求を使用できます。  
  
> [!NOTE]  
>  Internet Explorer の URL の最大文字数は 2,083 文字です。 この制限は、URL を要求する POST および GET に適用されます。 ただし、フォームの一部として名前と値の組を送信する場合、POST は URL のサイズによる制限を受けません。これは、名前と値の組が URL でなくヘッダーで転送されるためです。  
  
## <a name="url-access-through-a-form-post-method"></a>フォームの POST メソッドを使用した URL アクセス  
 URL アクセスを使用してレポート サーバーからデータを要求する場合、HTTP 要求では GET メソッドを使用します。 これは、METHOD="GET" の場合のフォーム送信と同じです。 METHOD="GET" を使用した URL 要求またはフォーム送信は、サーバーまたは Web ブラウザーが処理できる最大文字数による制限を受けます。  
  
 POST 要求 (METHOD="POST" と入力フィールド) の場合、名前と値の組が URL ではなくヘッダーで転送されます。 したがって、クエリ文字列の名前と値の組は URL の一部ではないため、より長い、かつ複雑なパラメーター リストを指定できます。  
  
 ユーザーは直接アクセスを使用して、レポート サーバーの URL を表示したり、クエリ文字列を変更したり、後で使用するために特定の URL 要求とレポート サーバー パラメーターを書き留めたりすることができます。  
  
 次の HTML サンプルは、特定の URL を使用してレポート サーバーを対象とし、クエリ文字列パラメーターをフォームの入力フィールドの一部として渡すことができるフォームの使用を示します。  
  
```  
<FORM id="frmRender" action="https://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 前の例では、フォームのボタンをクリックすると、レポート サーバーによって、現在のフレームで対象となっている HTML で表示されたレポートが返されます。 前の例に対して、この例での URL アクセスの文字列は、次のようになります。  
  
```  
https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>参照  
 [アプリケーションへの Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [URL アクセスを使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Windows アプリケーションでの URL アクセスの使用](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [URL アクセス &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)  
  
  
