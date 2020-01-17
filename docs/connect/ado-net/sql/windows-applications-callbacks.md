---
title: コールバックを使用する Windows アプリケーション
description: 非同期コマンドを安全に実行し、フォームとその内容との対話を別のスレッドから正しく処理する方法を示す例を示します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ae2ea457-0764-4b06-8977-713c77e85bd2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 5c2d46e3f2b26a8106e75f2bb116907e2f27a7b9
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451902"
---
# <a name="windows-applications-using-callbacks"></a>コールバックを使用する Windows アプリケーション

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ほとんどの非同期処理のシナリオでは、データベース操作を開始し、データベース操作の完了を待たずに、他のプロセスの実行を続行します。 ただし、多くのシナリオでは、データベース操作が終了した後に何らかの処理を行う必要があります。 たとえば、Windows アプリケーションでは、ユーザーインターフェイススレッドの応答性を維持しながら、長時間実行される操作をバックグラウンドスレッドに委任することができます。 ただし、データベース操作が完了したら、結果を使用してフォームにデータを入力する必要があります。 この種類のシナリオは、コールバックを使用して実装することをお勧めします。  
  
コールバックは、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A>、または <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> メソッドで <xref:System.AsyncCallback> デリゲートを指定することによって定義します。 操作が完了すると、デリゲートが呼び出されます。 デリゲートを <xref:Microsoft.Data.SqlClient.SqlCommand> 自体に渡すことで、<xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトに簡単にアクセスし、グローバル変数を使用しなくても適切な `End` メソッドを呼び出すことができます。  
  
## <a name="example"></a>例  
次の Windows アプリケーションは、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A> メソッドの使用方法を示しています。これは、数秒の遅延を含む Transact-sql ステートメントを実行する (長時間実行されるコマンドをエミュレートする) ことを示しています。  
  
この例は、別のスレッドからフォームと対話するメソッドを呼び出すなど、いくつかの重要な手法を示しています。 さらに、この例では、ユーザーがコマンドを複数回同時に実行するのをブロックする方法と、コールバックプロシージャが呼び出される前にフォームが閉じないようにする方法について説明します。  
  
この例を設定するには、新しい Windows アプリケーションを作成します。 <xref:System.Windows.Forms.Button> コントロールと2つの <xref:System.Windows.Forms.Label> コントロールをフォームに配置します (各コントロールの既定の名前をそのまま使用します)。 次のコードをフォームのクラスに追加し、環境に合わせて必要に応じて接続文字列を変更します。  
  
