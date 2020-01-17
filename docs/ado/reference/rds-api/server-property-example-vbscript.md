---
title: サーバー プロパティの例 (VBScript) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Server property [RDS], VBScript example
ms.assetid: 0fe57af9-a4d0-4986-a2e3-beaa4d26ed58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 661734c710cbc4aa8823965e22559c519e793d41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963487"
---
# <a name="server-property-example-vbscript"></a>Server プロパティの例 (VBScript)
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 次のコードを設定する方法を示しています、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)デザインにパラメーターし、SQLOLEDB プロバイダーを使用してデータ対応のコントロールにバインドします。 標準の ASP 文書にこのコードを貼り付けしてという名前を付けます**ServerDesignVBS.asp**します。 ASP スクリプトは、サーバーで識別されます。  
  
```  
<!-- BeginServerDesignVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Server Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>Server Property Example (VBScript)</h1>  
  
<TABLE DATASRC=#RDS>  
   <TR>  
      <TD> <SPAN DATAFLD="FirstName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="LastName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Title"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Type"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Email"></SPAN> </TD>  
   </TR>  
</TABLE>  
<!-- Remote Data Service with Parameters set at Design Time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS HEIGHT=1 WIDTH=1>  
   <PARAM NAME="SQL" VALUE="Select * from Employees">  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
</OBJECT>  
  
</body>  
</html>  
<!-- EndServerDesignVBS -->  
```  
  
 次の例は、の必要なパラメーターを設定する方法を示します**rds.DataControl**実行時にします。 この例をテストする切り取りと通常 ASP ドキュメントにこのコードを貼り付けるし、名前を付けます**ServerRuntimeVBS.asp**します。 ASP スクリプトは、サーバーで識別されます。  
  
```  
<!-- BeginServerRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Server Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>Server Property Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
  
<H3>Remote Data Service Server Property Set at Run Time</H3>  
  
<!-- RDS.DataControl with no parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC HEIGHT=1 WIDTH=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <SPAN DATAFLD="FirstName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="LastName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Title"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Type"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Email"></SPAN> </TD>  
   </TR>  
</TABLE>  
  
<HR>  
<Input Size=70 Name="txtServer" Value="HTTP://<%= Request.ServerVariables("SERVER_NAME")%>">  
<BR>  
<Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
<BR>  
<Input Size=70 Name="txtSQL" Value="Select * from Employees">  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
<Script Language="VBScript">  
<!--  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
   RDC.Server = txtServer.Value  
   RDC.SQL = txtSQL.Value  
   RDC.Connect = txtConnect.Value  
   RDC.Refresh  
End Sub  
-->  
</Script>  
  
</body>  
</html>  
<!-- EndServerRuntimeVBS -->  
```  
  
## <a name="see-also"></a>関連項目  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Server プロパティ (RDS)](../../../ado/reference/rds-api/server-property-rds.md)


































