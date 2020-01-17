---
title: XSL 変換の適用 (SQLXMLOLEDB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3040c337853a33748fe24a72892739664f8e8304
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246620"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>XSL 変換の適用 (SQLXMLOLEDB プロバイダー)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このサンプル ADO アプリケーションでは、SQL クエリが実行され、結果に XSL 変換が適用されます。 ClientSideXML プロパティを True に設定すると、クライアント側で行セットの処理が強制されます。 SQL クエリをテンプレートで指定する場合は、テンプレート実行時にコマンド言語を指定する必要があるため、コマンド言語 {5d531cb2-e6ed-11d2-b252-00c04f681b71} を設定します。 Xsl プロパティは、変換の適用に使用する XSL ファイルを指定します。 [基本パスプロパティの値は、XSL ファイルを検索するために使用されます。 Xsl プロパティの値にパスを指定した場合、パスは、[ベースパス] プロパティで指定したパスに対する相対パスになります。  
  
 この例では、次の SQLXMLOLEDB プロバイダー固有のプロパティについて、使用法を示します。  
  
-   ClientSideXML  
  
-   xsl  
  
 このクライアント側の ADO サンプル アプリケーションでは、SQL クエリで構成される XML テンプレートがサーバーで実行されます。  
  
 ClientSideXML プロパティが True に設定されているため、FOR XML 句を指定せずに SELECT ステートメントがサーバーに送信されます。 サーバーではクエリが実行され、クライアントに行セットが返されます。 次に、クライアントは、行セットに FOR XML 変換を適用し、XML ドキュメントを生成します。  
  
 Xsl プロパティは、アプリケーションで指定されています。そのため、クライアントで生成された XML ドキュメントに XSL 変換が適用され、結果は2列のテーブルになります。  
  
 テンプレートコマンドを実行するには、XML テンプレート言語 ({5d531cb2-e6ed-11d2-b252-00c04f681b71}) を指定する必要があります。  
  
> [!NOTE]  
>  コードでは、接続文字列に Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。 また、この例ではデータ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するよう指定していますが、これには追加ネットワーク クライアントがインストールされていることが必要です。 詳細については、「 [SQL Server Native Client のシステム要件](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)」を参照してください。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 次は XSL テンプレートです。 この XSL テンプレートを適用すると、2 列のテーブルが生成されます。  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
