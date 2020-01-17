---
title: WebForms ReportViewer コントロールの使用 | Microsoft Docs
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
ms.assetid: 4c200f36-4012-4108-8095-370b426ccf8d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a5ea5370cbb59d5fb70fa233f3695ac77e412669
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687382"
---
# <a name="using-the-webforms-reportviewer-control"></a>WebForms ReportViewer コントロールの使用
  レポート サーバーに配置されたレポートまたはローカル ファイル システムにあるレポートを表示するには、WebForms ReportViewer コントロールを使用して Web アプリケーションにレポートを表示します。  
  
## <a name="to-use-the-reportviewer-control-in-a-web-application"></a>Web アプリケーションで ReportViewer コントロールを使用するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] を使用して、新しい [!INCLUDE[msCoName](../../includes/msconame-md.md)] ASP.NET Web サイトを作成します。  
  
     \- または -  
  
     既存の ASP.NET Web サイトを開いて新しい Web フォームを追加します。  
  
2.  **[ツールボックス]** ウィンドウの **[AJAX Extensions]** で **ScriptManager** コントロールを見つけて、Web フォームのデザイン画面にドラッグします。  
  
     **ツールボックス**が表示されていない場合は、 **[表示]** メニューの **[ツールボックス]** をクリックするとアクセスできます。  
  
3.  **[ツールボックス]** で **ReportViewer** コントロールを見つけて、デザイン画面の **ScriptManager** コントロールの下にドラッグします。  
  
     reportViewer1 という名前の **ReportViewer** コントロールがフォームに追加されます。  
  
 コントロールがフォームに追加されると、 **[ReportViewer タスク]** スマート タグが表示され、レポートの選択を求めるメッセージが表示されます。 表示するレポートがレポート サーバーに配置されている場合は、 **[レポートの選択]** ドロップダウン リストから **[\<サーバー レポート>]** を選択します。 **[\<サーバー レポート>]** オプションを選択すると、 **[レポート サーバー URL]** および **[レポートのパス]** という 2 つの追加プロパティが表示されます。 **[レポート サーバー URL]** はレポート サーバーのアドレスで、 **[レポートのパス]** は表示するレポートへの完全なパスです。  
  
 レポートをローカル モードで表示する場合は、 **[新しいレポートをデザインします]** オプションを選択してレポート デザイナーを起動するか、または既存のプロジェクトに既に含まれているレポートを選択します。 レポートを選択した後、ReportViewer コントロールの **[レポートのパス]** プロパティにレポート RDLC ファイルの名前を入力してください。 このプロパティは、 **[プロパティ]** ウィンドウの **[LocalReport]** ノードの下に表示されます。  
  
 レポートを表示するときに ReportViewer ツール バーの項目を隠すことができます。 たとえば、印刷ボタンを隠すことができます。 ツール バーの項目を非表示にするには、 **[プロパティ]** ウィンドウで次の ReportViewer プロパティを **False** に設定します。  
  
-   **ShowBackButton**  
  
-   **ShowExportControls**  
  
-   **ShowFindControls**  
  
-   **ShowPageNavigationControls**  
  
-   **ShowPrintButton**  
  
-   **ShowRefreshButton**  
  
-   **ShowZoomControl**  
  
## <a name="viewing-reports-in-remote-processing-mode"></a>リモート処理モードでのレポートの表示  
 次の例では、レポート サーバーに配置されているレポートの表示方法を示します。 この例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル レポート プロジェクトに含まれている Sales Order Detail レポートを使用します。  
  
 この例では統合 Windows 認証を使用するので、最初に権限の借用を有効にする必要があります。 これを行うには、次の行を **web.config** ファイルに挿入します。  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  既定では、権限借用は無効になっています。  

