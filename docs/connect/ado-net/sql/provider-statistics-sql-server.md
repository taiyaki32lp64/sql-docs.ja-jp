---
title: SQL Server のプロバイダー統計情報
description: SQL Server の実行時の統計情報を取得するためのサポートについて説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 092cf63e62bce01e2a771ce4e5f7f46e1073e91a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452065"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server のプロバイダー統計情報

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

.NET Framework バージョン2.0 および .NET Core バージョン1.0 以降では、SQL Server 用の Microsoft SqlClient Data Provider で実行時の統計情報がサポートされます。 有効な接続オブジェクトを作成した後で、<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> プロパティを `True` に設定して、統計を有効にする必要があります。 統計情報が有効になったら、<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> メソッドを使用して <xref:System.Collections.IDictionary> 参照を取得することにより、それらを "時間内のスナップショット" として確認できます。 リストは、名前と値のペアのディクショナリエントリのセットとして列挙されます。 これらの名前と値のペアは順序付けされていません。 いつでも、<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> メソッドを呼び出して、カウンターをリセットできます。 統計情報の収集が有効になっていない場合、例外は生成されません。 また、最初にを呼び出さ <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> ずに <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> が呼び出された場合、取得される値は各エントリの初期値になります。 統計を有効にし、アプリケーションをしばらく実行してから統計を無効にした場合、取得される値には、統計が無効になった時点までに収集された値が反映されます。 収集されるすべての統計値は、接続ごとに行われます。  
  
## <a name="statistical-values-available"></a>使用可能な統計値  
現在、Microsoft SQL Server プロバイダーから18個の異なる項目を使用できます。 使用できる項目の数を確認するには、<xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> により返される <xref:System.Collections.IDictionary> インターフェイス参照の **Count** プロパティを使用します。 プロバイダーの統計情報のカウンターはすべて、64 ビット幅である共通言語ランタイムの <xref:System.Int64> 型 (C# と Visual Basic の場合は **long**) を使用します。 **int64** データ型の最大値は、**int64.MaxValue** フィールドにより定義されているように、((2^63)-1)) です。 カウンターの値がこの最大値になると、正確ではないと見なされます。 つまり、**int64.MaxValue**-1((2^63)-2) は、事実上、すべての統計情報について有効な値の最大値になります。  
  
> [!NOTE]
>  返される統計の数、名前、および順序は将来変更される可能性があるため、プロバイダーの統計情報を返すには、ディクショナリを使用します。 アプリケーションは、ディクショナリにある特定の値に依存しないようにする必要がありますが、その値が存在するかどうかを確認し、それに応じて分岐する必要があります。  
  
次の表では、使用できる現在の統計値について説明します。 個々の値のキー名は、Microsoft .NET Framework および .NET Core の地域バージョン間でローカライズされていないことに注意してください。  
  
|キーの名前|[説明]|  
|--------------|-----------------|  
|`BuffersReceived`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に SQL Server からプロバイダーによって受信された表形式のデータストリーム (TDS) パケットの数を返します。|  
|`BuffersSent`|統計が有効になった後にプロバイダーによって SQL Server に送信された TDS パケットの数を返します。 大きいコマンドでは、複数のバッファーが必要になる場合があります。 たとえば、大きなコマンドがサーバーに送信され、6個のパケットが必要な場合、`ServerRoundtrips` は1ずつインクリメントされ、`BuffersSent` は6ずつインクリメントされます。|  
|`BytesReceived`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に SQL Server からプロバイダーによって受信された TDS パケット内のデータのバイト数を返します。|  
|`BytesSent`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後、TDS パケットで SQL Server に送信されるデータのバイト数を返します。|  
|`ConnectionTime`|統計情報が有効になった後に接続が開かれている時間の長さ (ミリ秒単位) を示します (接続が開かれる前に統計情報が有効になっていた場合は、合計接続時間を示します)。|  
|`CursorOpens`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を介してカーソルが開かれた回数を返します。<br /><br /> SELECT ステートメントによって返される読み取り専用/順方向専用の結果は、カーソルとは見なされないため、このカウンターには影響しません。|  
|`ExecutionTime`|統計情報が有効になってから、プロバイダーが処理に費やした累計時間 (ミリ秒単位) を返します。この時間には、サーバーからの応答を待つために費やされた時間と、プロバイダー自体がコードを実行するために費やした時間が含まれます。<br /><br /> タイミング コードを含むクラスは次のとおりです。<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> パフォーマンス クリティカルなメンバーを可能な限り小さく維持するために、次のメンバーは時間指定されません。<br /><br /> SqlDataReader<br /><br /> this[] 演算子 (すべてのオーバーロード)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を介して実行された INSERT、DELETE、および UPDATE ステートメントの合計数を返します。|  
|`IduRows`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を介して実行された INSERT、DELETE、および UPDATE ステートメントの影響を受ける行の合計数を返します。|  
|`NetworkServerTime`|アプリケーションがプロバイダーを使って開始され、統計情報が有効になった後にプロバイダーがサーバーからの応答を待つために費やした累計時間 (ミリ秒単位) を返します。|  
|`PreparedExecs`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を通じて実行された準備されたコマンドの数を返します。|  
|`Prepares`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を通じて準備されたステートメントの数を返します。|  
|`SelectCount`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を通じて実行された SELECT ステートメントの数を返します。 これには、カーソルから行を取得するための FETCH ステートメントが含まれており、<xref:Microsoft.Data.SqlClient.SqlDataReader> の末尾に達したときに SELECT ステートメントの数が更新されます。|  
|`SelectRows`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に選択された行の数を返します。 このカウンターは、SQL ステートメントによって生成されたすべての行を反映します。これは、呼び出し元によって実際に使用されていない行も同様です。 たとえば、結果セット全体を読み取る前にデータリーダーを終了しても、カウントには影響しません。 これには、FETCH ステートメントを通じてカーソルから取得される行が含まれます。|  
|`ServerRoundtrips`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続がサーバーにコマンドを送信し、応答を返した回数を返します。|  
|`SumResultSets`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に使用された結果セットの数を返します。 たとえば、クライアントに返される結果セットが含まれます。 カーソルの場合、各フェッチまたはブロックフェッチ操作は、独立した結果セットと見なされます。|  
|`Transactions`|アプリケーションがプロバイダーを使用して開始され、ロールバックを含む統計を有効にした後に開始されたユーザートランザクションの数を返します。 自動コミットをオンにして接続が実行されている場合、各コマンドはトランザクションと見なされます。<br /><br /> このカウンターは、トランザクションがコミットされるか、後でロールバックされるかに関係なく、BEGIN TRAN ステートメントが実行されるとすぐにトランザクション数をインクリメントします。|  
|`UnpreparedExecs`|アプリケーションがプロバイダーを使用して開始され、統計情報が有効になった後に、接続を介して実行されていないステートメントの数を返します。|  
  
### <a name="retrieving-a-value"></a>値の取得  
次のコンソールアプリケーションは、接続の統計を有効にし、4つの統計値を取得して、コンソールウィンドウに書き込む方法を示しています。  
  
> [!NOTE]
>  次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプルコードに示されている接続文字列は、データベースがローカルコンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、環境に合わせて接続文字列を変更します。  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>すべての値の取得  
次のコンソールアプリケーションは、接続の統計を有効にする方法、列挙子を使用して使用可能なすべての統計値を取得する方法、およびそれらをコンソールウィンドウに書き込む方法を示しています。  
  
> [!NOTE]
>  次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプルコードに示されている接続文字列は、データベースがローカルコンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、環境に合わせて接続文字列を変更します。  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
