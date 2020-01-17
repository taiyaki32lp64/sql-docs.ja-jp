---
title: 名前付きコマンドにパラメーターを渡す |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9799fb3f05871c16cfcd8edb5f2a50c6f7792978
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924690"
---
# <a name="passing-parameters-to-a-named-command"></a>名前付きコマンドにパラメーターを渡す
コマンドの結果がとして渡された場合と同様、*アウト*名前付きのコマンドでは、パラメーターの変数されているパラメーター化コマンドとして渡された*で*変数を名前付きコマンド。  
  
 次のコード例を持つ顧客が配置のすべての注文の取得を試みます**CustomerID** "ALKFI"は、Northwind データベースからです。 値**CustomerID**は名前付きコマンドを呼び出すときに時間時に指定します。  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 任意の出力変数の前に指定する必要がありますすべての入力パラメーターやパラメーターのデータ型と一致する必要がありますでの対応するフィールドに変換できるいることに注意してください。 次のステートメント-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -の必須の入力パラメーターであるため、一致しないデータ型のエラーが発生、**文字列**の種類のではありません、**整数**型。  
  
 次の呼び出し-  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -有効ですが、データベースにこのようなレコードが存在しないため、設定、空の結果になります。  
  
## <a name="see-also"></a>関連項目  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
