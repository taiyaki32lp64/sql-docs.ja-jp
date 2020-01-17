---
title: ReportViewer コントロール 2016 でのデータ収集
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: 2372adbf0fd0b9ad15383d6538d25ef955b27426
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923800"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>ReportViewer コントロールを使用した Reporting Services の統合 - データ収集

顧客が製品をどのように使用しているかを理解するために、匿名の利用状況データがコントロールによって収集されます。 使用状況データを使用して、今後の開発で顧客に最も関係のある機能強化に注力できます。

Microsoft SQL Server と Report Viewer でのデータ収集と使用方法については、[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)をご覧ください。

## <a name="opting-out-of-data-collection"></a>データ収集のオプトアウト

使用状況データの収集は、```EnableTelemetry``` プロパティを使用して無効にすることができます。

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

または、コントロールがレンダリングされる前にプログラムで無効にできます。
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>参照

[WebForms レポート ビューアー コントロールの使用](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[レポート ビューアー コントロールを使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



