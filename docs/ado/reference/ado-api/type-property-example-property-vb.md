---
title: プロパティの例 (プロパティ) (VB) を入力します |。Microsoft Docs
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
- Type property [property] [ADO], Visual Basic example
ms.assetid: 2ee8e4c5-1d66-4a77-8892-6dad7e07e611
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8def5c7089be85c9b6eb7700a8a5bcdaeebe99e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937857"
---
# <a name="type-property-example-property-vb"></a>Type プロパティの例 (プロパティ) (VB)
この例では、[型](../../../ado/reference/ado-api/type-property-ado.md)プロパティ。 これは、モデルなどの名前と、コレクションの型を一覧表示するためのユーティリティの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)など。  
  
 開く必要はありません、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)へのアクセスをその**プロパティ**コレクションが存在することになるときに、**レコード セット**オブジェクトがインスタンス化します。 ただし、設定、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**をいくつかの動的プロパティを追加、**レコード セット**オブジェクトの**プロパティ**コレクション、例では、もう少し興味深いものを作成します。 図では、単純に明示的に使用して、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティにアクセスする各[プロパティ](../../../ado/reference/ado-api/property-object-ado.md)オブジェクト。  
  
```  
'BeginTypePropertyVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' recordset variables  
    Dim rst As ADODB.Recordset  
    Dim prop As ADODB.Property  
     ' property variables  
    Dim ix As Integer  
    Dim strMsg As String  
  
     ' create client-side recordset  
    Set rst = New ADODB.Recordset  
    rst.CursorLocation = adUseClient  
     ' enumerate property types  
    For ix = 0 To rst.Properties.Count - 1  
        Set prop = rst.Properties.Item(ix)  
        Select Case prop.Type  
           Case adBigInt  
              strMsg = "adBigInt"  
           Case adBinary  
              strMsg = "adBinary"  
           Case adBoolean  
              strMsg = "adBoolean"  
           Case adBSTR  
              strMsg = "adBSTR"  
           Case adChapter  
              strMsg = "adChapter"  
           Case adChar  
              strMsg = "adChar"  
           Case adCurrency  
              strMsg = "adCurrency"  
           Case adDate  
              strMsg = "adDate"  
           Case adDBDate  
              strMsg = "adDBDate"  
           Case adDBTime  
              strMsg = "adDBTime"  
           Case adDBTimeStamp  
              strMsg = "adDBTimeStamp"  
           Case adDecimal  
              strMsg = "adDecimal"  
           Case adDouble  
              strMsg = "adDouble"  
           Case adEmpty  
              strMsg = "adEmpty"  
           Case adError  
              strMsg = "adError"  
           Case adFileTime  
              strMsg = "adFileTime"  
           Case adGUID  
              strMsg = "adGUID"  
           Case adIDispatch  
              strMsg = "adIDispatch"  
           Case adInteger  
              strMsg = "adInteger"  
           Case adIUnknown  
              strMsg = "adIUnknown"  
           Case adLongVarBinary  
              strMsg = "adLongVarBinary"  
           Case adLongVarChar  
              strMsg = "adLongVarChar"  
           Case adLongVarWChar  
              strMsg = "adLongVarWChar"  
           Case adNumeric  
              strMsg = "adNumeric"  
           Case adPropVariant  
              strMsg = "adPropVariant"  
           Case adSingle  
              strMsg = "adSingle"  
           Case adSmallInt  
              strMsg = "adSmallInt"  
           Case adTinyInt  
              strMsg = "adTinyInt"  
           Case adUnsignedBigInt  
              strMsg = "adUnsignedBigInt"  
           Case adUnsignedInt  
              strMsg = "adUnsignedInt"  
           Case adUnsignedSmallInt  
              strMsg = "adUnsignedSmallInt"  
           Case adUnsignedTinyInt  
              strMsg = "adUnsignedTinyInt"  
           Case adUserDefined  
              strMsg = "adUserDefined"  
           Case adVarBinary  
              strMsg = "adVarBinary"  
           Case adVarChar  
              strMsg = "adVarChar"  
           Case adVariant  
              strMsg = "adVariant"  
           Case adVarNumeric  
              strMsg = "adVarNumeric"  
           Case adVarWChar  
              strMsg = "adVarWChar"  
           Case adWChar  
              strMsg = "adWChar"  
           Case Else  
              strMsg = "*UNKNOWN*"  
        End Select  
            'show results  
        Debug.Print "Property " & ix & ": " & prop.Name & _  
                    ", Type = " & strMsg  
    Next ix  
  
    ' clean up  
    Set rst = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    Set rst = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndTypePropertyVB  
```  
  
## <a name="see-also"></a>関連項目  
 [オブジェクトのプロパティ (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Type プロパティ (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
