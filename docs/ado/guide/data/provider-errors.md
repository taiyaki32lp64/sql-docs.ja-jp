---
title: プロバイダー エラー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d4a7607fae1df7dfb6ec62b8a3bfae8f58001b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924546"
---
# <a name="provider-errors"></a>プロバイダー エラー
プロバイダー エラーが発生する、-2147467259 の実行時エラーが返されます。 このエラーが表示されたら、確認、**エラー**のアクティブなコレクション**接続**オブジェクトで、発生した内容について説明する 1 つまたは複数のエラーが含まれます。  
  
## <a name="the-ado-errors-collection"></a>ADO エラーのコレクション  
 ADO が経由でエラー オブジェクトのコレクションを公開する ADO の特定の操作が複数のプロバイダー エラーを生成するため、**接続**オブジェクト。 このコレクションが含まれていないオブジェクトには操作が正常に完了した、1 つ以上含まれている場合**エラー**何らかの問題と、プロバイダーには、1 つまたは複数のエラーが発生したかどうかのオブジェクトします。 エラーの正確な原因を特定するには、各エラー オブジェクトを確認します。  
  
 発生したエラーの処理が完了するとすぐに呼び出してコレクションをクリアできます、**オフ**メソッド。 明示的にオフに特に重要ですが、**エラー**コレクションを呼び出す前に、**再同期**、 **UpdateBatch**、または**CancelBatch**メソッドを**レコード セット**オブジェクト、**オープン**メソッドを**接続**オブジェクト、または設定、**フィルター**プロパティを**Recordset**オブジェクト。 コレクションを明示的にオフにすることを確認することができます、**エラー**コレクション内のオブジェクトが以前の操作に残されていません。  
  
 一部の操作には、エラーだけでなく警告を生成できます。 警告はによっても表されます**エラー**内のオブジェクト、**エラー**コレクション。 プロバイダーが、警告をコレクションに追加すると、実行時エラーは生成されません。 チェック、**カウント**のプロパティ、**エラー**警告が特定の操作によって生成されたかどうかを確認します。 場合は、数が 1 つ以上の場合、**エラー**オブジェクトがコレクションに追加されました。 あると判断するとすぐ、**エラー**コレクションには、エラーまたは警告が含まれています、コレクションを反復処理し、それぞれに関する情報を取得することができます**エラー**含まれているオブジェクト。 次の簡単な Visual Basic の例では、これを示しています。  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 エラー処理ルーチンが含まれています、**各**ループ内の各オブジェクトを検査する、**エラー**コレクション。 この例では、表示用のメッセージが蓄積されます。 実際のプログラムでは、各エラーは、適切なタスクを実行するコードを記述しますすべてを閉じるなどのファイルを開くし、適切な方法でプログラムをシャット ダウンします。  
  
## <a name="the-error-object"></a>Error オブジェクト  
 調べることで、**エラー**オブジェクトのどのようなエラーが発生するかを調べるしより重要ですが、どのようなアプリケーションまたはオブジェクト、エラーが発生します。 **エラー**オブジェクトは、次のプロパティ。  
  
|プロパティ名|説明|  
|-------------------|-----------------|  
|**[説明]**|発生したエラーの説明テキスト。|  
|**HelpContext、HelpFile**|発生したエラーの説明が含まれているヘルプ トピックとヘルプ ファイルを参照します。|  
|**NativeError**|プロバイダー固有のエラー番号。|  
|**数値**|数を表す長整数 (記載、 **ErrorValueEnum**) の発生したエラー。|  
|**ソース**|オブジェクトまたはエラーを生成したアプリケーションの名前を示します。|  
|**SQLState**|プロバイダーを返す SQL ステートメントの処理中に 5 文字のエラー コードを指定します。|  
  
 ADO**エラー**オブジェクトは、標準の Visual Basic によく似た**Err**オブジェクト。 そのプロパティには、発生したエラーについて説明します。 エラーの数、2 つの関連情報が表示されます。 **NativeError**プロパティには、エラー番号が含まれています。 使用するプロバイダーに固有です。 前の例では、プロバイダーしたが、Microsoft OLE DB Provider for SQL Server, **NativeError**は SQL Server に固有のエラーが含まれます。 **SQLState**プロパティは、SQL ステートメントでエラーを説明するための 5 文字コード。  
  
## <a name="event-related-errors"></a>イベントに関連するエラー  
 **エラー**イベントに関連するエラーが発生したときにも、オブジェクトが使用されます。 ADO イベントを発生させたをチェックしてプロセスでエラーが発生するかどうかを指定できます、**エラー**イベント パラメーターとして渡されるオブジェクト。  
  
 イベントを実行する操作が正常に行われる場合、 *adStatus*イベント ハンドラーのパラメーターに設定する*adStatusOK*します。 その一方、イベントを発生させた操作が、失敗した場合、 *adStatus*にパラメーターが設定されている*adStatusErrorsOccurred*します。 その場合は、 *pError*パラメーターには、**エラー**エラーを説明するオブジェクト。
