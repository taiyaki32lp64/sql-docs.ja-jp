---
title: Commands という |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO]
ms.assetid: 5a0ec8f9-5ba3-4f9f-b80d-2073aa049586
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 928ac3b1d3cd753ded0bcf4337f10a654c9a3dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924823"
---
# <a name="named-commands"></a>名前付きコマンド
[作成して、単純なコマンドを実行する](../../../ado/guide/data/creating-and-executing-a-simple-command.md)コマンドを実行する方法を示しています。 別の方法がある: ことを名前付きコマンドと、名前付きコマンドで直接これを呼び出すことができます、**接続**オブジェクト (に割り当てられている、 **ActiveConnection**のプロパティ、 **コマンド**オブジェクト)。 名前を割り当てることを意味コマンドの名前を付け、**名前**のプロパティを**コマンド**オブジェクト。 例を次に示します。  
  
```  
objCmd.Name = "GetCustomers"  
objCmd.ActiveConnection = objConn  
objConn.GetCustomers objRs  
```  
  
 名前付きコマンドの"カスタム"メソッドの場合と同様の機能、**接続**オブジェクト。 コマンドの結果は、この「カスタム メソッド」の出力パラメーターとして返されます。  
  
 次の例では、この機能を説明します。  
  
```  
'BeginNamedCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
  
    objCmd.CommandText = "SELECT CustomerID, CompanyName FROM Customers"  
    objCmd.CommandType = adCmdText  
  
    'Name the command.  
    objCmd.Name = "GetCustomers"  
  
    objCmd.ActiveConnection = objConn  
  
    ' Execute using Command.Name from the Connection.  
    objConn.GetCustomers objRs  
  
    ' Display.  
    Do While Not objRs.EOF  
        Debug.Print objRs(0) & vbTab & objRs(1)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndNamedCmd  
```  
  
## <a name="see-also"></a>関連項目  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
