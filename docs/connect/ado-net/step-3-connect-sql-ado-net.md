---
title: 'ステップ 3: ADO.NET を使用した SQL への接続を概念実証する | Microsoft Docs'
description: SQL Server C#に接続し、クエリを実行し、行を挿入するためのコード例を示します。
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 2819697746f810e0c0b19a9ab7d076fa79c15a2f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451817"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>ステップ 3: ADO.NET を使用した SQL への接続を概念実証する

![Download-DownArrow-Circled](../../ssdt/media/download.png)[ADO.NET をダウンロードする](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- 前の記事:&nbsp;&nbsp;&nbsp;[ステップ 2: ADO.NET 開発用の SQL データベースを作成する](step-2-create-sql-database-ado-net-development.md)  
- 次の記事:&nbsp;&nbsp;&nbsp;[ステップ 4: ADO.NET で SQL に弾性的に接続する](step-4-connect-resiliently-sql-ado-net.md)  

  
この C# コードの例は、概念実証としてのみ検討してください。 わかりやすさのためにサンプル コードは簡略化されており、Microsoft が推奨するベスト プラクティスを表しているとは限りません。  
  
## <a name="step-1-connect"></a>手順 1: 接続する
  
このメソッドは、SQL データベースへの接続に使用されます **。**  


```csharp
// C# , ADO.NET  
using System;
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  

                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
Press any key to finish...  
****/  
```  


## <a name="step-2-execute-a-query"></a>手順 2: クエリの実行  
  
ExecuteReader メソッド:  
  
- Sql の SELECT ステートメントを SQL システムに発行します。  
- 結果行へのアクセスを提供する SqlDataReader のインスタンスを返します。  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.SelectRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void SelectRows(QC.SqlConnection connection)  
        {  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
SELECT  
    TOP 5  
        COUNT(soh.SalesOrderID) AS [OrderCount],  
        c.CustomerID,  
        c.CompanyName  
    FROM  
                        SalesLT.Customer         AS c  
        LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh  
            ON c.CustomerID = soh.CustomerID  
    GROUP BY  
        c.CustomerID,  
        c.CompanyName  
    ORDER BY  
        [OrderCount] DESC,  
        c.CompanyName; ";  
  
                QC.SqlDataReader reader = command.ExecuteReader();  
  
                while (reader.Read())  
                {  
                    Console.WriteLine("{0}\t{1}\t{2}",  
                        reader.GetInt32(0),  
                        reader.GetInt32(1),  
                        reader.GetString(2));  
                }  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
1       29736   Action Bicycle Specialists  
1       29638   Aerobic Exercise Company  
1       29546   Bulk Discount Store  
1       29741   Central Bicycle Specialists  
1       29612   Channel Outlet  
Press any key to finish...  
****/  
```  
  
  
  
## <a name="step-3-insert-a-row"></a>手順 3: 行を挿入する  
  
  
この例では、次の方法を示します。  
  
- パラメーターを渡すことにより、SQL INSERT ステートメントを安全に実行します。  
  - パラメーターを使用すると、SQL インジェクション攻撃を防ぐことができます。  
- 自動生成された値を取得します。  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.InsertRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void InsertRows(QC.SqlConnection connection)  
        {  
            QC.SqlParameter parameter;  
  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
INSERT INTO SalesLT.Product  
        (Name,  
        ProductNumber,  
        StandardCost,  
        ListPrice,  
        SellStartDate  
        )  
    OUTPUT  
        INSERTED.ProductID  
    VALUES  
        (@Name,  
        @ProductNumber,  
        @StandardCost,  
        @ListPrice,  
        CURRENT_TIMESTAMP  
        ); ";  
  
                parameter = new QC.SqlParameter("@Name", DT.SqlDbType.NVarChar, 50);  
                parameter.Value = "SQL Server Express 2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ProductNumber", DT.SqlDbType.NVarChar, 25);  
                parameter.Value = "SQLEXPRESS2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@StandardCost", DT.SqlDbType.Int);  
                parameter.Value = 11;  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ListPrice", DT.SqlDbType.Int);  
                parameter.Value = 12;  
                command.Parameters.Add(parameter);  
  
                int productId = (int)command.ExecuteScalar();  
                Console.WriteLine("The generated ProductID = {0}.", productId);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
The generated ProductID = 1000.  
Press any key to finish...  
****/  
```
