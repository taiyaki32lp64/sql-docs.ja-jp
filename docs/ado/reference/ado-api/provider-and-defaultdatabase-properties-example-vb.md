---
title: Provider および DefaultDatabase プロパティの例 (VB) |Microsoft Docs
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
- DefaultDatabase property [ADO], Visual Basic example
- provider property [ADO], Visual Basic example
ms.assetid: 677e1dbe-bcf6-4028-a62c-e99b1c88bf7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46486167ab5e8bd1b063928d4ba3f6f73c893784
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931512"
---
# <a name="provider-and-defaultdatabase-properties-example-vb"></a>Provider および DefaultDatabase プロパティの例 (VB)
この例では、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)プロパティを開き、3 つ[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトを別のプロバイダーを使用します。 また、使用、 [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) Microsoft ODBC プロバイダーの既定のデータベースを設定するプロパティ。  
  
> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。  
  
```  
'BeginProviderVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection strings  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim Cnxn3 As ADODB.Connection  
    Dim strCnxn As String  
  
    ' Open a connection using the Microsoft ODBC provider  
    Set Cnxn1 = New ADODB.Connection  
    Cnxn1.ConnectionString = "driver={SQL Server};server='MySqlServer';" & _  
        "user id='MyUserID';password='MyPassword';"  
    Cnxn1.Open strCnxn  
    Cnxn1.DefaultDatabase = "Pubs"  
  
    ' Display the provider  
    MsgBox "Cnxn1 provider: " & Cnxn1.Provider  
  
    ' Open a connection using the Microsoft Jet provider  
    Set Cnxn2 = New ADODB.Connection  
    Cnxn2.Provider = "Microsoft.Jet.OLEDB.4.0"  
    Cnxn2.Open "Northwind.mdb", _  
        "MyUserID", "MyPassword"  
  
    ' Display the provider.  
    MsgBox "Cnxn2 provider: " & Cnxn2.Provider  
  
    ' Open a connection using the Microsoft SQL Server provider  
    Set Cnxn3 = New ADODB.Connection  
    Cnxn3.Provider = "sqloledb"  
    Cnxn3.Open "Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Display the provider  
    MsgBox "Cnxn3 provider: " & Cnxn3.Provider  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Cnxn3.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Set Cnxn3 = Nothing  
    Exit Sub  
  
ErrorHandler:  
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
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndProviderVB  
```  
  
## <a name="see-also"></a>関連項目  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [DefaultDatabase プロパティ](../../../ado/reference/ado-api/defaultdatabase-property.md)   
 [Provider プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)
