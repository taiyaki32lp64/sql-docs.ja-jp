---
title: DeleteRule プロパティの例 (VB) |Microsoft Docs
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
- DeleteRule property [ADOX], Visual Basic example
ms.assetid: 9ba00118-a80d-4a6d-a7d6-4f5492fb7ded
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95f27c6ad6e4ae7cdfd0938f6c82a9932751fbc4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966404"
---
# <a name="deleterule-property-example-vb"></a>DeleteRule プロパティの例 (VB)
この例では、 [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)のプロパティを[キー](../../../ado/reference/adox-api/key-object-adox.md)オブジェクト。 新しいコードを追加します[テーブル](../../../ado/reference/adox-api/table-object-adox.md)し、新しいプライマリ キーが、設定を定義および**DeleteRule**に**adRICascade**します。  
  
```  
' BeginDeleteRuleVB  
Sub Main()  
    On Error GoTo DeleteRuleXError  
  
    Dim kyPrimary As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
    Dim tblNew As New ADOX.Table  
  
    ' Connect the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
                     "data source='Northwind.mdb';"  
  
    ' Name new table  
    tblNew.Name = "NewTable"  
  
    ' Append a numeric and a text field to new table.  
    tblNew.Columns.Append "NumField", adInteger, 20  
    tblNew.Columns.Append "TextField", adVarWChar, 20  
  
    ' Append the new table  
    cat.Tables.Append tblNew  
  
    ' Define the Primary key  
    kyPrimary.Name = "NumField"  
    kyPrimary.Type = adKeyPrimary  
    kyPrimary.RelatedTable = "Customers"  
    kyPrimary.Columns.Append "NumField"  
    kyPrimary.Columns("NumField").RelatedColumn = "CustomerId"  
    kyPrimary.DeleteRule = adRICascade  
  
    ' Append the primary key  
    cat.Tables("NewTable").Keys.Append kyPrimary  
    Debug.Print "The primary key is appended."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tblNew.Name  
    Debug.Print "The primary key is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
    Exit Sub  
  
DeleteRuleXError:  
  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDeleteRuleVB  
```  
  
## <a name="see-also"></a>関連項目  
 [DeleteRule プロパティ (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)   
 [Key オブジェクト (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
