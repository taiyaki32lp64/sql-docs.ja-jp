---
title: ストリームに結果セットを取得する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f0c76a668c7191467e9f66ba48c486aceea16df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924346"
---
# <a name="retrieving-resultsets-into-streams"></a>ストリーム形式で結果セットを取得する
従来の結果を受信するのではなく**Recordset**オブジェクト、ADO は代わりに、ストリームにクエリ結果を取得します。 ADO **Stream**オブジェクト (またはその他のオブジェクト、COM をサポートする**IStream** 、ASP などのインターフェイス**要求**と**応答**オブジェクト) これらの結果を含めるために使用できます。 この機能の 1 つの用途では、XML 形式で結果を取得します。 SQL Server では、たとえば、XML できます結果 SQL SELECT クエリで FOR XML 句を使用して、XPath クエリの使用など、複数の方法で。  
  
 ストリームの形式ではなくクエリ結果を受信する、**レコード セット**を指定する必要があります、 **adExecuteStream**から定数**ExecuteOptionEnum**のパラメーターとして、**Execute**のメソッド、**コマンド**オブジェクト。 ご利用のプロバイダーは、この機能をサポートする場合は実行時にストリームの結果が返されます。 コードが実行される前に、追加のプロバイダー固有のプロパティを指定する必要があります。 など、Microsoft OLE DB Provider for SQL Server などのプロパティで**出力 Stream**で、**プロパティ**のコレクション、**コマンド**オブジェクトである必要があります指定します。 この機能に関連する SQL Server に固有の動的プロパティの詳細については、SQL Server Books Online の XML-Related プロパティを参照してください。  
  
## <a name="for-xml-query-example"></a>FOR XML クエリの例  
 次の例は、VBScript に Northwind データベースに書き込まれます。  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
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
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
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
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
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
  
 FOR XML 句には、SQL Server XML ドキュメントの形式でデータを返すように指示します。  
  
### <a name="for-xml-syntax"></a>XML 構文について  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 生の XML を属性として列の値を持つジェネリック行要素を生成します。 FOR XML AUTO は、テーブル名に基づいて、要素名を持つ階層ツリーを生成するのにヒューリスティックを使用します。 FOR XML EXPLICIT には、メタデータで完全に記述するリレーションシップのユニバーサル テーブルを生成します。  
  
 SQL SELECT FOR XML ステートメントの例を次に示します。  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 コマンドは、前述のように割り当てられた文字列で指定できる**CommandText**、またはに割り当てられている XML テンプレートのクエリの形式で**CommandStream**します。 XML テンプレートのクエリの詳細については、次を参照してください。[コマンド ストリーム](../../../ado/guide/data/command-streams.md)ADO または、SQL Server Books Online でのコマンドの入力を使用するストリーム。  
  
 XML テンプレートのクエリとして、FOR XML クエリは次のようです。  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 この例では、ASP を指定します。**応答**オブジェクト、**出力 Stream**プロパティ。  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 次に、指定**adExecuteStream**パラメーターの**Execute**します。 この例は、XML データ アイランドを作成する XML タグ内のストリームをラップします。  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>コメント  
 この時点では、XML がクライアント ブラウザーにストリームされ、表示できる状態になります。 これは、XML ドキュメントを HTML 内の製品の一覧を作成する DOM とそれぞれの子ノードのループのインスタンスにバインドするクライアント側の VBScript を使用して行います。
