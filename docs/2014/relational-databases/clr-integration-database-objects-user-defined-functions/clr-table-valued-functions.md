---
title: CLR テーブル値関数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7dfd3db3a8193e92f9670213c602d55dc45f5c7f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232290"
---
# <a name="clr-table-valued-functions"></a>CLR テーブル値関数
  テーブル値関数とは、テーブルを返すユーザー定義関数です。  
  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、テーブル値関数の機能が拡張され、テーブル値関数をどのマネージド言語でも定義できるようになりました。 テーブル値関数からは `IEnumerable` オブジェクトまたは `IEnumerator` オブジェクトを経由してデータが返されます。  
  
> [!NOTE]  
>  テーブル値関数で返されるテーブル型の列には、timestamp 型の列および Unicode 以外の文字列データ型の列 (`char`、`varchar`、`text` など) を含めることはできません。 NOT NULL 制約はサポートされません。  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Transact-SQL と CLR のテーブル値関数の違い  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] のテーブル値関数は、関数の呼び出し結果を具体化して中間テーブルを作成します。 TVF では中間テーブルを使用するため、結果に対する制約や一意インデックスがサポートされます。 これらの機能は、大量の結果が返される場合に非常に有用です。  
  
 一方、CLR のテーブル値関数は同じことをストリーミングで実現します。 結果セット全体を 1 つのテーブルに具体化する必要はありません。 テーブル値関数を呼び出すクエリの実行プランから、マネージド関数が返す `IEnumerable` オブジェクトを直接呼び出し、結果を増分方式で使用します。 このストリーミング モデルでは、テーブル全体に値が格納されるまで待たなくても、最初の行が生成された直後から結果を使用できます。 返される行をメモリ内で一括して具体化する必要がないので、返される行数が多い場合にもストリーミングが適しています。 たとえば、マネージド テーブル値関数を使用して、テキスト ファイルを解析し、テキストの各行を 1 つのテーブル行にして返すことができます。  
  
## <a name="implementing-table-valued-functions"></a>テーブル値関数の実装  
 テーブル値関数は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework アセンブリのクラスのメソッドとして実装します。 テーブル値関数のコードでは、`IEnumerable` インターフェイスを実装する必要があります。 
  `IEnumerable` インターフェイスは .NET Framework で定義されています。 .NET Framework で配列およびコレクションを表す型は、既に `IEnumerable` インターフェイスを実装しています。 このため、コレクションまたは配列を結果セットに変換するテーブル値関数を簡単に記述できます。  
  
## <a name="table-valued-parameters"></a>テーブル値パラメーター  
 テーブル値パラメーターとは、プロシージャや関数に渡されるユーザー定義のテーブル型です。テーブル値パラメーターを使用すると、複数行のデータを効率的にサーバーに渡すことができます。 テーブル値パラメーターの機能はパラメーター配列に似ていますが、より柔軟性が高く、[!INCLUDE[tsql](../../includes/tsql-md.md)] との統合も緊密です。 テーブル値パラメーターを使用するとパフォーマンスが向上する可能性もあります。 さらに、サーバーへのラウンド トリップの回数を減らすのにも有用です。 スカラー パラメーターのリストを使用するなどしてサーバーに複数の要求を送信する代わりに、データをテーブル値パラメーターとしてサーバーに送信できます。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセスで実行されているマネージド ストアド プロシージャやマネージド関数にユーザー定義のテーブル型をテーブル値パラメーターとして渡したり、戻り値として受け取ったりすることはできません。 テーブル値パラメーターの詳細については、「[テーブル値パラメーターの使用 &#40;データベース エンジン&#41;](../tables/use-table-valued-parameters-database-engine.md)」を参照してください。  
  
## <a name="output-parameters-and-table-valued-functions"></a>出力パラメーターとテーブル値関数  
 出力パラメーターを使用すると、テーブル値関数から情報を返すことができます。 実装コードのテーブル値関数の対応するパラメーターは、引数として参照渡しのパラメーターを使用する必要があります。 Visual Basic は出力パラメーターを Visual C# と同様にはサポートしていません。 次に示すように、パラメーターを参照渡し\<で指定し、出力パラメーターを表す Out () > 属性を適用する必要があります。  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>Transact-SQL のテーブル値関数の定義  
 CLR テーブル値関数を定義するための構文は [!INCLUDE[tsql](../../includes/tsql-md.md)] テーブル値関数の構文と似ていますが、`EXTERNAL NAME` 句が追加されています。 例:  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 テーブル値関数を使用して、クエリで追加処理を行うリレーショナル形式のデータを表現できます。次に例を示します。  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 テーブル値関数は、次の場合にテーブルを返すことができます。  
  
-   スカラー値の入力引数から作成された場合。 たとえば、数値をコンマで区切った文字列をピボットしてテーブルにするテーブル値関数などです。  
  
-   外部データから生成した場合。 たとえば、イベント ログを読み取り、テーブルとして公開するテーブル値関数などです。  
  
 **メモ**テーブル値関数は、メソッドではなく[!INCLUDE[tsql](../../includes/tsql-md.md)] `InitMethod` `FillRow` 、メソッド内のクエリを通じてのみデータアクセスを実行できます。 
  `InitMethod` クエリを実行する場合は、`SqlFunction.DataAccess.Read` を [!INCLUDE[tsql](../../includes/tsql-md.md)] 属性プロパティに指定してください。  
  
## <a name="a-sample-table-valued-function"></a>テーブル値関数のサンプル  
 次のテーブル値関数は、システム イベント ログから情報を返します。 読み取るイベント ログの名前を含んだ文字列引数を 1 つ受け取ります。  
  
###### <a name="sample-code"></a>サンプル コード  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>サンプルのテーブル値関数の宣言と使用  
 コンパイルしたサンプルのテーブル値関数は、次のように [!INCLUDE[tsql](../../includes/tsql-md.md)] で宣言できます。  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、/clr:pure を指定してコンパイルした Visual C++ のデータベース オブジェクトは実行できません。 このようなデータベース オブジェクトには、テーブル値関数などがあります。  
  
 サンプルをテストするには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを使用してください。  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>サンプル: SQL Server クエリの結果を返す  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対してクエリを実行するテーブル値関数を示します。 この例では、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の AdventureWorks Light データベースを使用します。 AdventureWorks [https://www.codeplex.com/sqlserversamples](https://go.microsoft.com/fwlink/?LinkId=87843)のダウンロードの詳細については、「」を参照してください。  
  
 ソース コード ファイルに FindInvalidEmails.cs または FindInvalidEmails.vb という名前を付けます。  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 ソース コードをコンパイルして DLL を生成し、DLL を C ドライブのルート ディレクトリにコピーします。  その後、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを実行します。  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
