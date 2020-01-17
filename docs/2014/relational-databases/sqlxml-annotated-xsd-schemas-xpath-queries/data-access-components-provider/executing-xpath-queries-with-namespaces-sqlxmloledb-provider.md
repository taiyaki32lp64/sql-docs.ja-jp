---
title: 名前空間 (SQLXMLOLEDB プロバイダー) での XPath クエリの実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing XPath queries
- namespaces property
- queries [SQLXML], SQLXMLOLEDB Provider
- XPath queries [SQLXML], namespaces
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- namespaces [SQLXML], XPath queries
ms.assetid: 024a4b7d-435d-47ba-9e80-2c2f640108f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f72c5841989eb12f89eda34fbfb310e125612d1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013079"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxmloledb-provider"></a>名前空間を使用した、XPath クエリの実行 (SQLXMLOLEDB Provider)
  XPath クエリには名前空間を使用できます。 スキーマ要素が名前空間で限定されている (対象の名前空間を含んでいる) 場合、そのスキーマに対する XPath クエリでは、この名前空間を指定する必要があります。  
  
 SQLXML 4.0 ではワイルドカード文字 (*) の使用がサポートされないため、XPath クエリは、名前空間プレフィックスを使用して指定する必要があります。 このプレフィックスを解決するには、名前空間プロパティを使用して名前空間のバインドを指定します。  
  
 XPath クエリは次の例では、ワイルドカード文字を使用して名前空間を指定します (\*) および local-name() and namespace-uri() XPath 関数。 この XPath クエリは、ローカルの名前がすべての要素を返します`Contact`と名前空間 URI が`urn:myschema:Contacts`します。  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 SQLXML 4.0 では、この XPath クエリを名前空間プレフィックスと共に指定する必要があります。 たとえば、`x:Contact` と指定します。ここで、`x` は名前空間プレフィックスです。 次の XSD スキーマについて考えてみます。  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 このスキーマでは対象の名前空間が定義されているため、このスキーマに対して "Employee" などの XPath クエリを実行するときには、クエリに名前空間を含める必要があります。  
  
 これは、上の XSD スキーマに対して XPath クエリ (x:Employee) を実行する [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic アプリケーションのサンプルです。 プレフィックスを解決するには、名前空間バインディングが名前空間プロパティを使用して指定されます。  
  
> [!NOTE]  
>  コードでは、接続文字列に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。 また、この例ではデータ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) を使用するよう指定していますが、これには追加ネットワーク クライアントがインストールされていることが必要です。 詳細については、次を参照してください。 [SQL Server Native Client のシステム要件](../../native-client/system-requirements-for-sql-server-native-client.md)します。  
  
```  
Option Explicit  
Private Sub Form_Load()  
    Dim con As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim stm As New ADODB.Stream  
    con.Open "provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
    Set cmd.ActiveConnection = con  
    stm.Open  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    cmd.Properties("Mapping schema") = "C:\DirectoryPath\con-ex.xml"  
    cmd.Properties("namespaces") = "xmlns:x='urn:myschema:Contacts'"  
    '  Debug.Print "Set Command Dialect to DBGUID_XPATH"  
    cmd.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
    cmd.CommandText = "x:Contact"  
    cmd.Execute , , adExecuteStream   
    stm.Position = 0  
    Debug.Print stm.ReadText(adReadAll)  
End Sub  
```  
  
### <a name="to-test-this-application"></a>このアプリケーションをテストするには  
  
1.  サンプルの XSD スキーマをフォルダーに保存します。  
  
2.  Visual Basic 実行可能プロジェクトを作成し、プロジェクト内にコードをコピーして、 指定されたディレクトリ パスを適切に変更します。  
  
3.  次のプロジェクト参照を追加します。  
  
    ```  
    "Microsoft ActiveX Data Objects 2.8 Library"  
    ```  
  
4.  アプリケーションを実行します。  
  
 結果の一部を次に示します。  
  
```  
<y0:Employee xmlns:y0="urn:myschema:Contacts"   
             LName="Achong" CID="1" FName="Gustavo"/>  
<y0:Employee xmlns:y0="urn:myschema:Employees"   
             LName="Abel" CID="2" FName="Catherine"/>  
```  
  
 XML ドキュメント内に生成されるプレフィックスはその都度変わりますが、マップされる名前空間は同じです。  
  
  
