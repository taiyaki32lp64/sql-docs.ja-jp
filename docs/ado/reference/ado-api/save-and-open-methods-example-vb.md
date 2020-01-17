---
title: 保存および開く方法の例 (VB) |Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d42488f8f167cc7c98f663478c742963d24253c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931194"
---
# <a name="save-and-open-methods-example-vb"></a>Save および Open メソッドの例 (VB)
これら 3 つの例を示す方法、[保存](../../../ado/reference/ado-api/save-method.md)と[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドを併用することができます。  
  
 出張していると、データベースからテーブルを実行することを想定しています。 としてデータにアクセスするにする前に、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)移動可能な形式で保存します。 目的地に到着する場合にアクセスする、 **Recordset**として、ローカル切断**レコード セット**します。 変更を加える、 **Recordset**、し、もう一度保存します。 最後に、home、戻るときに再度データベースに接続し、外出先で行われた変更で更新します。  
  
 最初に、アクセスし、保存、***作成者***テーブル。  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 この時点では、目的地に到着しました。 アクセス、***作成者***として、ローカル テーブル切断**レコード セット**します。 必要があります、 **MSPersist**保存したファイルへのアクセスに使用しているコンピューター上のプロバイダー a:\Pubs.xml します。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最後に、戻っています。 変更内容をデータベースを更新ようになりました。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>関連項目  
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [詳細については、レコード セットの保持](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
