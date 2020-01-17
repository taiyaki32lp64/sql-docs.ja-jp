---
title: 検出および競合の解決 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce9917f144e8c63160f571a986263d8d7e97b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925564"
---
# <a name="detecting-and-resolving-conflicts"></a>競合の検出および解決
イミディ エイト モードで、レコード セットを処理する場合は、同時実行の問題が発生する可能性ははるかに少ないです。 その一方で、アプリケーションでは、バッチ モードの更新を使用する場合があります良い機会が同じレコードを編集する別のユーザーによって加えられた変更が保存される前にその 1 つのユーザーが、レコードを変更します。 このような場合は、競合を適切に処理するアプリケーションを必要があります。 最後に変更をサーバーに更新を送信するユーザーが優先します"をお望みがある可能性があります。 または、どの更新プログラムの優先順位が競合する 2 つの値の間で選択 (英語) を提供することで決定する最新のユーザーに通知します。  
  
 どのような場合は、ADO では、これらの種類の競合を処理するためにフィールド オブジェクトの UnderlyingValue と OriginalValue プロパティを提供します。 Resync メソッドと、レコード セットのフィルター プロパティはこれらのプロパティを組み合わせて使用します。  
  
## <a name="remarks"></a>コメント  
 ADO では、バッチ更新中に競合が検出されると、警告がエラー コレクションに追加されます。 そのため、必ずチェック エラー BatchUpdate を呼び出すし、検索する場合は、競合が発生しているという前提のテストを開始した後にすぐに。 最初の手順では、競合するレコード セットと等しいのフィルター プロパティを設定します。 これにより、競合するレコードのみをレコード セットの表示が制限されます。 RecordCount プロパティがこの手順の後に 0 に等しい場合は、以外の競合によってエラーが発生したがわかります。  
  
 BatchUpdate を呼び出すときに ADO とプロバイダーのデータ ソースで更新プログラムを実行する SQL ステートメントは生成します。 特定のデータ ソースにする列の型を使用して WHERE 句での制限事項があることに注意してください。  
  
 次に、設定 adAffectGroup と処理を等しく設定 ResyncValues 引数に等しい AffectRecords 引数で、レコード セットで再同期メソッドを呼び出します。 Resync メソッドは、基になるデータベースから現在のレコード セット オブジェクト内のデータを更新します。 AdAffectGroup を使用するは、データベース、つまり、競合するレコードのみを設定する現在のフィルターを使用して、表示されたレコードのみが再同期されることを確認します。 大規模なレコード セットを扱う場合、パフォーマンスに大きな違いでしたください。 再同期を呼び出すときに、処理を ResyncValues 引数を設定、UnderlyingValue プロパティでは、データベースから (競合) の値を含むこと、Value プロパティが、ユーザーが入力した値を維持することを確認し、ある OriginalValue プロパティは (最後の正常な UpdateBatch 呼び出しが行われた前に、の値) のフィールドの元の値を保持します。 プログラムで、競合を解決するか、またはユーザーが使用される値を選択し、これらの値を使用できます。  
  
 この手法は、次のコード例に示します。 例では、意図的には UpdateBatch が呼び出される前に、基になるテーブル内の値を変更する別のレコード セットを使用して競合を作成します。  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 どのような競合が発生したかを判断するのに、または特定のフィールドの現在のレコードの Status プロパティを使用できます。  
  
 エラー処理の詳細については、次を参照してください。[エラー処理](../../../ado/guide/data/error-handling.md)します。  
  
## <a name="see-also"></a>参照  
 [バッチ モード](../../../ado/guide/data/batch-mode.md)
