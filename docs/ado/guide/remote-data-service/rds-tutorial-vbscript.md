---
title: RDS のチュートリアル (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d45347bcdf212158fb6a0ee9f4599e1e1b00ff54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922425"
---
# <a name="rds-tutorial-vbscript"></a>RDS のチュートリアル (VBScript)
これは、RDS チュートリアルでは、Microsoft Visual Basic Scripting Edition で書き込まれます。 このチュートリアルの目的については、次を参照してください。、 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 このチュートリアルで[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)と[rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)作成はデザイン時にで定義される次のように、オブジェクト タグ:`<OBJECT>...</OBJECT>`します。 または、実行時に作成する可能性があります、 [CreateObject メソッド (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)メソッド。 たとえば、 **rds.DataControl**このようなオブジェクトを作成できます。  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>手順 1 - サーバー プログラムを指定します。  
 VBScript は、VBScript にアクセスすることで実行されている IIS Web サーバーの名前を検出できる**Request.ServerVariables** Active Server Pages を使用できるメソッド。  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 ただし、このチュートリアルでは、虚数部のサーバーでは、「通常」を使用します。  
  
> [!NOTE]
>  データ型に注意を払う**ByRef**引数。 VBScript では常に渡す必要がありますので、変数の型を指定することはできません、**バリアント**します。 RDS がすると、バリアントをでを起動する場合は、非バリアント型を受け取るメソッドに渡すことが HTTP を使用する場合、 **rds.DataSpace**オブジェクト[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)メソッド。 DCOM や、プロセスでサーバーを使用する場合はクライアントとサーバー側でパラメーターの型と一致する必要があります。 または「型の不一致」エラーが表示されます。  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>手順 2 a - RDS に関するサーバー プログラムを呼び出すDataControl  
 この例を示すコメントだけでは、既定の動作、 **rds.DataControl**指定されたクエリを実行することです。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>手順 2 b - RDSServer.DataFactory とサーバー プログラムを呼び出す  
  
## <a name="step-3---server-obtains-a-recordset"></a>手順 3 - サーバーは、レコード セットを取得します。  
  
## <a name="step-4---server-returns-the-recordset"></a>手順 4 - サーバーをレコード セットを返します。  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>手順 5: DataControl がビジュアル コントロールで使用可能な作成します。  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>手順 6 - 変更は、RDS に関するサーバーに送信されますDataControl  
 この例は、単なるコメントを示す方法、 **rds.DataControl**更新プログラムを実行します。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>手順 6 - 変更 RDSServer.DataFactory でサーバーに送信されます  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **これは、チュートリアルの最後です。**  
  
## <a name="see-also"></a>参照  
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
