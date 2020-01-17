---
title: CLR トリガー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87d822e97a75bbd08375980fe6a6f0341d8f9c60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755253"
---
# <a name="clr-triggers"></a>CLR トリガー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR (共通言語ランタイム) との統合により、任意の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 言語を使用して CLR トリガーを作成できるようになりました。 ここでは、CLR 統合によって実装されたトリガー固有の情報について説明します。 トリガーの詳細については、次を参照してください。 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)します。  
  
## <a name="what-are-triggers"></a>トリガーとは  
 トリガーとは、言語イベントの実行時に自動的に実行される、特殊なストアド プロシージャです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、DML (データ操作言語) トリガーと DDL (データ定義言語) トリガーという 2 種類の一般的なトリガーがあります。 DML トリガーは、`INSERT` ステートメント、`UPDATE` ステートメント、または `DELETE` ステートメントにより、指定されたテーブルやビューのデータが変更されるときに使用できます。 DDL トリガーは、主に `CREATE`、`ALTER`、および `DROP` で始まるさまざまな DDL ステートメントに応じてストアド プロシージャを起動します。 DDL トリガーは、データベース操作の監査や管理などの管理作業に使用できます。  
  
## <a name="unique-capabilities-of-clr-triggers"></a>CLR トリガー独自の機能  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] で記述されたトリガーには、トリガーを起動するビューやテーブルの列が `UPDATE(column)` 関数および `COLUMNS_UPDATED()` 関数を使用して更新されたかどうかを判断する機能があります。  
  
 CLR 言語で記述されたトリガーは、いくつかの重要な点で他の CLR 統合オブジェクトとは異なります。 CLR トリガーでは次のことを行えます。  
  
-   `INSERTED` テーブルや `DELETED` テーブル内のデータの参照  
  
-   `UPDATE` 操作の結果として変更された列の判断  
  
-   DDL ステートメントの実行によって影響を受けたデータベース オブジェクトに関する情報へのアクセス  
  
 このような機能は、クエリ言語の本質として提供されます。`SqlTriggerContext` クラスによって提供することもできます。 CLR 統合とマネージ コードの使い分けの利点については、[!INCLUDE[tsql](../../includes/tsql-md.md)]を参照してください[CLR 統合の概要](../../relational-databases/clr-integration/clr-integration-overview.md)します。  
  
