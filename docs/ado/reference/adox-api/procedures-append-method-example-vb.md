---
title: Procedures Append メソッドの例 (VB) |Microsoft Docs
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
- Append method [ADOX], Visual Basic example
ms.assetid: ce83b966-474b-4f57-8eb9-370996dfc5c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bacc5dc2d55fb335358ab9ca34248f8e322811a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965423"
---
# <a name="procedures-append-method-example-vb"></a>Procedures Append メソッドの例 (VB)
次のコードを使用する方法を示します、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトと[プロシージャ](../../../ado/reference/adox-api/procedures-collection-adox.md)コレクション[Append](../../../ado/reference/adox-api/append-method-adox-procedures.md)メソッドを基になるデータ ソースに新しいプロシージャを作成します。  
  
```  
' BeginCreateProcedureVB  
Sub Main()  
    On Error GoTo CreateProcedureError  
  
    Dim cnn As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the parameterized command (Microsoft Jet specific)  
    Set cmd.ActiveConnection = cnn  
    cmd.CommandText = "PARAMETERS [CustId] Text;" & _  
    "Select * From Customers Where CustomerId = [CustId]"  
  
    ' Open the Catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Create the new Procedure  
    cat.Procedures.Append "CustomerById", cmd  
  
    'Clean  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateProcedureError:  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateProcedureVB  
```  
  
## <a name="see-also"></a>関連項目  
 [ActiveConnection プロパティ (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Append メソッド (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Procedure オブジェクト (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [Procedures コレクション (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
