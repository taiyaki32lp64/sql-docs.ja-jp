---
title: コマンドを使用してストアド プロシージャを呼び出す |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32f1013ef0aa9c8f02e19ec98234418480bc5f22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925862"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Command を使用してストアド プロシージャを呼び出す
ストアド プロシージャを呼び出すコマンドを使用することができます。 このトピックの最後のコード サンプルは、次のように定義されている、CustOrdersOrders と呼ばれる、Northwind サンプル データベース内のストアド プロシージャを参照します。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 ストアド プロシージャの詳細を定義して呼び出す方法については、SQL Server のドキュメントを参照してください。  
  
 このストアド プロシージャで使用されるコマンドのような[コマンド オブジェクト パラメーター](../../../ado/guide/data/command-object-parameters.md)します。 これにより、顧客の ID パラメーターを受け取りし、その顧客の注文に関する情報を返します。 次のコード サンプルは、ソースとしてこのストアド プロシージャを使用して ado **Recordset**します。  
  
 ストアド プロシージャを使用すると、ADO のもう 1 つの機能にアクセスできます。**パラメーター**コレクション**更新**メソッド。 このメソッドを使用すると、ADO に自動的に実行時に、コマンドによって必要なパラメーターのすべての情報を入力できます。 パフォーマンスの低下がある、この方法で ADO は、パラメーターに関する情報については、データ ソースを照会する必要がありますので。  
  
 その他の重要な相違点は、次のコード サンプルと、コードの間存在[コマンド オブジェクト パラメーター](../../../ado/guide/data/command-object-parameters.md)パラメーターを手動で入力した場所、します。 まず、このコードは設定されません、**準備**プロパティを**True**のため SQL Server ストアド プロシージャは、定義では、プリコンパイル済み。 2 つ目は、 **CommandType**のプロパティ、**コマンド**にオブジェクトが変更された**adCmdStoredProc** ADO コマンドがストアド プロシージャをしたことを通知するために 2 番目の例です。  
  
 最後に、2 番目の例では、パラメーターする必要がありますを参照してインデックスを使用して、値を設定するときにデザイン時に、パラメーターの名前がわからないためです。 新しい設定することができます、パラメーターの名前がわかっている場合[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)のプロパティ、**コマンド**を True にオブジェクトし、プロパティの名前を参照してください。 最初のパラメーターの位置が、ストアド プロシージャで説明されている理由なのでしょう (@CustomerID) は 0 ではなく 1 (`objCmd(1) = "ALFKI"`)。 これは、パラメーター 0 には、SQL Server ストアド プロシージャからの戻り値が含まれています。  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
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
'EndAutoParamCmd  
  
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
  
## <a name="see-also"></a>関連項目  
 [サポート技術情報記事 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
