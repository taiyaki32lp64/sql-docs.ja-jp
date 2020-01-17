---
title: ソースのプロパティの例 (VB) |Microsoft Docs
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
- Source property [ADO], Visual Basic example
ms.assetid: 7c83eb01-71c7-4c5d-9778-6270471c8164
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5161dc2aa0a0a213095a160cf0473c138cdf2cf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930919"
---
# <a name="source-property-example-vb"></a>Source プロパティの例 (VB)
この例では、[ソース](../../../ado/reference/ado-api/source-property-ado-recordset.md)プロパティを 3 つを開いて[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトは、さまざまなデータ ソースに基づきます。  
  
```  
'BeginSourceVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstTitles As ADODB.Recordset  
    Dim rstPublishers As ADODB.Recordset  
    Dim rstPublishersDirect As ADODB.Recordset  
    Dim rstTitlesPublishers As ADODB.Recordset  
    Dim cmdSQL As ADODB.Command  
    Dim strCnxn As String  
    Dim strSQL As String  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open a recordset based on a command object  
    Set cmdSQL = New ADODB.Command  
    Set cmdSQL.ActiveConnection = Cnxn  
    strSQL = "Select title, type, pubdate FROM Titles ORDER BY title"  
    cmdSQL.CommandText = strSQL  
    Set rstTitles = cmdSQL.Execute()  
  
    ' Open a recordset based on a table  
    Set rstPublishers = New ADODB.Recordset  
    strSQL = "Publishers"  
    rstPublishers.Open strSQL, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
    'rstPublishers.Open strSQL, Cnxn, , , adCmdTable  
     ' the above two lines of code are identical  
  
    ' Open a recordset based on a table  
    Set rstPublishersDirect = New ADODB.Recordset  
    rstPublishersDirect.Open strSQL, strCnxn, , , adCmdTableDirect  
  
    ' Open a recordset based on an SQL string.  
    Set rstTitlesPublishers = New ADODB.Recordset  
    strSQL = "SELECT title_ID AS TitleID, title AS Title, " & _  
        "publishers.pub_id AS PubID, pub_name AS PubName " & _  
        "FROM publishers INNER JOIN Titles " & _  
        "ON publishers.pub_id = Titles.pub_id " & _  
        "ORDER BY Title"  
    rstTitlesPublishers.Open strSQL, strCnxn, , , adCmdText  
  
    ' Use the Source property to display the source of each recordset.  
    MsgBox "rstTitles source: " & vbCr & _  
        rstTitles.Source & vbCr & vbCr & _  
        "rstPublishers source: " & vbCr & _  
        rstPublishers.Source & vbCr & vbCr & _  
        "rstPublishersDirect source: " & vbCr & _  
        rstPublishersDirect.Source & vbCr & vbCr & _  
        "rstTitlesPublishers source: " & vbCr & _  
        rstTitlesPublishers.Source  
  
    ' clean up  
    rstTitles.Close  
    rstPublishers.Close  
    rstTitlesPublishers.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set rstPublishers = Nothing  
    Set rstTitlesPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not rstTitlesPublishers Is Nothing Then  
        If rstTitlesPublishers.State = adStateOpen Then rstTitlesPublishers.Close  
    End If  
    Set rstTitlesPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSourceVB  
```  
  
## <a name="see-also"></a>関連項目  
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Source プロパティ (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
