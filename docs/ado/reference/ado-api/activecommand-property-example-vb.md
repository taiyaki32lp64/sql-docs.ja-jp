---
title: ActiveCommand プロパティの例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d97f655c89c07f7866fbdee6aab236f942b5499c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921688"
---
# <a name="activecommand-property-example-vb"></a>ActiveCommand プロパティの例 (VB)
この例では、 [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)プロパティ。  
  
 サブルーチンを指定、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト**ActiveCommand**コマンド テキストと作成パラメーターを表示するプロパティが使用される、**レコード セット**します。  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 **ActiveCommandXprint**ルーチンがのみ与え、**レコード セット**オブジェクト、まだコマンド テキストと作成パラメーターを印刷する必要があります、**レコード セット**します。 これ行うため、 **Recordset**オブジェクトの**ActiveCommand**プロパティと関連付けられている[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。  
  
 **コマンド**オブジェクトの[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティを作成したパラメーター化されたコマンドの生成、 **Recordset**します。 **コマンド**オブジェクトの[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクションには、コマンドのパラメーターのプレース ホルダーの代わりに使用された値が得られます (" **?** ")。  
  
 最後に、エラー メッセージまたは作成者の名前と ID が出力されます。  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>関連項目  
 [ActiveCommand プロパティ (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [コマンド オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
