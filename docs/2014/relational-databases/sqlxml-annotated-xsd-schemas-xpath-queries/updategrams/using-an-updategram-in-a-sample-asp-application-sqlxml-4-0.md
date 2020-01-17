---
title: サンプル ASP アプリケーション (SQLXML 4.0) で、アップデート グラムを使用します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- ASP applications [SQLXML]
- Active Server Pages
- updategrams [SQLXML], ASP applications
ms.assetid: 10eff799-4c39-4b52-8b38-7ea6f68454a8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e209a4f6118ae9581889299c09653ebaf1cfe2cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014629"
---
# <a name="using-an-updategram-in-a-sample-asp-application-sqlxml-40"></a>サンプル ASP アプリケーションでのアップデートグラムの使用 (SQLXML 4.0)
  この ASP (Active Server Pages) アプリケーションでは、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の AdventureWorks サンプル データベースにある Person.Contact テーブル内の顧客情報を更新できます。 このアプリケーションによって次の処理が行われます。  
  
-   ユーザーに、連絡先 ID を入力するように指示する。  
  
-   入力された顧客 ID 値を使用してテンプレートを実行し、Person.Contact テーブルから連絡先に関する情報を取得する。  
  
-   取得した情報を HTML 形式で表示する。  
  
 この後、ユーザーは連絡先に関する情報を更新できますが、連絡先 ID の更新は、ContactID が主キーであるため行えません。 ユーザーが情報を送信すると、アップデートグラムが実行され、すべての form パラメーターがアップデートグラムに渡されます。  
  
 次のテンプレートは、最初のテンプレート (GetContact.xml) です。 このテンプレートを、`template` 型の仮想名が関連付けられているディレクトリに保存します。  
  
```  
<root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <sql:header>  
      <sql:param name="cid"></sql:param>  
   </sql:header>  
   <sql:query>  
      SELECT  *   
      FROM    Person.Contact  
      WHERE   ContactID=@cid   
      FOR XML AUTO  
   </sql:query>  
</root>  
```  
  
 次のテンプレートは、2 番目のテンプレート (UpdateContact.xml) です。 このテンプレートを、`template` 型の仮想名が関連付けられているディレクトリに保存します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
   <updg:param name="cid"/>  
   <updg:param name="title" />  
   <updg:param name="firstname" />  
   <updg:param name="lastname" />  
   <updg:param name="emailaddress" />  
   <updg:param name="phone" />  
</updg:header>  
<updg:sync >  
   <updg:before>  
      <Person.Contact ContactID="$cid" />   
   </updg:before>  
   <updg:after>  
      <Person.Contact ContactID="$cid"   
       Title="$title"  
       FirstName="$firstname"  
       LastName="$lastname"  
       EmailAddress="$emailaddress"  
       Phone="$phone"/>  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 次のコードは、ASP アプリケーション (SampleASP.asp) です。 このコードを、仮想ルートが関連付けられているディレクトリに保存します。仮想ルートはインターネット サービス マネージャー ユーティリティを使って作成します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用の IIS 仮想ディレクトリ管理ユーティリティは使用しません。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用の IIS 仮想ディレクトリ管理ユーティリティでは、ASP アプリケーションにアクセスしたり、このアプリケーションを識別したりできません。  
  
> [!NOTE]  
>  コードでは、"ServerName" に Microsoft インターネット インフォメーション サービス (IIS) を実行するサーバーの名前を指定する必要があります。  
  
```  
<% LANGUAGE=VBSCRIPT %>  
<%  
  Dim ContactID  
  ContactID=Request.Form("cid")  
%>  
<html>  
<body>  
<%  
  'If a ContactID value is not yet provided, display this form.  
  if ContactID="" then  
%>  
<!-- If the ContactID has not been specified, display the form that allows users to enter an ID. -->  
<form action="AdventureWorksContacts.asp" method="POST">  
<br>  
Enter ContactID: <input type=text name="cid"><br>  
<input type=submit value="Submit this ID" ><br><br>  
<-- Otherwise, if a ContactID is entered, display the second part of the form where the user can change customer information. -->  
<%  
  else  
%>  
<form name="Contacts" action="http://localhost/AdventureWorks/Template/UpdateContact.xml" method="POST">  
You may update customer information below.<br><br>  
<!-- A comment goes here to separate the parts of the application or page. -->  
<br>  
<%  
  ' Load the document in the parser and extract the values to populate the form.  
    Set objXML=Server.CreateObject("MSXML2.DomDocument")  
    ObjXML.setProperty "ServerHTTPRequest", TRUE  
  
    objXML.async=False  
    objXML.Load("http://localhost/AdventureWorks/Template/GetContact.xml?cid=" & ContactID)  
    set objCustomer=objXML.documentElement.childNodes.Item(0)  
  
  ' In retrieving data from the database, if a value in the column is NULL there  
  '  is no attribute for the corresponding element. In this case,  
  ' skip the error generation and go to the next attribute.  
  
  On Error Resume Next  
  
  Response.Write "Contact ID: <input type=text readonly=true style='background-color:silver' name=cid value="""  
  Response.Write objCustomer.attributes(0).value  
  Response.Write """><br><br>"  
  
  Response.Write "Title: <input type=text name=title value="""  
  Response.Write objCustomer.attributes(1).value  
  Response.Write """><br><br>"  
  
  Response.Write "First Name: <input type=text name=firstname value="""  
  Response.Write objCustomer.attributes(2).value  
  Response.Write """><br>"  
  
  Response.Write "Last Name: <input type=text name=lastname value="""  
  Response.Write objCustomer.attributes(3).value  
  Response.Write """><br><br>"  
  
  Response.Write "Email Address: <input type=text name=emailaddress value="""  
  Response.Write objCustomer.attributes(4).value  
  Response.Write """><br><br>"  
  
  Response.Write "Phone: <input type=text name=phone value="""  
  Response.Write objCustomer.attributes(9).value  
  Response.Write """><br><br>"  
  
  set objCustomer=Nothing  
  Set objXML=Nothing  
%>  
<input type="submit" value="Submit this change" ><br><br>  
<input type=hidden name="contenttype" value="text/xml">  
<input type=hidden name="eeid" value="<%=ContactID%>"><br><br>  
<% end if %>  
  
</form>  
</body>  
</html>  
```  
  
## <a name="see-also"></a>関連項目  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
