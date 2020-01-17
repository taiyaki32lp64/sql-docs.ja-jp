---
title: コマンド ストリーム |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd0c2273739a3651c7fdd4c424ce0cb47d39dd5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925845"
---
# <a name="command-streams"></a>コマンド ストリーム
ADO で指定された文字列の形式でコマンドの入力を常にサポートされている、 **CommandText**プロパティ。 代わりに、ADO 2.7 以降で使用することできますも情報のストリーム コマンドの入力のストリームを割り当てることで、 **CommandStream**プロパティ。 ADO を割り当てることができます**Stream**オブジェクト、または、COM をサポートする任意のオブジェクト**IStream**インターフェイス。  
  
 コマンド ストリームのコンテンツは、プロバイダーは、この機能を使用するためのストリームによって入力されたコマンドをサポートする必要がありますのでをプロバイダーに渡されます ADO からだけです。 たとえば、SQL Server では、XML テンプレートや TRANSACT-SQL に OpenXML の拡張機能の形式でクエリをサポートしています。  
  
 ストリームの詳細については、プロバイダーで解釈する必要があります、ため、設定して、コマンド言語を指定する必要があります、**言語**プロパティ。 値**言語**は、プロバイダーによって定義されている GUID を含む文字列です。 有効な値については**言語**プロバイダーによってサポートされている、プロバイダーのマニュアルを参照してください。  
  
## <a name="xml-template-query-example"></a>XML テンプレートのクエリ例  
 次の例は、VBScript で Northwind データベースに書き込まれます。  
  
 まず、初期化して開く、 **Stream**クエリ ストリームを格納するために使用するオブジェクト。  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 クエリのストリームの内容を XML テンプレートのクエリとなります。  
  
 テンプレートのクエリが sql で識別される XML 名前空間への参照が必要です: のプレフィックス、 \<sql:query > タグです。 SQL SELECT ステートメントは XML テンプレートのコンテンツとして含まれているし、次のように文字列変数に割り当てられています。  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 次に、文字列をストリームに書き込みます。  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery を割り当てる、 **CommandStream** ADO のプロパティ**コマンド**オブジェクト。  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 コマンド言語を指定する**言語**、SQL Server OLE DB プロバイダーがコマンド ストリームを解釈する方法を示します。 プロバイダー固有の GUID で指定された言語:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最後に、クエリを実行し、結果を返す、 **Recordset**オブジェクト。  
  
```  
Set objRS = adoCmd.Execute  
```
