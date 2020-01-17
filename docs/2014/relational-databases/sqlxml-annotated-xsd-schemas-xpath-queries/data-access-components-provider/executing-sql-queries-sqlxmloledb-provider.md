---
title: SQL クエリ (SQLXMLOLEDB プロバイダー) の実行 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 029ba9e05a422648d75487e85f367b3b4f698ebd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013175"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>SQL クエリの実行 (SQLXMLOLEDB プロバイダー)
  この例では、次の SQLXMLOLEDB プロバイダー固有のプロパティの使用を示します。  
  
-   ClientSideXML  
  
-   xml root  
  
 このクライアント側の ADO サンプル アプリケーションでは、クライアントで単純な SQL クエリを実行します。 ClientSideXML プロパティが True に設定されているために、FOR XML 句のない SELECT ステートメントは、サーバーに送信されます。 サーバーではクエリが実行され、クライアントに行セットが返されます。 次にクライアントではその行セットに FOR XML 変換が適用され、XML ドキュメントが作成されます。  
  
 Xml ルート プロパティは、生成される XML ドキュメントの 1 つの最上位ルート要素を提供します。  
  
> [!NOTE]  
>  コードでは、接続文字列に Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。 また、この例ではデータ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) を使用するよう指定していますが、これには追加ネットワーク クライアントがインストールされていることが必要です。 詳細については、次を参照してください。 [SQL Server Native Client のシステム要件](../../native-client/system-requirements-for-sql-server-native-client.md)します。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
