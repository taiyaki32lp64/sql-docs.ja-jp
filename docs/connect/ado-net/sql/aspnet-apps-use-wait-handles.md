---
title: 待機ハンドルを使用する ASP.NET アプリケーション
description: ASP.NET ページから複数の同時実行コマンドを実行する方法を示す例を示します。待機ハンドルを使用して、すべてのコマンドの完了時に操作を管理します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: f7d242410b5f7aadd74494bb33a7572afe23be54
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452330"
---
# <a name="aspnet-applications-using-wait-handles"></a>待機ハンドルを使用する ASP.NET アプリケーション

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

非同期操作を処理するためのコールバックおよびポーリングモデルは、アプリケーションが一度に1つの非同期操作のみを処理する場合に便利です。 待機モデルを使用すると、複数の非同期操作をより柔軟に処理できます。 2つの待機モデルがあり、それを実装するために使用される <xref:System.Threading.WaitHandle> メソッド (Wait (Any) モデルと Wait (All) モデル) という名前が付けられています。  
  
どちらの待機モデルを使用する場合も、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A>、または <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> メソッドによって返される <xref:System.IAsyncResult> オブジェクトの <xref:System.IAsyncResult.AsyncWaitHandle%2A> プロパティを使用する必要があります。 <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドと <xref:System.Threading.WaitHandle.WaitAll%2A> メソッドでは、両方とも <xref:System.Threading.WaitHandle> オブジェクトを引数として、配列内にグループ化して送信する必要があります。  
  
どちらの待機メソッドも、非同期操作を監視し、完了を待機します。 <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドは、いずれか 1 つの操作の完了またはタイムアウトを待機します。特定の操作が完了したことがわかれば、その結果を処理し、引き続き次の操作の完了またはタイムアウトを待機できます。<xref:System.Threading.WaitHandle.WaitAll%2A> メソッドは、<xref:System.Threading.WaitHandle> インスタンスの配列に含まれているすべてのプロセスが完了するかタイムアウトするまで次の操作の監視を開始しません。  
  
待機モデルの利点は、ある程度の長さの複数の操作を異なるサーバーで実行する必要がある場合、またはサーバーがすべてのクエリを同時に処理するのに十分な性能を備えている場合に最も影響を受けます。 ここで示す例では、3つのクエリは、さまざまな長さの WAITFOR コマンドを、重要でない SELECT クエリに追加することで、長いプロセスをエミュレートします。  
  
## <a name="example-wait-any-model"></a>例: Wait (Any) モデル  
次の例は、待機 (Any) モデルを示しています。 3つの非同期プロセスが開始されると、<xref:System.Threading.WaitHandle.WaitAny%2A> メソッドが呼び出され、いずれかの処理が完了するまで待機します。 各プロセスが完了すると、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> メソッドが呼び出され、結果の <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトが読み取られます。 この時点で、実際のアプリケーションでは、<xref:Microsoft.Data.SqlClient.SqlDataReader> を使用して、ページの一部にデータを入力する可能性があります。 この簡単な例では、プロセスに対応するテキストボックスにプロセスが完了した時刻が追加されています。 テキストボックス内の時刻は、プロセスが完了するたびにコードが実行されることを示しています。  
  
この例を設定するには、新しい ASP.NET Web サイトプロジェクトを作成します。 <xref:System.Web.UI.WebControls.Button> コントロールと4つの <xref:System.Web.UI.WebControls.TextBox> コントロールをページに配置します (各コントロールの既定の名前をそのまま使用します)。  
  
次のコードをフォームのクラスに追加し、環境に合わせて必要に応じて接続文字列を変更します。  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,              
     //  you can retrieve it from a configuration file.   
     //  If you have not included "Asynchronous Processing=true"   
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to   
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =   
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous   
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin   
          //  execution. Use the IAsyncResult object returned by   
          //  BeginExecuteReader to add a WaitHandle for the   
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to   
               //  complete. The return value is either the index   
               //  of the array element whose process just   
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,   
                    60000, false);  
               //  This example doesn't actually do anything with   
               //  the data returned by the processes, but the   
               //  code opens readers for each just to demonstrate       
               //  the concept.  
               //  Instead of using the returned data to fill the   
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =   
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =   
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =   
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>例: Wait (All) モデル  
次の例は、Wait (All) モデルを示しています。 3つの非同期プロセスが開始されると、<xref:System.Threading.WaitHandle.WaitAll%2A> メソッドが呼び出され、プロセスの完了またはタイムアウトを待機します。  
  
Wait (Any) モデルの例と同様に、プロセスが完了した時刻が、プロセスに対応するテキストボックスに追加されます。 ここでも、テキストボックス内の時刻はポイントを示しています。 <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドに続くコードは、すべてのプロセスが完了した後にのみ実行されます。  
  
この例を設定するには、新しい ASP.NET Web サイトプロジェクトを作成します。 <xref:System.Web.UI.WebControls.Button> コントロールと4つの <xref:System.Web.UI.WebControls.TextBox> コントロールをページに配置します (各コントロールの既定の名前をそのまま使用します)。  
  
次のコードをフォームのクラスに追加し、環境に合わせて必要に応じて接続文字列を変更します。  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,              
    //  you can retrieve it from a configuration file.   
    //  If you have not included "Asynchronous Processing=true"   
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to   
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =   
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous   
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =   
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =   
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin   
        //  execution. Use the IAsyncResult object returned by   
        //  BeginExecuteReader to add a WaitHandle for the   
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to   
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =   
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =   
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =   
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [非同期操作](asynchronous-operations.md)