**C#**
```
protected void Page_Init(object sender, EventArgs e)  
{  
    if (!Page.IsPostBack)  
    {  
        // Set the processing mode for the ReportViewer to Remote  
        reportViewer.ProcessingMode = ProcessingMode.Remote;  
  
        ServerReport serverReport = reportViewer.ServerReport;  
  
        // Set the report server URL and report path  
        serverReport.ReportServerUrl =  
            new Uri("https://<Server Name>/reportserver");  
        serverReport.ReportPath =  
            "/AdventureWorks Sample Reports/Sales Order Detail";  
  
        // Create the sales order number report parameter  
        ReportParameter salesOrderNumber = new ReportParameter();  
        salesOrderNumber.Name = "SalesOrderNumber";  
        salesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        reportViewer.ServerReport.SetParameters(  
            new ReportParameter[] { salesOrderNumber });  
    }  
}  
```  
  
**VB.NET**
```
Imports Microsoft.Reporting.WebForms  
  
Partial Class _Default  
    Inherits System.Web.UI.Page  
  
    Protected Sub Page_Init(ByVal sender As Object, _  
            ByVal e As System.EventArgs) Handles Me.Init  
  
        If Not Page.IsPostBack Then  
  
            'Set the processing mode for the ReportViewer to Remote  
            reportViewer.ProcessingMode = ProcessingMode.Remote  
  
            Dim serverReport As ServerReport  
            serverReport = reportViewer.ServerReport  
  
            'Set the report server URL and report path  
            serverReport.ReportServerUrl = _  
                New Uri("https://<Server Name>/reportserver")  
            serverReport.ReportPath = _  
                "/AdventureWorks Sample Reports/Sales Order Detail"  
  
            'Create the sales order number report parameter  
            Dim salesOrderNumber As New ReportParameter()  
            salesOrderNumber.Name = "SalesOrderNumber"  
            salesOrderNumber.Values.Add("SO43661")  
  
            'Set the report parameters for the report  
            Dim parameters() As ReportParameter = {salesOrderNumber}  
            serverReport.SetParameters(parameters)  
  
        End If  
  
    End Sub  
  
End Class  
```  
  
## <a name="viewing-reports-in-local-processing-mode"></a>ローカル処理モードでのレポートの表示  
 次の例では、Windows アプリケーションの一部であり、レポート サーバーに配置されていないレポートの表示方法を示します。  
  
###### <a name="to-add-the-sales-order-detail-report-to-a-web-site"></a>Sales Order Detail レポートを Web サイトに追加するには  
  
1.  レポートを追加する Web サイトを開きます。  
  
2.  **[Web サイト]** メニューの **[既存項目の追加]** を選択します。  
  
3.  AdventureWorks Report Samples プロジェクトがインストールされている場所を参照します。  
  
     既定の場所は C:\Program Files\Microsoft SQL Server\100\Samples\Reporting Services\Report Samples\AdventureWorks Sample Reports です。  
  
4.  Sales Order Detail.rdl ファイルを選択して **[追加]** ボタンをクリックします。  
  
     Sales Order Detail.rdl ファイルが、プロジェクトの一部になります。  
  
5.  ソリューション エクスプローラーで Sales Order Detail.rdl ファイルを右クリックし、 **[名前の変更]** を選択します。 レポートの名前を **Sales Order Detail.rdlc** に変更し、Enter キーを押します。  
  
     ソリューション エクスプローラーが表示されていない場合は、 **[表示]** メニューの [ソリューション エクスプローラー] を選択して開くことができます。  
  
 次のコード例では、販売注文データのデータセットが作成され、Sales Order Detail レポートがローカル モードで表示されます。  

