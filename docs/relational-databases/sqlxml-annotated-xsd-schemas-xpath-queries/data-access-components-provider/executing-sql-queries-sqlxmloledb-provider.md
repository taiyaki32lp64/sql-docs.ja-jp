---
title: SQL クエリの実行 (SQLXMLOLEDB プロバイダー)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f716d9e682c3b98fe35ea80dd4b630486d7e836
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257320"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>SQL クエリの実行 (SQLXMLOLEDB プロバイダー)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  この例では、次の SQLXMLOLEDB プロバイダー固有のプロパティの使用方法を示します。  
  
-   ClientSideXML  
  
-   xml root  
  
 このクライアント側の ADO サンプル アプリケーションでは、クライアントで単純な SQL クエリを実行します。 ClientSideXML プロパティが True に設定されているため、FOR XML 句を指定せずに SELECT ステートメントがサーバーに送信されます。 サーバーではクエリが実行され、クライアントに行セットが返されます。 次にクライアントではその行セットに FOR XML 変換が適用され、XML ドキュメントが作成されます。  
  
 Xml ルートプロパティは、生成される XML ドキュメントの最上位レベルのルート要素を1つ提供します。  
  
> [!NOTE]  
>  コードでは、接続文字列に Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。 また、この例ではデータ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) を使用するよう指定していますが、これには追加ネットワーク クライアントがインストールされていることが必要です。 詳細については、「 [SQL Server Native Client のシステム要件](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)」を参照してください。  
  
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
  
  
