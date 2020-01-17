---
title: 接続の Close メソッド、Table Type プロパティの例 (VB) |Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4559a8d46852f37f2e828ce8f4abbd0e40845744
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966709"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Connection Close メソッド、Table Type プロパティの例 (VB)
設定、 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)プロパティを**Nothing**カタログへの接続を閉じる必要があります。 関連付けられたコレクションは空になります。 カタログ内のスキーマ オブジェクトから作成されたすべてのオブジェクトは孤立します。 キャッシュされているこれらのオブジェクトのプロパティはいずれも使用できなくなりますが、プロバイダーの呼び出しを必要とするプロパティの読み取りを試行は失敗します。  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 閉じる、[接続](../../../ado/reference/ado-api/connection-object-ado.md)カタログを開くために使用するオブジェクトの設定と同じ効果があります、 **ActiveConnection**プロパティを**Nothing**します。  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>関連項目  
 [ActiveConnection プロパティ (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [列オブジェクト (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [列のコレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Table オブジェクト (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables コレクション (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type プロパティ (テーブル) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
