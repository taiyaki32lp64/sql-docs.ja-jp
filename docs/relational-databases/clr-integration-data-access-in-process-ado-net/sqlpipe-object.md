---
title: SqlPipe オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 6ecc3f87313b6ddcd48b7b0e527ba4effd58e624
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913554"
---
# <a name="sqlpipe-object"></a>SqlPipe オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、結果や出力パラメーターを呼び出し側のクライアントに送信するストアド プロシージャ (または拡張ストアド プロシージャ) を作成することがごく一般的でした。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]任意のストアド プロシージャ、**選択**0 個以上の行を返すステートメントが接続されている呼び出し元の「パイプ」に、結果を送信します  
  
 共通言語ランタイム (CLR) データベースで実行されているオブジェクト[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して、接続されているパイプに結果を送信することができます、**送信**のメソッド、 **SqlPipe**オブジェクト。 アクセス、**パイプ**のプロパティ、 **SqlContext**オブジェクトを取得する、 **SqlPipe**オブジェクト。 **SqlPipe**クラスは、概念的に似ています、**応答**クラスは ASP.NET です。 詳細については、.NET Framework Software Development Kit の SqlPipe クラスのリファレンス ドキュメントを参照してください。  
  
## <a name="returning-tabular-results-and-messages"></a>表形式の結果とメッセージを返す  
 **SqlPipe**が、**送信**メソッドで、次の 3 つのオーバー ロードがあります。 これらは次のとおりです。  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **送信**メソッドは、クライアントまたは呼び出し元に直接データを送信します。 出力を使用するクライアントでは、通常は、 **SqlPipe**、CLR ストアド プロシージャの入れ子になった場合出力のコンシューマーもストアド プロシージャをできます。 たとえば、Procedure1 がコマンド テキスト "EXEC Procedure2" の SqlCommand.ExecuteReader() を呼び出すとします。 Procedure2 もマネージド ストアド プロシージャです。 ここで Procedure2 が SqlPipe.Send( SqlDataRecord ) を呼び出すと、行はクライアントではなく、Procedure1 のリーダーに送信されます。  
  
 **送信**メソッドの PRINT と情報メッセージとしてクライアントに表示される文字列メッセージを送信[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 単一行の結果セットを使用しても送信できる**SqlDataRecord**、または複数行の結果セットを使用して、 **SqlDataReader**します。  
  
 **SqlPipe**オブジェクトも、 **ExecuteAndSend**メソッド。 このメソッドは、コマンドを実行するために使用できます (として渡される、 **SqlCommand**オブジェクト) し、呼び出し元に直接の結果を送信します。 送信されたコマンドにエラーがある場合、パイプに例外が送信されますが、呼び出し元のマネージド コードにもコピーが送信されます。 呼び出し元コードが例外をキャッチしない場合は、履歴を伝わり [!INCLUDE[tsql](../../includes/tsql-md.md)] コードに反映され、2 度出力に表示されます。 呼び出し元コードが例外をキャッチした場合、パイプ コンシューマーにはまだエラーが表示されますが、重複するエラーはありません。  
  
 かかるのみ、 **SqlCommand**コンテキスト接続に関連付けられている; 非コンテキスト接続に関連付けられているコマンドがかかることはできません。  
  
## <a name="returning-custom-result-sets"></a>カスタム結果セットを返す  
 マネージ ストアド プロシージャから提供されない結果セットを送信できる、 **SqlDataReader**します。 **SendResultsStart**メソッドと共に**SendResultsRow**と**SendResultsEnd**、により、ストアド プロシージャに独自の結果セットをクライアントに送信します。  
  
 **SendResultsStart**は、 **SqlDataRecord**として入力します。 さらに、結果セットの先頭にマークを付け、レコード メタデータを使用して、結果セットを説明するメタデータを生成します。 レコードの値を送信しません**SendResultsStart**します。 その後すべての行を使用して送信**SendResultsRow**、そのメタデータの定義に一致する必要があります。  
  
> [!NOTE]  
>  呼び出した後、 **SendResultsStart**メソッドのみ**SendResultsRow**と**SendResultsEnd**呼び出すことができます。 同じインスタンス内の他のメソッドの呼び出し**SqlPipe**により、 **InvalidOperationException**します。 **SendResultsEnd**設定**SqlPipe**他のメソッドを呼び出すことができます、初期状態に戻す。  
  
### <a name="example"></a>例  
 **UspGetProductLine**ストアド プロシージャ名、製品番号、色、および指定した製品ラインに含まれるすべての製品の表示価格を返します。 このストアド プロシージャでは、完全に一致する*prodLine*します。  
  
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
  
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントの実行、 **uspGetProduct**プロシージャで、ツーリング自転車製品の一覧を返します。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>関連項目  
 [SqlDataRecord オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR ストアド プロシージャ](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
