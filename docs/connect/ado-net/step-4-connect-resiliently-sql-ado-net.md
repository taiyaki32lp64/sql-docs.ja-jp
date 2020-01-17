---
title: '手順 4: ADO.NET | を使用して弾性的を SQL に接続するMicrosoft Docs'
description: SQL に接続する方法について説明します。
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 62ec2eb775ef5fba76b402d1871afe6c87bcc606
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451803"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>ステップ 4: ADO.NET で SQL に弾性的に接続する

![Download-DownArrow-Circled](../../ssdt/media/download.png)[ADO.NET をダウンロードする](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- 前の記事:&nbsp;&nbsp;&nbsp;[手順 3: ADO.NET を使用した SQL への接続を概念実証する](step-3-connect-sql-ado-net.md)  

  
このトピックでは、カスタムの再試行ロジックを示す C# コード サンプルを提供します。 再試行ロジックは信頼性を提供します。 再試行ロジックは、一時的なエラーまたは一時的な*障害*を適切に処理するように設計されています。これは、プログラムが数秒待ってから再試行した場合に解消される傾向があります。  
  
一時的なエラーの原因は次のとおりです。  
  
- インターネットをサポートするネットワークの簡単な障害。  
- クラウドシステムでは、クエリが送信された時点でそのリソースを負荷分散することがあります。  
  
  
ローカル Microsoft SQL Server に接続するための ADO.NET クラスでは、Azure SQL Database に接続することもできます。 ただし、ADO.NET クラスでは、実稼働環境で必要なすべての堅牢性と信頼性を提供することはできません。 クライアントプログラムで一時的な障害が発生し、そのエラーが発生した場合は、自動的に復旧して正常に回復し続ける必要があります。  
  
## <a name="step-1-identify-transient-errors"></a>手順 1: 一時的なエラーを特定する  
  
プログラムでは、一時的なエラーと永続的なエラーを区別する必要があります。 一時的なエラーは、一時的なネットワークの問題など、短時間に発生する可能性があるエラー状態です。  永続的なエラーの例としては、プログラムでターゲットデータベース名のスペルミスが発生した場合 (この場合、"そのようなデータベースが見つかりませんでした" というエラーが発生し、短時間で消去することはできません) が考えられます。  
  
一時的な障害として分類されたエラー番号の一覧は、「 [SQL Database クライアントアプリケーションのエラーメッセージ](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)」で確認できます。  
  
## <a name="step-2-create-and-run-sample-application"></a>手順 2: サンプルアプリケーションを作成して実行する  
  
このサンプルでは .NET Framework 4.5.1 以降がインストールされていることを前提としています。  このC#コードサンプルは、Program.cs という名前の1つのファイルで構成されています。 そのコードは、次のセクションで説明します。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>手順 2. a: コードサンプルをキャプチャしてコンパイルする  
  
このサンプルをコンパイルするには、次の手順を実行します。  
  
1. [無料の Visual Studio Community edition](https://www.visualstudio.com/products/visual-studio-community-vs)、C# コンソール アプリケーション テンプレートから新しいプロジェクトを作成します。  
    - ファイル > 新しい > プロジェクト > インストールされているC# > テンプレート > Visual > Windows > クラシックデスクトップ > コンソールアプリケーション  
    - プロジェクトに**retryado2.exe**という名前を指定します。  
2. [ソリューションエクスプローラー] ウィンドウを開きます。  
    - プロジェクトの名前を確認します。  
    - Program.cs ファイルの名前を参照してください。  
3. Program.cs ファイルを開きます。  
4. Program.cs ファイルの内容を、次のコードブロックのコードに完全に置き換えます。  
5. [ビルド > ビルド] メニューをクリックします。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>手順 2. b: サンプルコードをコピーして貼り付ける  
  
このコードを**Program.cs**ファイルに貼り付けます。  
  
次に、サーバー名、パスワードなどの文字列を編集する必要があります。 これらの文字列は、 **GetSqlConnectionStringBuilder**という名前のメソッドで見つけることができます。  
  
注: サーバー名の接続文字列は、 **tcp:** の4文字のプレフィックスが含まれているため、Azure SQL Database に合わせて構成されています。 ただし、サーバー文字列を調整して Microsoft SQL Server に接続することもできます。  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
using TD = System.Threading;  
    
namespace RetryAdo2  
{  
  public class Program  
  {  
    static public int Main(string[] args)  
    {  
      bool succeeded = false;  
      int totalNumberOfTimesToTry = 4;  
      int retryIntervalSeconds = 10;  
    
      for (int tries = 1;  
        tries <= totalNumberOfTimesToTry;  
        tries++)  
      {  
        try  
        {  
          if (tries > 1)  
          {  
            Console.WriteLine  
              ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
              tries, totalNumberOfTimesToTry  
              );  
            TD.Thread.Sleep(1000 * retryIntervalSeconds);  
            retryIntervalSeconds = Convert.ToInt32  
              (retryIntervalSeconds * 1.5);  
          }  
          AccessDatabase();  
          succeeded = true;  
          break;  
        }  
    
        catch (QC.SqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (TestSqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (Exception Exc)  
        {  
          Console.WriteLine(Exc);  
          succeeded = false;  
          break;  
        }  
      }  
    
      if (succeeded == true)  
      {  
        return 0;  
      }  
      else  
      {  
        Console.WriteLine("ERROR: Unable to access the database!");  
        return 1;  
      }  
    }  
    
    /// <summary>  
    /// Connects to the database, reads,  
    /// prints results to the console.  
    /// </summary>  
    static public void AccessDatabase()  
    {  
      //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
    
      using (var sqlConnection = new QC.SqlConnection  
          (GetSqlConnectionString()))  
      {  
        using (var dbCommand = sqlConnection.CreateCommand())  
        {  
          dbCommand.CommandText = @"  
SELECT TOP 3  
    ob.name,  
    CAST(ob.object_id as nvarchar(32)) as [object_id]  
  FROM sys.objects as ob  
  WHERE ob.type='IT'  
  ORDER BY ob.name;";  
    
          sqlConnection.Open();  
          var dataReader = dbCommand.ExecuteReader();  
    
          while (dataReader.Read())  
          {  
            Console.WriteLine("{0}\t{1}",  
              dataReader.GetString(0),  
              dataReader.GetString(1));  
          }  
        }  
      }  
    }  
    
    /// <summary>  
    /// You must edit the four 'my' string values.  
    /// </summary>  
    /// <returns>An ADO.NET connection string.</returns>  
    static private string GetSqlConnectionString()  
    {  
      // Prepare the connection string to Azure SQL Database.  
      var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
    
      // Change these values to your values.  
      sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
      sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
    
      sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
      sqlConnectionSB.Password = "MyPassword";  
      sqlConnectionSB.IntegratedSecurity = false;  
    
      // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
      sqlConnectionSB.ConnectRetryCount = 3;  
      sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
    
      // Leave these values as they are.  
      sqlConnectionSB.IntegratedSecurity = false;  
      sqlConnectionSB.Encrypt = true;  
      sqlConnectionSB.ConnectTimeout = 30;  
    
      return sqlConnectionSB.ToString();  
    }  
    
    static public CG.List<int> TransientErrorNumbers =  
      new CG.List<int> { 4060, 40197, 40501, 40613,  
      49918, 49919, 49920, 11001 };  
  }  
    
  /// <summary>  
  /// For testing retry logic, you can have method  
  /// AccessDatabase start by throwing a new  
  /// TestSqlException with a Number that does  
  /// or does not match a transient error number  
  /// present in TransientErrorNumbers.  
  /// </summary>  
  internal class TestSqlException : ApplicationException  
  {  
    internal TestSqlException(int testErrorNumber)  
    { this.Number = testErrorNumber; }  
    
    internal int Number  
    { get; set; }  
  }  
}  
```  
  
###  <a name="step-2c-run-the-program"></a>手順 2. c: プログラムを実行する  
  
  
**Retryado2.exe**実行可能ファイルは、パラメーターを入力しません。 .Exe を実行するには、次のようにします。  
  
1. Retryado2.exe バイナリをコンパイルしたコンソールウィンドウを開きます。  
2. 入力パラメーターを使用せずに Retryado2.exe を実行します。  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>手順 3: 再試行ロジックをテストする方法  
  
一時エラーをシミュレートして再試行ロジックをテストするには、さまざまな方法があります。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>手順 3. a: テスト例外をスローする  
  
このコードサンプルには次のものが含まれます。  
  
- **TestSqlException**という小さい2番目のクラス。 **Number**という名前のプロパティがあります。  
- `//throw new TestSqlException(4060);`。コメントを解除できます。  
  
Throw ステートメントのコメントを解除して再コンパイルすると、次の**retryado2.exe**の実行時に次のような内容が出力されます。  
  
```  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>> RetryAdo2.exe  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 2 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 3 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 4 of 4 max...  
4060: transient occurred. (TESTING.)  
ERROR: Unable to access the database!  
  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>手順 3. b: 永続的なエラーで再テストする  
  
コードが永続的なエラーを正しく処理することを証明するには、前のテストを再実行します。ただし、4060のような実際の一時的なエラーの数は使用しないようにします。 代わりに、数字7654321を使用します。 プログラムはこれを永続的なエラーとして扱い、再試行をすべてバイパスする必要があります。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>手順 3. c: ネットワークから切断する  
  
1. クライアントコンピューターをネットワークから切断します。  
    - デスクトップの場合は、ネットワークケーブルを取り外します。  
    - ラップトップの場合は、キーの関数の組み合わせを押して、ネットワークアダプターをオフにします。  
2. Retryado2.exe を起動し、コンソールが最初の一時的なエラー (11001 など) を表示するのを待ちます。  
3. ネットワークに再接続し、Retryado2.exe は実行を継続します。  
4. 次回の再試行で、コンソールの成功を確認します。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>手順 2. d: サーバー名を一時的にスペルミスにする  
  
1. 一時的に40615を別のエラー番号として一時的に追加し**てから、** 再コンパイルします。  
2. `new QC.SqlConnectionStringBuilder()` 行にブレークポイントを設定します。  
3. 次のように、*エディットコンティニュ*機能を使用して、サーバー名を意図的に間違えます。  
    - プログラムを実行して、ブレークポイントに戻ります。  
    - エラー40615が発生します。  
4. スペルミスを修正します。  
5. プログラムを正常に実行して完了させます。  
6. 40615を削除し、再コンパイルします。  
  
## <a name="next-steps"></a>次の手順  
  
その他のベスト practicies と設計ガイドラインについては、「 [SQL Database への接続: リンク、ベストプラクティス、設計ガイドライン](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)」を参照してください。  
