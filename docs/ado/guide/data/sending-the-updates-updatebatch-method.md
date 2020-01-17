---
title: '更新プログラムの送信: UpdateBatch メソッド |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 182e444587ce9bb3ca73166fb05dfac2506a39aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924258"
---
# <a name="sending-the-updates-updatebatch-method"></a>更新プログラムの送信: UpdateBatch メソッド
次のコードは、バッチ モードで adLockBatchOptimistic を CursorLocation LockType プロパティを設定してレコード セットを開きます。 2 つの新しいレコードを追加しますして、元の値を保存、既存のレコードのフィールドの値を変更し、データ ソースへの変更の送信を UpdateBatch を呼び出します。  
  
## <a name="remarks"></a>コメント  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 現在のレコードを編集または UpdateBatch メソッドを呼び出すと、新しいレコードを追加する場合、ADO は自動的に、Update メソッドをプロバイダーに変更を一括送信する前に、現在のレコードに保留中の変更を保存を呼び出します。  
  
## <a name="see-also"></a>関連項目  
 [バッチ モード](../../../ado/guide/data/batch-mode.md)
