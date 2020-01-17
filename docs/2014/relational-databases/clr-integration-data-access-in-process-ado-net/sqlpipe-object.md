---
title: SqlPipe オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcf462f82d7455f83bb0bee8a3b0af991ec2e7db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920054"
---
# <a name="sqlpipe-object"></a>SqlPipe オブジェクト
  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、結果や出力パラメーターを呼び出し側のクライアントに送信するストアド プロシージャ (または拡張ストアド プロシージャ) を作成することがごく一般的でした。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャでは、0 行以上の行を返す `SELECT` ステートメントはすべて、接続している呼び出し側の "パイプ" に結果を送信します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行されている CLR (共通言語ランタイム) データベース オブジェクトの場合は、`Send` オブジェクトの `SqlPipe` メソッドを使用して、接続しているパイプに結果を送信できます。 `Pipe` オブジェクトを取得するには、`SqlContext` オブジェクトの `SqlPipe` プロパティにアクセスします。 `SqlPipe` クラスは、概念的には ASP.NET の `Response` クラスに似ています。 詳細については、.NET Framework Software Development Kit の SqlPipe クラスのリファレンス ドキュメントを参照してください。  
  
## <a name="returning-tabular-results-and-messages"></a>表形式の結果とメッセージを返す  
 `SqlPipe` には、3 つのオーバーロードを持つ `Send` メソッドがあります。 これらは次のとおりです。  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 `Send` メソッドでは、データがそのままクライアントまたは呼び出し元に送信されます。 通常、`SqlPipe` の出力を使用するのはクライアントですが、入れ子になった CLR ストアド プロシージャの場合、ストアド プロシージャが出力のコンシューマーになる可能性もあります。 たとえば、Procedure1 がコマンド テキスト "EXEC Procedure2" の SqlCommand.ExecuteReader() を呼び出すとします。 Procedure2 もマネージド ストアド プロシージャです。 ここで Procedure2 が SqlPipe.Send( SqlDataRecord ) を呼び出すと、行はクライアントではなく、Procedure1 のリーダーに送信されます。  
  
 `Send` メソッドは、クライアントで情報メッセージとして表示される文字列メッセージを送信します。これは、[!INCLUDE[tsql](../../includes/tsql-md.md)] の PRINT と同等です。 また、`SqlDataRecord` を使用して単一行の結果セットを送信することも、`SqlDataReader` を使用して複数行の結果セットを送信することもできます。  
  
 `SqlPipe` オブジェクトには、`ExecuteAndSend` メソッドもあります。 このメソッドは、(`SqlCommand` オブジェクトで渡された) コマンドを実行し、その結果を直接呼び出し側に返送するために使用できます。 送信されたコマンドにエラーがある場合、パイプに例外が送信されますが、呼び出し元のマネージド コードにもコピーが送信されます。 呼び出し元コードが例外をキャッチしない場合は、履歴を伝わり [!INCLUDE[tsql](../../includes/tsql-md.md)] コードに反映され、2 度出力に表示されます。 呼び出し元コードが例外をキャッチした場合、パイプ コンシューマーにはまだエラーが表示されますが、重複するエラーはありません。  
  
 このメソッドは、コンテキスト接続に関連付けられた `SqlCommand` だけを受け取ります。コンテキスト接続以外に関連付けられたコマンドを受け取ることはできません。  
  
## <a name="returning-custom-result-sets"></a>カスタム結果セットを返す  
 マネージド ストアド プロシージャでは、`SqlDataReader` 以外からの結果セットを送信できます。 `SendResultsStart` メソッドでは、`SendResultsRow` や `SendResultsEnd` と同様に、ストアド プロシージャからクライアントにカスタム結果セットを送信できます。  
  
 `SendResultsStart` は、`SqlDataRecord` を入力として受け取ります。 さらに、結果セットの先頭にマークを付け、レコード メタデータを使用して、結果セットを説明するメタデータを生成します。 `SendResultsStart` を使ってレコードの値が送信されることはありません。 以降、`SendResultsRow` を使用して送信されるすべての行は、そのメタデータ定義に一致する必要があります。  
  
> [!NOTE]  
>  `SendResultsStart` メソッドを呼び出した後に呼び出せるのは、`SendResultsRow` と `SendResultsEnd` のみです。 `SqlPipe` の同じインスタンスで他のどのメソッドを呼び出しても、`InvalidOperationException` が発生することになります。 `SendResultsEnd` は、`SqlPipe` を初期状態に戻し、他のメソッドを呼び出せるようにします。  
  
### <a name="example"></a>例  
 `uspGetProductLine` ストアド プロシージャは、指定した製品ライン内のすべての製品の名前、製品番号、色、および表示価格を返します。 このストアド プロシージャでは、完全に一致する*prodLine*します。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、ツーリング自転車製品の一覧を返す `uspGetProduct` プロシージャを実行します。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>参照  
 [SqlDataRecord オブジェクト](sqldatarecord-object.md)   
 [CLR ストアド プロシージャ](../../database-engine/dev-guide/clr-stored-procedures.md)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