## <a name="using-the-sqltriggercontext-class"></a>SqlTriggerContext クラスの使用  
 `SqlTriggerContext` クラスをパブリックに生成することはできません。このクラスは、CLR トリガー本体に含まれる `SqlContext.TriggerContext` プロパティにアクセスすることによってのみ取得できます。 `SqlTriggerContext` クラスは、`SqlContext` プロパティを呼び出すことにより、アクティブな `SqlContext.TriggerContext` から取得できます。  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 `SqlTriggerContext` クラスでは、トリガーに関するコンテキスト情報が提供されます。 このコンテキスト情報には、トリガーを起動した動作の種類、UPDATE 操作で変更された列、および DDL トリガーの場合はトリガー操作が記述されている XML `EventData` 構造体が含まれます。 詳細については、次を参照してください。 [EVENTDATA &#40;TRANSACT-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)します。  
  
### <a name="determining-the-trigger-action"></a>トリガー動作の判断  
 `SqlTriggerContext` を取得すると、これを使用してトリガーを起動した動作の種類を判断できます。 この情報は、`TriggerAction` クラスの `SqlTriggerContext` プロパティから入手できます。  
  
 DML トリガーの場合、`TriggerAction` プロパティは次のいずれかの値になります。  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete(0x3)  
  
-   DDL トリガーの場合、TriggerAction の有効な値は非常に多くなります。 詳細については、.NET Framework SDK の「TriggerAction Enumeration」を参照してください。  
  
### <a name="using-the-inserted-and-deleted-tables"></a>Inserted テーブルと Deleted テーブルの使用  
 DML トリガー ステートメントで 2 つの特殊なテーブルが使用されます。**挿入**テーブルおよび**削除**テーブル。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、これらのテーブルを自動的に作成および管理します。 これらの一時テーブルを使用して、あるデータ変更の影響を調べたり、DML トリガー動作の条件を設定することができます。ただし、このテーブル内のデータを直接変更することはできません。  
  
 CLR トリガーにアクセスできる、**挿入**と**削除**CLR インプロセス プロバイダーを使用してテーブル。 この操作は、SqlContext オブジェクトから `SqlCommand` オブジェクトを取得することによって行います。 以下に例を示します。  
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>更新された列の判断  
 `ColumnCount` オブジェクトの `SqlTriggerContext` プロパティを使用して、UPDATE 操作によって変更された列の数を判断できます。 入力パラメーターとして列序数を受け取る `IsUpdatedColumn` メソッドを使用すると、列が更新されたかどうかを判断できます。 値 `True` は、列が更新されたことを示します。  
  
 たとえば、後半で示す EmailAudit トリガーからの次のコードでは、更新されたすべての列が一覧されます。  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>CLR DDL トリガーの EventData へのアクセス  
 DDL トリガーは標準的なトリガーと同様、イベントに応じてストアド プロシージャを起動します。 ただし、DML トリガーとは異なり、テーブルやビューでの UPDATE、INSERT、または DELETE ステートメントに応じて DDL トリガーが起動されることはありません。 代わりに、DDL トリガーは、さまざまな DDL ステートメントに応じて起動されます。このような DDL ステートメントは、主に CREATE、ALTER、DROP で始まるステートメントです。 DDL トリガーは、データベース操作やスキーマの変更の監査や管理などの管理作業に使用できます。  
  
 DDL トリガーを起動するイベントに関する情報は、`EventData` クラスの `SqlTriggerContext` プロパティで入手できます。 このプロパティには、`xml` 値が含まれます。 xml スキーマには、次の項目に関する情報が含まれています。  
  
-   イベントの時刻。  
  
-   トリガーが実行されている間の接続のシステム プロセス ID (SPID)。  
  
-   トリガーを起動したイベントの種類。  
  
 イベントの種類に応じて、イベントが発生したデータベース、イベントが発生したオブジェクト、イベントの [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドなどの追加情報がスキーマに含まれます。  
  
 次の例では、DDL トリガーは `EventData` プロパティをそのまま返します。  
  
> [!NOTE]  
>  `SqlPipe` オブジェクトを使用して結果やメッセージを送信する例は、説明をわかりやすくするために記載しているものです。通常、CLR トリガーをプログラミングするときに、この処理を実稼働コードに実装することはお勧めしません。 予期しない追加データが返され、アプリケーション エラーの原因となる場合があります。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
       }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 次のサンプル出力は、`EventData` イベントによって DDL トリガーを起動された後の `CREATE TABLE` プロパティの値です。  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 クエリでは、`SqlTriggerContext` クラスからアクセスできる情報のほか、インプロセスで実行されるコマンドのテキスト内で `COLUMNS_UPDATED`、COLUMNS_INSERTED、および COLUMNS_DELETED を引き続き参照できます。  
  
## <a name="sample-clr-trigger"></a>サンプル CLR トリガー  
 この例では、ユーザーに必要な任意の ID を選択させ、具体的に ID として電子メール アドレスを入力したユーザーを知りたい場合のシナリオについて考えてみます。 次のトリガーは、その情報を検出し、監査テーブルにログを記録します。  
  
> [!NOTE]  
>  `SqlPipe` オブジェクトを使用して結果とメッセージを送信する例は、説明をわかりやすくするために記載しているものです。通常、この処理を実稼働コードに実装することはお勧めしません。 返される追加のデータに予期しない原因となるアプリケーション エラー可能性があります。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
     }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 次の定義では 2 つのテーブルが存在することを前提にしています。  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]でトリガーを作成するステートメント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は次のように、アセンブリを前提と**SQLCLRTest**現在では既に登録されて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>無効なトランザクションの検証およびキャンセル  
 無効な INSERT、UPDATE、または DELETE トランザクションの検証および取り消しを行う場合や、データベース スキーマへの変更を回避する場合には、トリガーを使用するのが一般的です。 これは、検証ロジックをトリガーに組み込み、アクションが検証条件に合わない場合は現在のトランザクションをロールバックすることにより、行うことができます。  
  
 トリガー内で呼び出されると、`Transaction.Rollback` メソッドまたはコマンド テキスト "TRANSACTION ROLLBACK" の SqlCommand は、不明確なエラー メッセージを発生して例外をスローし、これを try/catch ブロックにラップする必要が生じます。 表示されるエラー メッセージは、次のような。  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 この例外は想定されるものであり、コードの実行を継続するには try/catch ブロックが必要です。 トリガー コードが実行を終了すると、別の例外が発生します。  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 この例外が予期されても、および前後の try/catch ブロック、[!INCLUDE[tsql](../../includes/tsql-md.md)]実行を続行するために、トリガーを起動するアクションを実行するステートメントは必要です。 この 2 つの例外がスローされても、トランザクションはロールバックされ、変更はテーブルにコミットされません。 CLR トリガーと [!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーの主な違いは、トランザクションがロールバックされた後、[!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーは、動作を継続してさらに実行を行えるということです。  
  
### <a name="example"></a>例  
 次のトリガーでは、テーブルで INSERT ステートメントの簡単な検証を実行します。 挿入された整数値が 1 に等しい場合、トランザクションはロールバックされ、値はテーブルに挿入されません。 その他のすべての整数値はテーブルに挿入されます。 `Transaction.Rollback` メソッドの前後の try/catch ブロックに注意してください。 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトは、テスト テーブル、アセンブリ、およびマネージド ストアド プロシージャを作成します。 トリガーにより実行が終了されたときにスローされる例外をキャッチするため、2 つの INSERT ステートメントが try/catch ブロックにラップされることに注意してください。  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DML トリガー](../../relational-databases/triggers/dml-triggers.md)   
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [共通言語ランタイムによるデータベース オブジェクトを構築&#40;CLR&#41;統合](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
