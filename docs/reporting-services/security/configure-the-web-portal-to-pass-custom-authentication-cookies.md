---
title: カスタム認証クッキーを送信するように Web ポータルを構成する | Microsoft Docs
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2f3200a17f00efedae3f52be7f3b17df31167765
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579425"
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>カスタム認証クッキーを送信するように Web ポータルを構成する

カスタム認証拡張機能を使用している場合、カスタム認証クッキーを送信するように Web ポータルを構成してください。 構成しない場合、Web ポータルはレポート サーバー固有の HTTP 要求を使用してクッキーを送信するだけです。 追加のクッキーを送信するには、RSReportServer.Config ファイルを変更する必要があります。

## <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.Config ファイルの変更

[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] を有効にしてレポート サーバーに追加のクッキーを送信できます。RSReportServer.config ファイルの Web ポータル構成設定に \<**PassThroughCookies**> 要素を追加します。 追加のクッキーの送信は、レポート サーバーの認証クッキーだけでなく、サード パーティの認証システムのクッキーも必要なシングル サインオン認証ソリューションで便利です。

Web ポータルの使用時に HTTP 要求を使用した追加のクッキーの送信を有効にするには、RSReportServer.config ファイルに次の要素を設定してください。
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>参照

[レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[セキュリティ拡張機能の概要](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[レポート サーバーを構成および管理する &#40;SSRSネイティブ モード&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
その他の質問 [Reporting Services のフォーラムにアクセスします](https://go.microsoft.com/fwlink/?LinkId=620231)
