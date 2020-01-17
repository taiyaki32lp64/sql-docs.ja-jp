---
title: XML レコード セットの保持シナ リオ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55ea62fac0cb2fe73b368429bb164cd28147fa7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923367"
---
# <a name="xml-recordset-persistence-scenario"></a>XML レコードセットの保持シナリオ
このシナリオでは、ASP の応答オブジェクトに直接レコード セット オブジェクトの内容を保存する Active Server Pages (ASP) アプリケーションを作成します。  
  
> [!NOTE]
>  このシナリオには、サーバーがインターネット インフォメーション サーバー 5.0 (iis) や、後でインストールされている必要があります。  
  
 Internet Explorer で表示される、返されたレコード セットを使用して、 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)します。  
  
 次の手順では、このシナリオを作成する必要があります。  
  
-   アプリケーションを設定します。  
  
-   データを取得します。  
  
-   データを送信します。  
  
-   受信して、データの表示  
  
## <a name="step-1-set-up-the-application"></a>手順 1:アプリケーションを設定します。  
 スクリプトのアクセス許可を持つ"XMLPersist"をという名前の IIS 仮想ディレクトリを作成します。 仮想ディレクトリがポイントする、1 つ名前付き"XMLResponse.asp、"、他の名前付き"Default.htm"フォルダー内の 2 つの新しいテキスト ファイルを作成します。  
  
## <a name="step-2-get-the-data"></a>手順 2:データを取得します。  
 この手順では、ADO レコード セットを開くし、クライアントに送信するための準備にコードを記述します。 メモ帳などのテキスト エディターで XMLResponse.asp ファイルを開き、次のコードを挿入します。  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 値を変更してください、`Data Source`パラメーター `strCon` Microsoft SQL Server コンピューターの名前にします。  
  
 オープンで、次の手順に進んでください、ファイルを保持します。  
  
## <a name="step-3-send-the-data"></a>手順 3:データを送信します。  
 レコード セットがある場合は、できたは、ASP の応答オブジェクトを XML として保存して、クライアントに送信する必要があります。 XMLResponse.asp の一番下には、次のコードを追加します。  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 レコード セットの変換先として指定されていますが、ASP の応答オブジェクト[Save メソッド](../../../ado/reference/ado-api/save-method.md)します。 Save メソッドの宛先は、ADO など、IStream インターフェイスをサポートする任意のオブジェクトを指定できます[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)、またはレコード セットが保存される完全なパスを含むファイル名。  
  
 保存して、次の手順に進む前に XMLResponse.asp を閉じます。 Adovbs.inc ファイルを既定 ADO ライブラリのインストール フォルダーから同じ XMLResponse.asp ファイルを保存したフォルダーにコピーします。  
  
## <a name="step-4-receive-and-display-the-data"></a>手順 4:受信して、データの表示  
 この手順では、埋め込みの HTML ファイルを作成します[DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトを指し示す XMLResponse.asp ファイルをレコード セットを取得します。 Default.htm をメモ帳などのテキスト エディターで開き、次のコードを追加します。 URL に"sqlserver"をサーバーの名前に置き換えます。  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 Default.htm ファイルを閉じて XMLResponse.asp が保存されている同じフォルダーに保存します。 Internet Explorer 4.0 を使用して、または後で、URL https:// を開いて*sqlserver*/XMLPersist/default.htm し、結果を確認します。 データは、バインドされた DHTML テーブルに表示されます。 開く URL https:// *sqlserver* /XMLPersist/XMLResponse.asp し、結果を確認します。 XML が表示されます。  
  
## <a name="see-also"></a>関連項目  
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)   
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
