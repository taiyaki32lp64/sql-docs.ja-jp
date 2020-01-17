---
title: 接続プロパティの例 (VB) |Microsoft Docs
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
- ConnectionString property [ADO], Visual Basic example
- ConnectionTimeout property [ADO], Visual Basic example
- State property [ADO], Visual Basic example
ms.assetid: 4de7336a-b5ea-43f1-b750-5fa302b5b756
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d0cd34b13889ed44e32e29a058ca01d48aea1b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933473"
---
# <a name="connectionstring-connectiontimeout-and-state-properties-example-vb"></a>ConnectionString、ConnectionTimeout、および状態のプロパティの例 (VB)
この例を使用してさまざまな方法を示しています、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティを開き、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 またを使用して、 [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)接続タイムアウトを設定するプロパティと[状態](../../../ado/reference/ado-api/state-property-ado.md)接続の状態を確認するプロパティ。 GetState 関数は、この手順を実行する必要があります。  
  
> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。  
  
```  
'BeginConnectionStringVB  
  
    'To integrate this code replace  
    'the database, DSN or Data Source values  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim Cnxn3 As ADODB.Connection  
    Dim Cnxn4 As ADODB.Connection  
  
     ' Open a connection without using a Data Source Name (DSN)  
    Set Cnxn1 = New ADODB.Connection  
    Cnxn1.ConnectionString = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn1.Open  
    MsgBox "Cnxn1 state: " & GetState(Cnxn1.State)  
  
     ' Open a connection using a DSN and ODBC tags  
     ' It is assumed that you have created DSN 'Pubs' with a user name as  
     ' 'MyUserId' and password as 'MyPassword'.  
    Set Cnxn2 = New ADODB.Connection  
    Cnxn2.ConnectionString = "Data Source='Pubs';" & _  
        "User ID='MyUserId';Password='MyPassword';"  
    Cnxn2.ConnectionTimeout = 30  
    Cnxn2.Open  
    MsgBox "Cnxn2 state: " & GetState(Cnxn2.State)  
  
     ' Open a connection using a DSN and OLE DB tags  
     ' It is assumed that you have created DSN 'Pubs1' with windows authentication.  
    Set Cnxn3 = New ADODB.Connection  
    Cnxn3.ConnectionString = "Data Source='Pubs1';"  
    Cnxn3.Open  
    MsgBox "Cnxn2 state: " & GetState(Cnxn3.State)  
  
     ' Open a connection using a DSN and individual  
     ' arguments instead of a connection string  
     ' It is assumed that you have created DSN 'Pubs' with a user name as  
     ' 'MyUserId' and password as 'MyPassword'.  
    Set Cnxn4 = New ADODB.Connection  
    Cnxn4.Open "Pubs", "MyUserId", "MyPassword"  
    MsgBox "Cnxn4 state: " & GetState(Cnxn4.State)  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Cnxn3.Close  
    Cnxn4.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Set Cnxn3 = Nothing  
    Set Cnxn4 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn1 Is Nothing Then  
        If Cnxn1.State = adStateOpen Then Cnxn1.Close  
    End If  
    Set Cnxn1 = Nothing  
  
    If Not Cnxn2 Is Nothing Then  
        If Cnxn2.State = adStateOpen Then Cnxn2.Close  
    End If  
    Set Cnxn2 = Nothing  
  
    If Not Cnxn3 Is Nothing Then  
        If Cnxn3.State = adStateOpen Then Cnxn3.Close  
    End If  
    Set Cnxn3 = Nothing  
  
    If Not Cnxn4 Is Nothing Then  
        If Cnxn4.State = adStateOpen Then Cnxn4.Close  
    End If  
    Set Cnxn4 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
Public Function GetState(intState As Integer) As String  
  
   Select Case intState  
      Case adStateClosed  
         GetState = "adStateClosed"  
      Case adStateOpen  
         GetState = "adStateOpen"  
   End Select  
  
End Function  
'EndConnectionStringVB  
```  
  
## <a name="see-also"></a>関連項目  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [ConnectionTimeout プロパティ (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)   
 [State プロパティ (ADO)](../../../ado/reference/ado-api/state-property-ado.md)
