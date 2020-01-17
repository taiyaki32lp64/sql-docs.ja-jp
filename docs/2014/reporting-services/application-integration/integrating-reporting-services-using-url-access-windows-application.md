---
title: Windows アプリケーションでの URL アクセスの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Windows applications [Reporting Services]
- Web Browser controls [Reporting Services]
- Windows Forms [Reporting Services]
- browser controls [Reporting Services]
- URL access [Reporting Services], Windows applications
ms.assetid: a4b222e5-0cbd-409c-92c4-046a674db8ac
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cb841d187385724ea31b5a7db86fcb323bf10663
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126242"
---
# <a name="using-url-access-in-a-windows-application"></a>Windows アプリケーションでの URL アクセスの使用
  レポート サーバーへの URL アクセスは Web 環境用に最適化されていますが、URL アクセスを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートを [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーションに埋め込むこともできます。 ただし、Windows フォームに関連する URL アクセスでは、Web ブラウザー テクノロジを使用する必要があります。 URL アクセスと Windows フォームでは、次の統合シナリオを使用できます。  
  
-   プログラムで Web ブラウザーを起動し、Windows フォーム アプリケーションからレポートを表示します。  
  
-   Windows フォームで <xref:System.Windows.Forms.WebBrowser> コントロールを使用し、レポートを表示します。  
  
## <a name="starting-internet-explorer-from-a-windows-form"></a>Windows フォームからの Internet Explorer の起動  
 <xref:System.Diagnostics.Process> クラスを使用して、コンピューターで実行されているプロセスにアクセスできます。 <xref:System.Diagnostics.Process> クラスは、アプリケーションの起動、停止、制御、および監視に役立つ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の構成要素です。 レポート サーバー データベースの特定のレポートを表示するには、レポートへの URL を渡して **IExplore** プロセスを起動できます。 次のコード例を使用すると、ユーザーが Windows フォームのボタンをクリックしたときに [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer が起動し、特定のレポート URL を渡すことができます。  
  
```vb  
Private Sub viewReportButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles viewReportButton.Click  
   ' Build the URL access string based on values supplied by a user  
   Dim url As String = serverUrlTextBox.Text + "?" & reportPathTextBox.Text & _  
   "&rs:Command=Render" & "&rs:Format=HTML4.0"  
  
   ' If the user does not select the toolbar check box,  
   ' turn the toolbar off in the HTML Viewer  
   If toolbarCheckBox.Checked = False Then  
      url += "&rc:Toolbar=False"  
   End If  
   ' load report in the Web browser  
   Try  
      System.Diagnostics.Process.Start("IExplore", url)  
   Catch  
      MessageBox.Show("The system could not start the specified report using Internet Explorer.", _  
      "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error)  
   End Try  
End Sub 'viewReportButton_Click  
```  
  
```csharp  
// Sample click event for a Button control on a Windows Form  
private void viewReportButton_Click(object sender, System.EventArgs e)  
{  
   // Build the URL access string based on values supplied by a user  
   string url = serverUrlTextBox.Text + "?" + reportPathTextBox.Text +  
      "&rs:Command=Render" + "&rs:Format=HTML4.0";  
  
   // If the user does not check the toolbar check box,  
   // turn the toolbar off in the HTML Viewer  
   if (toolbarCheckBox.Checked == false)  
      url += "&rc:Toolbar=False";  
  
   // load report in the Web browser  
   try  
   {  
      System.Diagnostics.Process.Start("IExplore", url);  
   }  
  
   catch (Exception)  
   {  
      MessageBox.Show(  
         "The system could not open the specified report using Internet Explorer.",   
         "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error);  
   }  
}  
```  
  
## <a name="embedding-a-browser-control-on-a-windows-form"></a>Windows フォームへのブラウザー コントロールの埋め込み  
 外部 Web ブラウザーでレポートを表示したくない場合は、<xref:System.Windows.Forms.WebBrowser> コントロールを使用して、Windows フォームの一部としてシームレスに Web ブラウザーを埋め込むことができます。  
  
###### <a name="to-add-the-webbrowser-control-to-your-windows-form"></a>Windows フォームに WebBrowser コントロールを追加するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] で新しい Windows アプリケーションを作成します。  
  
2.  **[ツールボックス]** ダイアログ ボックスで <xref:System.Windows.Forms.WebBrowser> コントロールを探します。  
  
     **ツールボックス**が表示されていない場合は、 **[表示]** メニュー項目をクリックして **[ツールボックス]** を選択することでアクセスできます。  
  
3.  <xref:System.Windows.Forms.WebBrowser> コントロールを Windows フォームのデザイン画面にドラッグします。  
  
     webBrowser1 という <xref:System.Windows.Forms.WebBrowser> コントロールがフォームに追加されます。  
  
 <xref:System.Windows.Forms.WebBrowser> コントロールを URL に指定するには、その **Navigate** メソッドを呼び出します。 次の例に示すように、実行時に特定の URL アクセス文字列を <xref:System.Windows.Forms.WebBrowser> コントロールに割り当てることができます。  
  
```vb  
Dim url As String = "http://localhost/reportserver?/" & _  
                    "AdventureWorks2012 Sample Reports/" & _  
                    "Company Sales&rs:Command=Render"  
WebBrowser1.Navigate(url)  
```  
  
```csharp  
string url = "http://localhost/reportserver?/" +  
             "AdventureWorks2012 Sample Reports/" +  
             "Company Sales&rs:Command=Render";  
webBrowser1.Navigate(url);  
```  
  
## <a name="see-also"></a>参照  
 [アプリケーションへの Reporting Services の統合](../application-integration/integrating-reporting-services-into-applications.md)   
 [URL アクセスを使用した Reporting Services の統合](integrating-reporting-services-using-url-access.md)   
 [SOAP を使用した Reporting Services の統合](integrating-reporting-services-using-soap.md)   
 [ReportViewer コントロールを使用した Reporting Services の統合](integrating-reporting-services-using-reportviewer-controls.md)   
 [URL アクセス &#40;SSRS&#41;](../url-access-ssrs.md)  
  
  
