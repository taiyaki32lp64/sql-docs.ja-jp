---
title: カスタム セキュリティ拡張機能をインストールする方法 | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fcef802f6c61b85b4905365bda075a9f11d9e10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68223231"
---
# <a name="how-to-install-custom-security-extensions"></a>カスタム セキュリティ拡張機能をインストールする方法

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 では新しい Web ポータルが導入されました。このポータルは、新しい Odata API をホストし、また、モバイル レポートや KPI などの新しいレポート ワークロードをホストするためのものです。 この新しいポータルは新しいテクノロジに依存しており、別のプロセスで実行することで使い慣れた ReportingServicesService からは分離されます。 このプロセスでは、アプリケーションを ASP.NET でホストしないため、既存のカスタム セキュリティ拡張機能の前提条件には従いません。 さらに、カスタム セキュリティ拡張機能の現在のインターフェイスではどの外部コンテキストも渡すことができず、実装者は既知のグローバル ASP.NET オブジェクトを検査するしかありません。そのため、インターフェイスの一部を変更する必要がありました。

## <a name="what-changed"></a>変更内容

導入された新しいインターフェイスを実装することで、認証に関する決定を行う場合に拡張機能で使用されるより一般的なプロパティを提供する IRSRequestContext を提供できます。

以前のバージョンでは、レポート マネージャーはフロント エンドだったため、独自のカスタム ログイン ページで構成できました。 Reporting Services 2016 では、reportserver でホストされる 1 ページのみがサポートされ、両方のアプリケーションに対して認証を行う必要があります。

## <a name="implementation"></a>実装

以前のバージョンでは、拡張機能は、ASP.NET オブジェクトをすぐに使用できるという一般的な前提条件に依存できました。 ASP.NET では新しいポータルが実行されないため、拡張機能ではオブジェクトが NULL になるという問題が発生する可能性があります。

最も一般的な例は、ヘッダーや Cookie などの要求情報を読み取るための HttpContext.Current へのアクセスです。 拡張機能で同じ決定を行えるように、新しいメソッドを拡張機能に導入しました。このメソッドは要求情報を提供し、ポータルからの認証時に呼び出されます。 

これを活用するには、拡張機能で <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> インターフェイスを実装する必要があります。 拡張機能では両方のバージョンの <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> メソッド (reportserver コンテキストとその他の Web ホスト プロセスで使用されるコンテキストによって呼び出される) を実装する必要があります。 以下のサンプルは、reportserver で解決される ID が使用されるポータルの単純な実装の 1 つを示しています。

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>配置と構成

カスタム セキュリティ拡張機能に必要な基本構成は、以前のリリースと同じです。 web.config および rsreportserver.config の変更が必要です。詳細については、「[レポート サーバーでカスタム認証またはフォーム認証を構成する](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)」を参照してください。

レポート マネージャーの個別の web.config はなくなりましたが、ポータルでは reportserver エンドポイントと同じ設定が継承されます。

## <a name="machine-keys"></a>コンピューター キー

認証 Cookie の復号化を必要とするフォーム認証の場合、両方のプロセスを同じコンピューター キーと復号化アルゴリズムで構成する必要があります。 これは、以前 Reporting Services をスケールアウト環境で動作するようにセットアップしたユーザーには馴染みのある手順でしたが、単一コンピューターに配置する場合でも必要になりました。

配置では特定の検証キーを使用する必要があります。インターネット インフォメーション サービス マネージャー (IIS) のような、キーを生成するためのツールはいくつかあります。 その他のツールはインターネットで見つけることができます。

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 以降

**\ReportServer\rsReportServer.config**

`<configuration>` の下に追加します。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

`<system.web>` の下に追加します。
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

`<configuration>` の下に追加します。

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI レポート サーバー

これは、2017 年 6 月 (ビルド 14.0.600.301) リリースの時点で使用可能な内容です。

**\ReportServer\rsReportServer.config**

`<configuration>` の下に追加します。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>パススルー Cookie を構成する

新しいポータルと reportserver は、いくつかの操作で内部 SOAP API を使用して通信を行います (以前のバージョンのレポート マネージャーに似ています)。 ポータルからサーバーに追加の Cookies を渡す必要がある場合は、PassThroughCookies プロパティを引き続き使用できます。 詳細については、「[カスタム認証クッキーを送信するように Web ポータルを構成する](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)」を参照してください。

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>次の手順

[レポート サーバーでカスタム認証またはフォーム認証を構成する](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[カスタム認証クッキーを送信するようにレポート マネージャーを構成する](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
