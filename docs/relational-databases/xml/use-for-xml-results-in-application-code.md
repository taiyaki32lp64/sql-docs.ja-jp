---
title: アプリケーション コードでの FOR XML の結果の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 754b7a4baaff71cf0abe7193e5ba9c9cbd0a943a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039184"
---
# <a name="use-for-xml-results-in-application-code"></a>アプリケーション コードでの FOR XML の結果の使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  SQL クエリで FOR XML 句を使用することにより、クエリの結果を XML データで取得したり、XML データにキャストすることができます。 この機能により、FOR XML のクエリの結果を XML アプリケーション コードで使用するときに、次のことが可能になります。  
  
-   [XML Data &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md) 値のインスタンスの SQL テーブルにクエリを実行する  
  
-   text 型や image 型のデータが含まれているクエリ結果を XML として返すために [FOR XML クエリの TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md)を適用する  
  
 このトピックでは、これらの方法を示す例を提供します。  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>ADO と XML データ アイランドによる、FOR XML データの取得  
 FOR XML クエリで作業を行っているときに、ADO **Stream** オブジェクト、または ASP (Active Server Page) **Request** オブジェクトや **Response** オブジェクトなどの、COM **IStream** インターフェイスをサポートする他のオブジェクトを使用して、結果を含めることができます。  
  
 たとえば、次の ASP コードは、AdventureWorks サンプル データベースの Sales.Store テーブルにある、 **xml** データ型の列である Demographics のクエリ結果を示しています。 具体的には、クエリは CustomerID が 3 の行で、この列のインスタンス値を検索します。  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
   Response.write "Connect String = " & sConn & "<BR/>"  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
   adoConn.Open  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
   Response.write "Query String = " & sQuery & "<BR/>"  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
%>  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
</SCRIPT>  
</HEAD>  
<BODY>  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
```  
  
 この例の ASP ページには、ADO を使用して FOR XML クエリを実行し、XML データ アイランドの MyDataIsle に XML の結果を返す、サーバー側の VBScript が含まれています。 次に、クライアント側の追加処理用に、この XML データ アイランドがブラウザーに返されます。 その後、クライアント側の追加の VBScript コードを使用して、XML データ アイランドのコンテンツが処理されます。 この処理が実行されてから、結果の DHTML の一部としてコンテンツを表示し、メッセージ ボックスを開いて XML データ アイランドの前処理されたコンテンツを示します。  
  
#### <a name="to-test-this-example"></a>この例をテストするには  
  
1.  IIS がインストールされ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の AdventureWorks サンプル データベースがインストールされていることを確認します。  
  
     この例では、IIS (インターネット インフォメーション サービス) Version 5.0 以降がインストールされていて、ASP のサポートが有効になっている必要があります。 また、AdventureWorks サンプル データベースがインストールされている必要があります。  
  
2.  前述のコード例をコピーし、XML エディターまたはテキスト エディターに貼り付けます。 ファイルに RetrieveResults.asp という名前を付けて、IIS で使用されているルート ディレクトリに保存します。 通常、ルート ディレクトリは C:\Inetpub\wwwroot です。  
  
3.  次の URL を使用して、ブラウザー ウィンドウで ASP ページを開きます。 まず、"MyServer" を "localhost" または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と IIS がインストールされている実際のサーバー名に置き換えます。  
  
    ```  
    https://MyServer/RetrieveResults.asp  
    ```  
  
 表示される生成後の HTML ページの結果は、次のサンプル出力のようになります。  
  
##### <a name="server-side-processing"></a>サーバー側の処理  
 Page Generated \@ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI;  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 Pushing XML to client for processing  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>XML ドキュメント MyDataIsle のクライアント側の処理  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 次に、VBScript メッセージ ボックスに、元のフィルター処理されていない XML データ アイランドのコンテンツが次のように表示されます。これは、FOR XML のクエリ結果によって返されたデータです。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>ASP.NET と .NET Framework を使用した、FOR XML データの取得  
 前述の例と同様に、次の ASP.NET コードは、AdventureWorks サンプル データベースの Sales.Store テーブルにある、 **xml** データ型の列である Demographics のクエリ結果を示しています。 前述の例と同様に、クエリは CustomerID が 3 の行で、この列のインスタンス値を検索します。  
  
 この例では、FOR XML のクエリ結果を返して表示するために、次の Microsoft .NET Framework マネージド API が使用されています。  
  
1.  指定した接続文字列変数 strConn の内容に基づいて SQL Server への接続を開くために、**SqlConnection** が使用されます。  
  
2.  次に、データ アダプターとして**SqlDataAdapter** が使用されます。また、FOR XML クエリを実行するために、SQL 接続および指定した SQL クエリ文字列を使用します。  
  
3.  クエリの実行後、 **SqlDataAdapter.Fill** メソッドが呼び出され、FOR XML クエリの出力をデータセットに設定するために、 **DataSet** のインスタンスである MyDataSet が渡されます。  
  
4.  その後、サーバーで生成される HTML ページに表示可能な文字列としてクエリ結果を返すために、 **DataSet.GetXml** メソッドが呼び出されます。  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
    <TITLE>FOR XML Query Example</TITLE>  
    <STYLE>  
       BODY  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
       H3  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
    </STYLE>  
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>この例をテストするには  
  
1.  IIS がインストールされ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の AdventureWorks サンプル データベースがインストールされていることを確認します。  
  
     この例では、IIS (インターネット インフォメーション サービス) Version 5.0 以降がインストールされていて、ASP.NET のサポートが有効になっている必要があります。 また、AdventureWorks サンプル データベースがインストールされている必要があります。  
  
2.  前述のコードをコピーし、XML エディターまたはテキスト エディターに貼り付けます。 ファイルに RetrieveResults.aspx という名前を付けて、IIS で使用されているルート ディレクトリに保存します。 通常、ルート ディレクトリは C:\Inetpub\wwwroot です。  
  
3.  次の URL を使用して、ブラウザー ウィンドウで ASP.NET ページを開きます。 まず、"MyServer" を "localhost" または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と IIS がインストールされている実際のサーバー名に置き換えます。  
  
    ```  
    https://MyServer/RetrieveResults.aspx  
    ```  
  
 表示される生成後の HTML ページの結果は、次のサンプル出力のようになります。  
  
##### <a name="server-side-processing"></a>サーバー側の処理  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] による **xml** データ型のサポートにより、[TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md)を指定することで、FOR XML クエリの結果を、string データ型または image データ型ではなく、**xml** データ型で返すように要求できます。 FOR XML クエリに TYPE ディレクティブを使用すると、「[アプリケーションでの XML データの使用](../../relational-databases/xml/use-xml-data-in-applications.md)」で示したのと同様に、プログラムから FOR XML の結果にアクセスできます。  
  
## <a name="see-also"></a>参照  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
