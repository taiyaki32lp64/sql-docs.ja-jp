---
title: ストリームと永続性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22fbf503196c467a7816bf4e9c76151276cc6d4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924028"
---
# <a name="streams-and-persistence"></a>ストリームと永続性
[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト[保存](../../../ado/reference/ado-api/save-method.md)メソッド ストア、または*が解決しない*、**レコード セット**ファイルでは、および[を開く](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドの復元、 **Recordset**そのファイルから。  
  
 2\.7 以降、ADO を使用した、**保存**と**オープン**メソッドを永続化できる、**レコード セット**を[Stream](../../../ado/reference/ado-api/stream-object-ado.md)もオブジェクトです。 この機能は、リモート データ サービス (RDS) や Active Server Pages (ASP) を使用する場合に便利です。  
  
 ASP ページで永続化を単独で使用する方法の詳細については、ASP の現在のドキュメントを参照してください。  
  
 次に、いくつかのシナリオを示す方法**Stream**オブジェクトや永続化を使用できます。  
  
## <a name="scenario-1"></a>シナリオ 1  
 このシナリオは単に保存、 **Recordset** 、ファイルに、 **Stream**します。 別に、永続化ストリームを開きます**Recordset**します。  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>シナリオ 2  
 このシナリオが引き続き発生する、**レコード セット**に、 **Stream** XML 形式でします。 これは、後、読み取ります、 **Stream**を調べて、操作、または表示できる文字列にします。  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>シナリオ 3  
 このコード例は、ASP のコードの永続化を示しています、 **Recordset**に直接 XML として、**応答**オブジェクト。  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>シナリオ 4  
 このシナリオでは、ASP コードの内容を書き込みます。、 **Recordset**クライアント adtg 形式の形式でします。 [OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)このデータを使用して、作成、接続が切断された**Recordset**します。  
  
 RDS での新しいプロパティ[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)、 [URL](../../../ado/reference/rds-api/url-property-rds.md)、によって生成される .asp ページを指す、**レコード セット**します。 つまり、**レコード セット**オブジェクトを取得できる RDS せず、サーバー側を使用して[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクトまたはユーザーのビジネス オブジェクトを記述します。 これにより、RDS のプログラミング モデルが大幅に合理化されます。  
  
 という名前のサーバー側コード https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 クライアント側のコード:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 開発者を使用するオプションもある、 **Recordset**クライアント上のオブジェクト。  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>関連項目  
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
