---
title: Resync メソッドの例 (VB) |Microsoft Docs
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
- Resync method [ADO], Visual Basic example
ms.assetid: ab95315c-fe15-458c-9e0c-937ae5596592
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8ad898c7a02a46b12c546ae11b2387f8da0479e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917156"
---
# <a name="resync-method-example-vb"></a>Resync メソッドの例 (VB)
この例では、[再同期](../../../ado/reference/ado-api/resync-method.md)静的レコード セット内のデータを更新する方法。  
  
```  
'BeginResyncVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection strings  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'connection and recordset variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstTitles As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset using object refs to set properties  
    ' that allow for updates to the database  
    Set rstTitles = New ADODB.Recordset  
    Set rstTitles.ActiveConnection = Cnxn  
    rstTitles.CursorType = adOpenKeyset  
    rstTitles.LockType = adLockOptimistic  
  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles  
  
    'rstTitles.Open strSQLTitles, Cnxn, adOpenKeyset, adLockPessimistic, adCmdTable  
    'the above line of code passes the same refs as the object refs listed above  
  
    ' Change the type of the first title in the recordset  
    rstTitles!Type = "database"  
  
    ' Display the results of the change  
    MsgBox "Before resync: " & vbCr & vbCr & _  
        "Title - " & rstTitles!Title & vbCr & _  
        "Type - " & rstTitles!Type  
  
    ' Resync with database and redisplay results  
    rstTitles.Resync  
    MsgBox "After resync: " & vbCr & vbCr & _  
        "Title - " & rstTitles!Title & vbCr & _  
        "Type - " & rstTitles!Type  
  
    ' clean up  
    rstTitles.CancelBatch  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then  
            rstTitles.CancelBatch  
            rstTitles.Close  
        End If  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndResyncVB  
```  
  
## <a name="see-also"></a>関連項目  
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Resync メソッド](../../../ado/reference/ado-api/resync-method.md)
