---
title: Open および Close メソッドの例 (VB) |Microsoft Docs
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
- Close method [ADO], Visual Basic example
- Open method [ADO], Visual Basic example
ms.assetid: 1311d561-0e86-40f5-8cbc-ad8f13e626d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a37568f6bf4435d762d62c0475abb7d0fb8065a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917980"
---
# <a name="open-and-close-methods-example-vb"></a>Open および Close メソッドの例 (VB)
この例では、**オープン**と[閉じる](../../../ado/reference/ado-api/close-method-ado.md)両方のメソッド[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)と[接続](../../../ado/reference/ado-api/connection-object-ado.md)が開かれているオブジェクト。  
  
```  
'BeginOpenVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub OpenX()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
    Dim varDate As Variant  
  
    ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
    ' Open employee table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "employee"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Assign the first employee record's hire date  
    ' to a variable, then change the hire date  
    varDate = rstEmployees!hire_date  
    Debug.Print "Original data"  
    Debug.Print "  Name - Hire Date"  
    Debug.Print "  " & rstEmployees!fname & " " & _  
        rstEmployees!lname & " - " & rstEmployees!hire_date  
    rstEmployees!hire_date = #1/1/1900#  
    rstEmployees.Update  
    Debug.Print "Changed data"  
    Debug.Print "  Name - Hire Date"  
    Debug.Print "  " & rstEmployees!fname & " " & _  
        rstEmployees!lname & " - " & rstEmployees!hire_date  
  
    ' Requery Recordset and reset the hire date  
    rstEmployees.Requery  
    rstEmployees!hire_date = varDate  
    rstEmployees.Update  
    Debug.Print "Data after reset"  
    Debug.Print "  Name - Hire Date"  
    Debug.Print "  " & rstEmployees!fname & " " & _  
       rstEmployees!lname & " - " & rstEmployees!hire_date  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOpenVB  
```  
  
## <a name="see-also"></a>関連項目  
 [Close メソッド (ADO)](../../../ado/reference/ado-api/close-method-ado.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