**C#**
```csharp  
protected void Page_Init(object sender, EventArgs e)  
{  
    if (!Page.IsPostBack)  
    {  
        // Set the processing mode for the ReportViewer to Local  
        reportViewer.ProcessingMode = ProcessingMode.Local;  
  
        LocalReport localReport = reportViewer.LocalReport;  
  
        localReport.ReportPath = "Sales Order Detail.rdlc";  
  
        DataSet dataset = new DataSet("Sales Order Detail");  
  
        string salesOrderNumber = "SO43661";  
  
        GetSalesOrderData(salesOrderNumber, ref dataset);  
  
        ReportDataSource dsSalesOrder = new ReportDataSource();  
        dsSalesOrder.Name = "SalesOrder";  
        dsSalesOrder.Value = dataset.Tables["SalesOrder"];  
  
        localReport.DataSources.Add(dsSalesOrder);  
  
        GetSalesOrderDetailData(salesOrderNumber, ref dataset);  
  
        ReportDataSource dsSalesOrderDetail = new ReportDataSource();  
        dsSalesOrderDetail.Name = "SalesOrderDetail";  
        dsSalesOrderDetail.Value = dataset.Tables["SalesOrderDetail"];  
  
        localReport.DataSources.Add(dsSalesOrderDetail);  
  
        // Create the sales order number report parameter  
        ReportParameter rpSalesOrderNumber = new ReportParameter();  
        rpSalesOrderNumber.Name = "SalesOrderNumber";  
        rpSalesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        localReport.SetParameters(  
            new ReportParameter[] { rpSalesOrderNumber });  
    }  
}  

private void GetSalesOrderData(string salesOrderNumber,  
                           ref DataSet dsSalesOrder)  
{  
    string sqlSalesOrder =  
        "SELECT SOH.SalesOrderNumber, S.Name AS Store, " +  
        "       SOH.OrderDate, C.FirstName AS SalesFirstName, " +  
        "       C.LastName AS SalesLastName, E.Title AS " +  
        "       SalesTitle, SOH.PurchaseOrderNumber, " +  
        "       SM.Name AS ShipMethod, BA.AddressLine1 " +  
        "       AS BillAddress1, BA.AddressLine2 AS " +  
        "       BillAddress2, BA.City AS BillCity, " +  
        "       BA.PostalCode AS BillPostalCode, BSP.Name " +  
        "       AS BillStateProvince, BCR.Name AS " +  
        "       BillCountryRegion, SA.AddressLine1 AS " +  
        "       ShipAddress1, SA.AddressLine2 AS " +  
        "       ShipAddress2, SA.City AS ShipCity, " +  
        "       SA.PostalCode AS ShipPostalCode, SSP.Name " +  
        "       AS ShipStateProvince, SCR.Name AS " +  
        "       ShipCountryRegion, CC.Phone AS CustPhone, " +  
        "       CC.FirstName AS CustFirstName, CC.LastName " +  
        "       AS CustLastName " +  
        "FROM   Person.Address SA INNER JOIN " +  
        "       Person.StateProvince SSP ON " +  
        "       SA.StateProvinceID = SSP.StateProvinceID " +  
        "       INNER JOIN Person.CountryRegion SCR ON " +  
        "       SSP.CountryRegionCode = SCR.CountryRegionCode " +  
        "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " +  
        "       LEFT OUTER JOIN  Person.Contact CC ON " +  
        "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" +  
        "       Person.Address BA INNER JOIN " +  
        "       Person.StateProvince BSP ON " +  
        "       BA.StateProvinceID = BSP.StateProvinceID " +  
        "       INNER JOIN Person.CountryRegion BCR ON " +  
        "       BSP.CountryRegionCode = " +  
        "       BCR.CountryRegionCode ON SOH.BillToAddressID " +  
        "       = BA.AddressID ON  SA.AddressID = " +  
        "       SOH.ShipToAddressID LEFT OUTER JOIN " +  
        "       Person.Contact C RIGHT OUTER JOIN " +  
        "       HumanResources.Employee E ON C.ContactID = " +  
        "       E.ContactID ON SOH.SalesPersonID = " +  
        "       E.EmployeeID LEFT OUTER JOIN " +  
        "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " +  
        "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" +  
        "        S ON SOH.CustomerID = S.CustomerID " +  
        "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)";  
  
    SqlConnection connection = new  
        SqlConnection("Data Source=(local); " +  
                      "Initial Catalog=AdventureWorks; " +  
                      "Integrated Security=SSPI");  
  
    SqlCommand command =  
        new SqlCommand(sqlSalesOrder, connection);  
  
    command.Parameters.Add(  
        new SqlParameter("SalesOrderNumber",  
        salesOrderNumber));  
  
    SqlDataAdapter salesOrderAdapter = new  
        SqlDataAdapter(command);  
  
    salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder");  
}  
  
private void GetSalesOrderDetailData(string salesOrderNumber,  
                       ref DataSet dsSalesOrder)  
{  
    string sqlSalesOrderDetail =  
        "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " +  
        "        SOD.UnitPrice, CASE WHEN " +  
        "        SOD.UnitPriceDiscount IS NULL THEN 0 " +  
        "        ELSE SOD.UnitPriceDiscount END AS " +  
        "        UnitPriceDiscount, SOD.LineTotal, " +  
        "        SOD.CarrierTrackingNumber, " +  
        "        SOD.SalesOrderID, P.Name, P.ProductNumber " +  
        "FROM    Sales.SalesOrderDetail SOD INNER JOIN " +  
        "        Production.Product P ON SOD.ProductID = " +  
        "        P.ProductID INNER JOIN " +  
        "        Sales.SalesOrderHeader SOH ON " +  
        "        SOD.SalesOrderID = SOH.SalesOrderID " +  
        "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " +  
        "ORDER BY SOD.SalesOrderDetailID";  
  
    using (SqlConnection connection = new  
        SqlConnection("Data Source=(local); " +  
                      "Initial Catalog=AdventureWorks; " +  
                      "Integrated Security=SSPI"))  
    {  
  
        SqlCommand command =  
            new SqlCommand(sqlSalesOrderDetail, connection);  
  
        command.Parameters.Add(  
            new SqlParameter("SalesOrderNumber",  
            salesOrderNumber));  
  
        SqlDataAdapter salesOrderDetailAdapter = new  
            SqlDataAdapter(command);  
  
        salesOrderDetailAdapter.Fill(dsSalesOrder,  
            "SalesOrderDetail");  
    }  
}  
```  
**VB.NET**
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.Reporting.WebForms  
  
