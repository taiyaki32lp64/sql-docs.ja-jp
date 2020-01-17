---
title: データの編集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e8fd90849b8e046a7f4fe5d158d4594e612c91f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925492"
---
# <a name="editing-data"></a>データの編集
説明しました ADO を使用してデータ ソースへの接続、コマンドを実行で、結果を得る方法、**レコード セット**オブジェクト内を移動したり、**レコード セット**します。 このセクションでは、次の基本的な ADO 操作について重点的に取り上げます。: データを編集します。  
  
 このセクションは、サンプルを使用して引き続き**レコード セット**で導入された[データを調べる](../../../ado/guide/data/examining-data.md)、1 つの重要な変更。 次のコードの使用を開く、 **Recordset**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 コードに重要な変更は、設定、 **CursorLocation**のプロパティ、**接続**オブジェクトと等しい**adUseClient**で、 *GetNewConnection*クライアント カーソルの使用を示します (次の例で示すように) 関数。 クライアント側とサーバー側のカーソルの違いの詳細については、次を参照してください。[カーソルとロック](../../../ado/guide/data/understanding-cursors-and-locks.md)します。  
  
 **CursorLocation**プロパティの**adUseClient**設定は、データ ソース (この場合は SQL Server) から、カーソルの位置をクライアント コード (デスクトップ ワークステーション) の場所に移動します。 この設定が強制的に作成し、カーソルを管理するためにクライアントで OLE DB 用のクライアント カーソル エンジンを起動します。  
  
 お気付きかもしれませんが、 **LockType**のパラメーター、**オープン**方法に変更**adLockBatchOptimistic**します。 これにより、カーソルがバッチ モードで開きます。 (プロバイダーが複数の変更をキャッシュし、呼び出すときにのみ、基になるデータ ソースに書き込む、 **UpdateBatch**メソッドです)。加えられた変更、 **Recordset**までデータベースには更新されません、 **UpdateBatch**メソッドが呼び出されます。  
  
 最後に、このセクションのコードでは、GetNewConnection 関数の変更バージョンを使用します。 このバージョンの関数は、クライアント側カーソルを返すようになりました。 関数のようになります。  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 このセクションでは、次のトピックを扱います。  
  
-   [既存のレコードの編集](../../../ado/guide/data/editing-existing-records.md)  
  
-   [レコードの追加](../../../ado/guide/data/adding-records.md)  
  
-   [サポートされている機能を特定する](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Delete メソッドを使用してレコードを削除する](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [代替手段:SQL ステートメントを使用](../../../ado/guide/data/alternatives-using-sql-statements.md)