```csharp  
// Add these to the top of the class, if they're not already there:  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
// Hook up the form's Load event handler (you can double-click on   
// the form's design surface in Visual Studio), and then add   
// this code to the form's class:  
  
// You'll need this delegate in order to display text from a thread  
// other than the form's thread. See the HandleCallback  
// procedure for more information.  
// This same delegate matches both the DisplayStatus   
// and DisplayResults methods.  
private delegate void DisplayInfoDelegate(string Text);  
  
// This flag ensures that the user doesn't attempt  
// to restart the command or close the form while the   
// asynchronous command is executing.  
private bool isExecuting;  
  
// This example maintains the connection object   
// externally, so that it's available for closing.  
private SqlConnection connection;  
  
private static string GetConnectionString()  
{  
    // To avoid storing the connection string in your code,              
    // you can retrieve it from a configuration file.   
  
    // If you have not included "Asynchronous Processing=true" in the  
    // connection string, the command will not be able  
    // to execute asynchronously.  
    return "Data Source=(local);Integrated Security=SSPI;" +  
    "Initial Catalog=AdventureWorks; Asynchronous Processing=true";  
}  
  
private void DisplayStatus(string Text)  
{  
    this.label1.Text = Text;  
}  
  
private void DisplayResults(string Text)  
{  
    this.label1.Text = Text;  
    DisplayStatus("Ready");  
}  
  
private void Form1_FormClosing(object sender, System.Windows.Forms.FormClosingEventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Can't close the form until " +  
        "the pending asynchronous command has completed. Please " +  
        "wait...");
        e.Cancel = true;  
    }  
}  
  
private void button1_Click(object sender, System.EventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Already executing. Please wait until " +  
        "the current query has completed.");  
    }  
    else  
    {  
        SqlCommand command = null;  
        try  
        {  
            DisplayResults("");  
            DisplayStatus("Connecting...");  
            connection = new SqlConnection(GetConnectionString());  
            // To emulate a long-running query, wait for   
            // a few seconds before working with the data.  
            // This command doesn't do much, but that's the point--  
            // it doesn't change your data, in the long run.  
            string commandText =  
                "WAITFOR DELAY '0:0:05';" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint + 1 " +  
                "WHERE ReorderPoint Is Not Null;" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint - 1 " +  
                "WHERE ReorderPoint Is Not Null";  
  
            command = new SqlCommand(commandText, connection);  
            connection.Open();  
  
            DisplayStatus("Executing...");  
            isExecuting = true;  
            // Although it's not required that you pass the   
            // SqlCommand object as the second parameter in the   
            // BeginExecuteNonQuery call, doing so makes it easier  
            // to call EndExecuteNonQuery in the callback procedure.  
            AsyncCallback callback = new AsyncCallback(HandleCallback);  
  
            // Once the BeginExecuteNonQuery method is called,  
            // the code continues--and the user can interact with  
            // the form--while the server executes the query.  
            command.BeginExecuteNonQuery(callback, command);  
  
        }  
        catch (Exception ex)  
        {  
            isExecuting = false;  
            DisplayStatus($"Ready (last error: {ex.Message})");
            if (connection != null)  
            {  
                connection.Close();  
            }  
        }  
    }  
}  
  
private void HandleCallback(IAsyncResult result)  
{  
    try  
    {  
        // Retrieve the original command object, passed  
        // to this procedure in the AsyncState property  
        // of the IAsyncResult parameter.  
        SqlCommand command = (SqlCommand)result.AsyncState;  
        int rowCount = command.EndExecuteNonQuery(result);  
        string rowText = " rows affected.";  
        if (rowCount == 1)  
        {  
            rowText = " row affected.";  
        }  
        rowText = rowCount + rowText;  
  
        // You may not interact with the form and its contents  
        // from a different thread, and this callback procedure  
        // is all but guaranteed to be running from a different thread  
        // than the form. Therefore you cannot simply call code that   
        // displays the results, like this:  
        // DisplayResults(rowText)  
  
        // Instead, you must call the procedure from the form's thread.  
        // One simple way to accomplish this is to call the Invoke  
        // method of the form, which calls the delegate you supply  
        // from the form's thread.   
        DisplayInfoDelegate del =   
         new DisplayInfoDelegate(DisplayResults);  
        this.Invoke(del, rowText);  
    }  
    catch (Exception ex)  
    {  
        // Because you're now running code in a separate thread,   
        // if you don't handle the exception here, none of your other  
        // code will catch the exception. Because none of your  
        // code is on the call stack in this thread, there's nothing  
        // higher up the stack to catch the exception if you don't   
        // handle it here. You can either log the exception or   
        // invoke a delegate (as in the non-error case in this   
        // example) to display the error on the form. In no case  
        // can you simply display the error without executing a   
        // delegate as in the try block here.   
  
        // You can create the delegate instance as you   
        // invoke it, like this:  
        this.Invoke(new DisplayInfoDelegate(DisplayStatus),  
            $"Ready (last error: {ex.Message}");
    }  
    finally  
    {  
        isExecuting = false;  
        if (connection != null)  
        {  
            connection.Close();  
        }  
    }  
}  
  
private void Form1_Load(object sender, System.EventArgs e)  
{  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    this.FormClosing += new System.Windows.Forms.  
        FormClosingEventHandler(this.Form1_FormClosing);  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [非同期操作](asynchronous-operations.md)
