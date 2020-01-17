---
title: BOF、EOF、および Bookmark プロパティの例 (VB) |Microsoft Docs
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
- BOF property [ADO], Visual Basic example
- Bookmark property [ADO], Visual Basic example
- EOF property [ADO], Visual Basic example
ms.assetid: b6573c6e-fee8-4267-a722-fadaec6eafe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ab332d7d4144d62dd3a0cee1d3585820bf77e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920436"
---
# <a name="bof-eof-and-bookmark-properties-example-vb"></a>BOF、EOF、および Bookmark プロパティの例 (VB)
この例では、 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)と[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)ユーザーでは、最初と最後のレコードのを越えて移動しようとすると、メッセージを表示するプロパティを[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 使用して、[ブックマーク](../../../ado/reference/ado-api/bookmark-property-ado.md)ユーザーが内のレコードにフラグを設定できるプロパティ、**レコード セット**し、後で戻ります。  
  
```  
'BeginBOFVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstPublishers As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLPubs As String  
     'record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
    Dim varBookmark As Variant  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' Open recordset and use client cursor  
     ' to enable AbsolutePosition property  
    Set rstPublishers = New ADODB.Recordset  
    strSQLPubs = "SELECT pub_id, pub_name FROM publishers ORDER BY pub_name"  
    rstPublishers.Open strSQLPubs, strCnxn, adUseClient, adOpenStatic, adCmdText  
  
    rstPublishers.MoveFirst  
    Do Until rstPublishers.EOF  
        ' Display information about current record  
        ' and get user input  
        strMessage = "Publisher: " & rstPublishers!pub_name & _  
            vbCr & "(record " & rstPublishers.AbsolutePosition & _  
            " of " & rstPublishers.RecordCount & ")" & vbCr & vbCr & _  
            "Enter command:" & vbCr & _  
            "[1 - next / 2 - previous /" & vbCr & _  
            "3 - set bookmark / 4 - go to bookmark]"  
        intCommand = Val(InputBox(strMessage))  
  
        ' Check user input  
        Select Case intCommand  
            Case 1  
                ' Move forward trapping for EOF  
                rstPublishers.MoveNext  
                If rstPublishers.EOF Then  
                    MsgBox "Moving past the last record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveLast  
                End If  
            Case 2  
                ' Move backward trapping for BOF  
                rstPublishers.MovePrevious  
                If rstPublishers.BOF Then  
                    MsgBox "Moving past the first record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveFirst  
                End If  
            Case 3  
                ' Store the bookmark of the current record  
                varBookmark = rstPublishers.Bookmark  
            Case 4  
                ' Go to the record indicated by the stored bookmark  
                If IsEmpty(varBookmark) Then  
                    MsgBox "No Bookmark set!"  
                Else  
                    rstPublishers.Bookmark = varBookmark  
                End If  
            Case Else  
                Exit Do  
        End Select  
    Loop  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndBOFVB  
```  
  
 この例では、**ブックマーク**と[フィルター](../../../ado/reference/ado-api/filter-property.md)ビューの一部を作成するプロパティ、 **Recordset**します。 ブックマークの配列によって参照される唯一のレコードはアクセスできます。  
  
```  
Attribute VB_Name = "BOF"  
```  
  
## <a name="see-also"></a>関連項目  
 [BOF、EOF プロパティ (ADO)](../../../ado/reference/ado-api/bof-eof-properties-ado.md)   
 [Bookmark プロパティ (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
