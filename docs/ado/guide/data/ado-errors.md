---
title: ADO エラー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c357384a3de683c05b2922149e2b61630881922
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926193"
---
# <a name="ado-run-time-errors"></a>ADO の実行時エラー
ADO エラーは、プログラムを実行時エラーとして報告されます。 トラップし、それらを処理するプログラミング言語のエラー トラップ メカニズムを使用できます。 たとえば、Visual Basic では、使用して、 **On Error**ステートメント。 Visual C で ADO ライブラリへのアクセスに使用しているメソッドに依存します。 #Import を使用して、 **try catch**ブロックします。 それ以外の場合、C++ プログラマは、明示的に呼び出すことによって、エラー オブジェクトを取得する必要があります。 **GetErrorInfo**します。 ADO エラーをトラップする次の Visual Basic のサブ手順を示しています。

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 これは、 **Form_Load**イベント プロシージャが同じを開こうとしてエラーを意図的に作成**接続**オブジェクトを 2 回クリックします。 2 回目、**オープン**メソッドが呼び出されると、エラー ハンドラーがアクティブ化されます。 型のエラーがここでは**adErrObjectOpen**ので、エラー ハンドラーは、プログラムの実行を再開する前に、次のメッセージを表示します。

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 エラー メッセージには、Visual Basic で提供される情報の各部分が含まれています。 **Err**以外のオブジェクト、 **LastDLLError**値で、ここでは適用されません。 エラー番号は、エラーの種類を指示します。 説明は、自分で、エラーを処理する必要なしない場合に便利です。 ユーザーに、作業は渡すだけで済みます。 ただし、アプリケーション用にカスタマイズされたメッセージを使用することは通常、すべてのエラーが予想されることはできません。説明ではいくつか問題点に関する手がかりとなります。 サンプル コードでエラーが報告された、**接続**オブジェクト。 オブジェクトの型またはプログラムで、ID が表示されます、変数名ではありません。

> [!NOTE]
>  Visual Basic **Err**オブジェクトには、最新のエラーに関する情報にはのみが含まれています。 ADO**エラー**のコレクション、**接続**オブジェクトには、1 つ含まれる**エラー**の最新の ADO 操作によって発生した各エラー オブジェクト。 使用して、**エラー**コレクションではなく、 **Err**複数のエラーを処理するオブジェクト。 詳細については、**エラー** 、コレクションを参照してください[プロバイダー エラー](../../../ado/guide/data/provider-errors.md)します。 ただし、有効ながある場合**接続**オブジェクト、 **Err**オブジェクトは ADO エラーに関する情報の唯一のソース。

 操作の種類は、ADO のエラーが発生する可能性がありますか。 ADO の一般的なエラーによってなどのオブジェクトを開くことができますが含まれる、**接続**または**レコード セット**データを更新しようとしています。 または、プロバイダーでサポートされていないプロパティまたはメソッドの呼び出し。

 OLE DB エラーは、実行時のエラーとしてアプリケーションに渡すこともできます、**エラー**コレクション。

 次のトピックでは、ADO エラーについて詳しく説明します。

-   [ADO エラー リファレンス](../../../ado/guide/data/ado-error-reference.md)