Partial Class _Default  
    Inherits System.Web.UI.Page  
  
    Protected Sub Page_Init(ByVal sender As Object, _  
                ByVal e As System.EventArgs) Handles Me.Init  
  
        If Not Page.IsPostBack Then  
  
            'Set the processing mode for the ReportViewer to Local  
            reportViewer.ProcessingMode = ProcessingMode.Local  
  
            Dim localReport As LocalReport  
            localReport = reportViewer.LocalReport  
  
            localReport.ReportPath = "Sales Order Detail.rdlc"  
  
            Dim dataset As New DataSet("Sales Order Detail")  
  
            Dim salesOrderNumber As String = "SO43661"  
  
            'Get the sales order data  
            GetSalesOrderData(salesOrderNumber, dataset)  
  
            'Create a report data source for the sales order data  
            Dim dsSalesOrder As New ReportDataSource()  
            dsSalesOrder.Name = "SalesOrder"  
            dsSalesOrder.Value = dataset.Tables("SalesOrder")  
  
            localReport.DataSources.Add(dsSalesOrder)  
  
            'Get the sales order detail data  
            GetSalesOrderDetailData(salesOrderNumber, dataset)  
  
            'Create a report data source for the sales   
            'order detail data  
            Dim dsSalesOrderDetail As New ReportDataSource()  
            dsSalesOrderDetail.Name = "SalesOrderDetail"  
            dsSalesOrderDetail.Value = _  
                dataset.Tables("SalesOrderDetail")  
  
            localReport.DataSources.Add(dsSalesOrderDetail)  
  
            'Create a report parameter for the sales order number   
            Dim rpSalesOrderNumber As New ReportParameter()  
            rpSalesOrderNumber.Name = "SalesOrderNumber"  
            rpSalesOrderNumber.Values.Add("SO43661")  
  
            'Set the report parameters for the report  
            Dim parameters() As ReportParameter = {rpSalesOrderNumber}  
            localReport.SetParameters(parameters)  
  
        End If  
  
    End Sub  
  
    Private Sub GetSalesOrderData(ByVal salesOrderNumber As String, _  
                               ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrder As String = _  
            "SELECT SOH.SalesOrderNumber, S.Name AS Store, " & _  
            "       SOH.OrderDate, C.FirstName AS SalesFirstName, " & _  
            "       C.LastName AS SalesLastName, E.Title AS " & _  
            "       SalesTitle, SOH.PurchaseOrderNumber, " & _  
            "       SM.Name AS ShipMethod, BA.AddressLine1 " & _  
            "       AS BillAddress1, BA.AddressLine2 AS " & _  
            "       BillAddress2, BA.City AS BillCity, " & _  
            "       BA.PostalCode AS BillPostalCode, BSP.Name " & _  
            "       AS BillStateProvince, BCR.Name AS " & _  
            "       BillCountryRegion, SA.AddressLine1 AS " & _  
            "       ShipAddress1, SA.AddressLine2 AS " & _  
            "       ShipAddress2, SA.City AS ShipCity, " & _  
            "       SA.PostalCode AS ShipPostalCode, SSP.Name " & _  
            "       AS ShipStateProvince, SCR.Name AS " & _  
            "       ShipCountryRegion, CC.Phone AS CustPhone, " & _  
            "       CC.FirstName AS CustFirstName, CC.LastName " & _  
            "       AS CustLastName " & _  
            "FROM   Person.Address SA INNER JOIN " & _  
            "       Person.StateProvince SSP ON " & _  
            "       SA.StateProvinceID = SSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion SCR ON " & _  
            "       SSP.CountryRegionCode = SCR.CountryRegionCode " & _  
            "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " & _  
            "       LEFT OUTER JOIN  Person.Contact CC ON " & _  
            "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" & _  
            "       Person.Address BA INNER JOIN " & _  
            "       Person.StateProvince BSP ON " & _  
            "       BA.StateProvinceID = BSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion BCR ON " & _  
            "       BSP.CountryRegionCode = " & _  
            "       BCR.CountryRegionCode ON SOH.BillToAddressID " & _  
            "       = BA.AddressID ON  SA.AddressID = " & _  
            "       SOH.ShipToAddressID LEFT OUTER JOIN " & _  
            "       Person.Contact C RIGHT OUTER JOIN " & _  
            "       HumanResources.Employee E ON C.ContactID = " & _  
            "       E.ContactID ON SOH.SalesPersonID = " & _  
            "       E.EmployeeID LEFT OUTER JOIN " & _  
            "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " & _  
            "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" & _  
            "        S ON SOH.CustomerID = S.CustomerID " & _  
            "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrder, connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderAdapter As New SqlDataAdapter(command)  
  
            salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder")  
  
        End Using  
  
    End Sub  
  
    Private Sub GetSalesOrderDetailData( _  
                           ByVal salesOrderNumber As String, _  
                           ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrderDetail As String = _  
            "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " & _  
            "        SOD.UnitPrice, CASE WHEN " & _  
            "        SOD.UnitPriceDiscount IS NULL THEN 0 " & _  
            "        ELSE SOD.UnitPriceDiscount END AS " & _  
            "        UnitPriceDiscount, SOD.LineTotal, " & _  
            "        SOD.CarrierTrackingNumber, " & _  
            "        SOD.SalesOrderID, P.Name, P.ProductNumber " & _  
            "FROM    Sales.SalesOrderDetail SOD INNER JOIN " & _  
            "        Production.Product P ON SOD.ProductID = " & _  
            "        P.ProductID INNER JOIN " & _  
            "        Sales.SalesOrderHeader SOH ON " & _  
            "        SOD.SalesOrderID = SOH.SalesOrderID " & _  
            "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " & _  
            "ORDER BY SOD.SalesOrderDetailID"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrderDetail, _  
                                          connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderDetailAdapter As New SqlDataAdapter(command)  
  
            salesOrderDetailAdapter.Fill(dsSalesOrder, _  
                "SalesOrderDetail")  
  
        End Using  
  
    End Sub  
  
End Class  
```  
  
## <a name="see-also"></a>参照  
 [ReportViewer コントロールを使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 [ReportViewer コントロール 2016 でのデータ収集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)
  
  
