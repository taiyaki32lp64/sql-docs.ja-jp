---
title: 接続オブジェクトを使用して |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f1b867e1870b81641c7cea09d9a8fb3accfcc01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923647"
---
# <a name="using-a-connection-object"></a>接続オブジェクトを使用する
開始する前に、**接続**オブジェクト、データ ソースと接続の種類に関する特定の情報を定義する必要があります。 この情報の大部分が保持している、 *ConnectionString*のパラメーター、 [Open メソッド](../../../ado/reference/ado-api/open-method-ado-connection.md)上、**接続**オブジェクト、または、 [ConnectionStringプロパティ](../../../ado/reference/ado-api/connectionstring-property-ado.md)上、**接続**オブジェクト。 接続文字列は、単一引用符で囲まれた値を使用して、セミコロンで区切られた引数と値のペアの一覧で構成されます。 例:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  接続文字列で、ODBC データ ソース名 (DSN) またはデータ リンク (UDL) ファイルを指定することもできます。 Dsn の詳細については、次を参照してください。[データ ソースを管理する](../../../odbc/admin/managing-data-sources.md)ODBC プログラマ リファレンス。 Udl の詳細については、次を参照してください。 [Data Link API の概要](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc)OLE DB プログラマーズ リファレンス。  
  
 通常、呼び出して接続を確立する、 **Connection.Open** 、適切なメソッドを*接続文字列*パラメーターとして。 例は、次の Visual Basic コード スニペットに示されます。  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 ここで**oRs.Open**は、**接続**オブジェクト (*oConn*) 変数の値としてその*ActiveConnection*パラメーター。 また、 **Connection.CursorLocation**プロパティの既定値を前提としています**adUseServer**します。 対照的にこれを[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)前のセクションで例です。 次の命令は、実行時エラーになります。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
