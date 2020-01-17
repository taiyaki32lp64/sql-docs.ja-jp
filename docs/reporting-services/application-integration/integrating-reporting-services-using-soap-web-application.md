---
title: Reporting Services の Web アプリケーションで SOAP API の使用 |Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3d9b086f6ec5a57493c96e3a4d0462a44d9c2e3c
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492771"
---
# <a name="integrating-reporting-services-using-soap---web-application"></a>SOAP を使用した Reporting Services の統合 - Web アプリケーション
  Reporting Services SOAP API からは、レポート サーバーのすべての機能にアクセスできます。 SOAP API は Web サービスであるため、容易にアクセスし、エンタープライズ レポート機能をカスタム ビジネス アプリケーションに取り入れることができます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーションから SOAP API にアクセスするのと同じように、Web アプリケーションからレポート サーバー Web サービスにアクセスします。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用して、レポート サーバー Web サービスのプロパティとメソッドを公開するプロキシ クラスを生成できます。このクラスにより、使い慣れたインフラストラクチャとツールを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] テクノロジに基づいたビジネス アプリケーションをビルドできます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート管理機能は、Windows アプリケーションからと同様に、Web アプリケーションからも簡単にアクセスできます。 Web アプリケーションから、レポート サーバー データベースのアイテムの追加と削除、アイテム セキュリティの設定、レポート サーバー データベースのアイテムの変更、スケジューリングと配信の管理などを行うことができます。  
  
## <a name="enabling-impersonation"></a>権限借用の有効化  
 Web アプリケーションを構成する最初の手順は、Web サービス クライアントからの権限借用を有効にすることです。 権限借用により、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションは代行するクライアントの ID を使用して実行できます。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] では [!INCLUDE[msCoName](../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) を使用してユーザーを認証し、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションに認証済みトークンを渡すか、ユーザーを認証できない場合は未認証トークンを渡します。 どちらの場合も、権限借用が有効であれば、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションで受け取ったトークンの権限を借用します。 クライアントの権限借用を有効にするには、次のようにクライアント アプリケーションの Web.config ファイルを変更します。  
  
```asp.net  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  既定では、権限借用は無効になっています。  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] の権限借用の詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK のドキュメントを参照してください。  
  
## <a name="managing-the-report-server-using-soap-api"></a>SOAP API を使用したレポート サーバーの管理  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 Web アプリケーションを使用してレポート サーバーとその内容を管理することもできます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と共に含まれているレポート マネージャーは、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] と Reporting Services SOAP API を使用して完全に構築された Web アプリケーションの一例です。 レポート マネージャーのレポート管理機能はカスタム Web アプリケーションに追加できます。 たとえば、レポート サーバー データベースの利用可能なレポートの一覧を返し、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] **Listbox** コントロールに表示して、ユーザーが選択できるようにすることができます。 次のコードでは、レポート サーバー データベースに接続し、レポート サーバー データベースのアイテムの一覧を返します。 利用可能なレポートは Listbox コントロールに追加され、各レポートのパスが表示されます。  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

 Web アプリケーションを使用してレポート サーバーとその内容を管理することもできます。 Web ポータルでは、付属[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、Reporting Services の使用は通常実行タスクの大部分を管理する Web アプリケーションの例を示します。 Web ポータルのレポート管理機能はカスタム Web アプリケーションに追加できます。 たとえば、レポート サーバー データベースの利用可能なレポートの一覧を返し、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] **Listbox** コントロールに表示して、ユーザーが選択できるようにすることができます。 次のコードでは、レポート サーバー データベースに接続し、レポート サーバー データベースのアイテムの一覧を返します。 利用可能なレポートは Listbox コントロールに追加され、各レポートのパスが表示されます。  

::: moniker-end
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>参照  

 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [アプリケーションへの Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Windows アプリケーションでの SOAP API の使用](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
  
  
