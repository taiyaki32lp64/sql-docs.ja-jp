---
title: Command オブジェクトのパラメーター |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29ad7f3aa9347af77080b04fb309f8b50b95dbe4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925874"
---
# <a name="command-object-parameters"></a>Command オブジェクトのパラメーター
前のトピックで説明した[を作成して、単純なコマンドを実行する](../../../ado/guide/data/creating-and-executing-a-simple-command.md)します。 使用して、興味深い、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)で次の例では、SQL コマンドのパラメーター化するオブジェクトを表示します。 この変更により、パラメーターのたびに別の値を渡して、コマンドを再利用することです。 [プロパティの準備](../../../ado/reference/ado-api/prepared-property-ado.md)プロパティを**コマンド**にオブジェクトが設定されている**true**、ADO で指定されたコマンドをコンパイルするプロバイダーが必要になります[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)を初めて実行する前にします。 メモリ内のコンパイル済みのコマンドも保持されます。 少しそれがパフォーマンスの向上、コマンドがその後呼び出されるたびに結果を準備するために必要なオーバーヘッドが原因で実行される初めてのコマンドの実行はこの低下します。 そのため、1 つ以上の時間を使用する場合にのみ、コマンドを準備する必要があります。  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndManualParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
 すべてのプロバイダーは、準備されたコマンドをサポートします。 このプロパティに設定するとすぐには、エラーを返す可能性がありますが、プロバイダーがコマンドの準備をサポートしていない場合**True**します。 エラーを返さない場合、コマンド ウィンドウとセットを準備する要求は無視されます、**準備**プロパティを**false**します。
