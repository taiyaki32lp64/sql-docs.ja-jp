---
title: Windows アプリケーションでの SOAP API の使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- rendered reports [Reporting Services]
- Windows applications [Reporting Services]
- Windows Forms [Reporting Services]
- SOAP [Reporting Services], Windows applications
ms.assetid: e4804792-20cd-4df2-9257-fb958ff447b4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bb34dc31d65c9b0814a348232d0e2405d7676fda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63218346"
---
# <a name="using-the-soap-api-in-a-windows-application"></a>Windows アプリケーションでの SOAP API の使用
  Reporting Services SOAP API からは、レポート サーバーのすべての機能にアクセスできます。 SOAP API は Web サービスです。したがって、SOAP API に容易にアクセスし、エンタープライズ レポート機能をカスタム ビジネス アプリケーションに取り入れることができます。 Windows アプリケーションの Web サービスにアクセスするには、サービスへの呼び出しを作成するコードを記述します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用すると、プロキシ クラスを生成して、Web サービスのプロパティとメソッドを表示し、使い慣れたインフラストラクチャとツールを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の技術に基づいたビジネス アプリケーションを構築できます。  
  
## <a name="integrating-report-management-functionality-using-windows-forms"></a>Windows フォームを使用したレポート管理機能の統合  
 SOAP API は、URL アクセスとは異なり、レポート サーバーで使用できる管理機能の完全なセットを提供します。 つまり、SOAP を使用すれば、開発者はレポート マネージャーのすべての管理機能を利用することができます。 したがって、Windows フォームを使用して完全な管理ツールを開発できます。 たとえば、Windows アプリケーションにおいて、レポート サーバー名前空間のコンテンツをユーザーが取得できるようにするとします。 そのためには、Web サービス <xref:ReportService2010.ReportingService2010.ListChildren%2A> メソッドを使用してレポート サーバー データベースの全アイテムを一覧表示した後、Listview、Treeview、または Combobox コントロールを使用してアイテムをユーザーに表示します。 次の Web サービス コードを使用した場合、ユーザーがフォームのボタンをクリックすると、ユーザーの [個人用レポート] フォルダー内にある使用可能なレポートの現在の一覧を取得できます。  
  
```vb  
' Button click event that retrieves a list of reports from  
' the My Reports folder and displays them in a combo box  
Private Sub listReportsButton_Click(sender As Object, e As System.EventArgs)  
   ' Create a new Web service object and set credentials  
   ' to Windows Authentication  
   Dim rs As New ReportingService2010()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return the list of items in My Reports  
   Dim items As CatalogItem() = rs.ListChildren("/Adventureworks 2008 Sample Reports", False)  
  
   Dim ci As CatalogItem  
   For Each ci In  items  
      ' If the item is a report, add it to   
      ' a combo box  
      If ci.TypeName = "Report" Then  
         catalogComboBox.Items.Add(ci.Name)  
      End If  
   Next ci  
End Sub 'listReportsButton_Click  
```  
  
```csharp  
// Button click event that retrieves a list of reports from  
// the My Reports folder and displays them in a combo box  
private void listReportsButton_Click(object sender, System.EventArgs e)  
{  
   // Create a new Web service object and set credentials  
   // to Windows Authentication  
   ReportingService2010 rs = new ReportingService2010();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return the list of items in My Reports  
   CatalogItem[] items = rs.ListChildren("/Adventureworks 2008 Sample Reports", false);  
  
   foreach (CatalogItem ci in items)  
   {  
      // If the item is a report, add it to   
      // a combo box  
      if (ci.TypeName == "Report")  
         catalogComboBox.Items.Add(ci.Name);  
   }  
}  
```  
  
 その後で、ユーザーがコンボ ボックスからレポートを選択し、Web ブラウザー コントロールまたは画像コントロールを使用してフォームのレポートをプレビューできるようにします。  
  
## <a name="enabling-report-viewing-and-navigation-using-windows-forms"></a>Windows フォームを使用したレポートの表示とナビゲーション  
 レポートを Windows フォーム アプリケーションに統合する場合に使用できるメソッドは、2 つあります。  
  
 SOAP API を使用してサポートされている表示形式でレポートを表示するには、<xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドを使用します。 SOAP を使用してレポートの表示とナビゲーションを有効化する方法には、次のようなわずかな欠点があります。  
  
-   URL アクセスによる HTML ビューアーで使用できるレポート ツール バーの組み込み機能を利用できません。  
  
-   HTML で表示する場合は、<xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> メソッドを使用して画像やリソースを追加ストリームとして個別に表示する必要があります。  
  
-   URL アクセスによってレポートを表示した場合、SOAP API を使用する場合よりもパフォーマンスが多少向上します。  
  
 ただし、SOAP API の <xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドを使用すると、プログラムによってさまざまな出力形式でレポートを表示および保存できます。 これは、ユーザーとの対話を必要とする URL アクセスよりも優れた点です。 SOAP API の <xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドを使用してレポートを表示すると、サポートされている出力形式のいずれでも表示できます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] に含まれている配信可能な ReportViewer コントロールも自由に使用できます。 ReportViewer コントロールでは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能をカスタム アプリケーションに容易に埋め込むことができます。 ReportViewer コントロールは、事前にデザインして完全な形にしあげたレポートを、アプリケーションの機能セットの一部として提供することを予定している開発者を対象にしています (たとえば、Web サイト管理アプリケーションであれば、企業の Web サイトに関するクリックストリーム分析を表示するレポートなどが考えられます)。 これらのコントロールをアプリケーションに埋め込む方法は、アプリケーションの配置に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバー コンポーネントを組み込む方法を簡略化したものと言えます。 これらのコントロールではレポート機能が提供されますが、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に含まれる他の機能 (レポートの作成、パブリッシュ、配布、配信のためのサポート) はありません。  
  
 ReportViewer コントロールには 2 つのバージョンがあります。1 つは Windows リッチ クライアント アプリケーション、もう 1 つは [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションを対象にしています。 また、これらのコントロールは、ローカル処理モードとリモート処理モードの両方をサポートしています。 ローカル処理モードの場合は、アプリケーションによってレポートの定義とデータセットを提供し、レポートの処理を起動します。 リモート処理モードの場合は、データの取得とレポートの処理をレポート サーバー側で実行し、これらのコントロールをレポートの表示とナビゲーションのために使用します。 このモデルを使用すれば、デスクトップの規模にもエンタープライズの規模にも対応できるスケーラビリティの高いリッチ アプリケーションを作成できます。  
  
 ReportViewer コントロールの説明は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のオンライン ヘルプにあります。 詳細については、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の製品ドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [アプリケーションへの Reporting Services の統合](../application-integration/integrating-reporting-services-into-applications.md)   
 [Web アプリケーションでの SOAP API の使用](integrating-reporting-services-using-soap-web-application.md)  
  
  
