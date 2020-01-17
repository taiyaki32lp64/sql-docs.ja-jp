---
title: DataSpace オブジェクトおよび CreateObject メソッドの例 (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- DataSpace object [RDS], VBScript example
- CreateObject method [ADO], VBScript example
ms.assetid: 12b0e160-5e5c-441f-bed7-ac0bd061e003
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c9eb9a15094f6c08bacb9e063c707163548875a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964334"
---
# <a name="dataspace-object-and-createobject-method-example-vbscript"></a>DataSpace オブジェクトおよび CreateObject メソッドの例 (VBScript)
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 次の例は、使用する方法を示します、 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)のメソッド、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)既定ビジネス オブジェクトが、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)します。 この例をテストする切り取りし、の間には、このコードを貼り付け、\<本文 > と\</Body > の通常の HTML タグを文書化し、名前を**DataSpaceVBS.asp**します。 ASP スクリプトは、サーバーで識別されます。  
  
```  
<!-- BeginDataSpaceVBS -->  
<html>  
<head>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>DataSpace Object and CreateObject Method Example (VBScript)</title>  
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
<h1>DataSpace Object and CreateObject Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID rdsDS-->  
<OBJECT ID="rdsDS" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters set at run time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
  
<H4>Click Run -  
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates an instance of the RDSServer.DataFactory.  
The <i>Query</i> Method of the RDSServer.DataFactory is used to bring back a Recordset.</H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            "<%=Request.ServerVariables("SERVER_NAME")%>" & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
       Dim rs        
        ' Create Data Factory  
       Set rdsDF = rdsDS.CreateObject("RDSServer.DataFactory", strServer)  
        'Get Recordset    
       Set rs = rdsDF.Query(strCnxn, strSQL)     
       ' Use  RDS.DataControl to bind Recordset to data-aware Table above  
       RDS.SourceRecordset = rs  
  
    End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndDataSpaceVBS -->  
```  
  
 次の例は、使用する方法を示します、 **CreateObject** VbBusObj.VbBusObjCls、カスタム ビジネス オブジェクトのインスタンスを作成するメソッド。 また、スクリプト、Web サーバー名を識別するために、Active Server Pages を使用します。  
  
 完全な例を表示するには、サンプル アプリケーションのセレクターを開きます。 **クライアント層**列で、 **Internet Explorer で VBScript**します。 **中間層**列で、**カスタム Visual Basic のビジネス オブジェクト**します。  
  
> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。  
  
```  
Sub Window_OnLoad()  
   strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
   Set BO = ADS1.CreateObject("VbBusObj.VbBusObjCls", strServer)  
   txtConnect.Value = "dsn=Pubs;uid=MyUserID;pwd=MyPassword;"  
   txtGetRecordset.Value = "Select * From authors for Browse"  
End Sub  
```  
  
## <a name="see-also"></a>関連項目  
 [CreateObject メソッド (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)   
 [DataSpace オブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)


