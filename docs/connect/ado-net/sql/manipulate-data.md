---
title: データの操作
description: MARS アプリケーションのコーディング例を示します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: df430bbacb69e1d95d001e4f9340ca60473503cd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452165"
---
# <a name="manipulating-data"></a>データの操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

複数のアクティブな結果セット (MARS) を導入する前に、開発者は複数の接続またはサーバー側のカーソルを使用して、特定のシナリオを解決する必要がありました。 さらに、トランザクションの状況で複数の接続を使用するときは、接続をバインド (**sp_getbindtoken** と **sp_bindsession**) する必要がありました。 次のシナリオは、複数の接続ではなく、MARS が有効な接続を使用する方法を示しています。  
  
## <a name="using-multiple-commands-with-mars"></a>MARS で複数のコマンドを使用する  
次のコンソールアプリケーションは、2つの <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトを使用して、<xref:Microsoft.Data.SqlClient.SqlCommand> 2 つのオブジェクトと MARS が有効になっている1つの <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを使用する方法を示しています。  
  
### <a name="example"></a>例  
この例では、 **AdventureWorks**データベースへの単一の接続を開きます。 <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを使用すると、<xref:Microsoft.Data.SqlClient.SqlDataReader> が作成されます。 リーダーが使用されると、2番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> が開き、2番目のリーダーの WHERE 句への入力として最初の <xref:Microsoft.Data.SqlClient.SqlDataReader> のデータが使用されます。  
  
> [!NOTE]
>  次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプルコードに示されている接続文字列は、データベースがローカルコンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、環境に合わせて接続文字列を変更します。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>MARS を使用したデータの読み取りと更新  
MARS を使用すると、複数の保留中の操作で、読み取り操作と DML (データ操作言語) 操作の両方に接続を使用できます。 この機能により、アプリケーションが接続ビジーエラーを処理する必要がなくなります。 さらに、MARS を使用すると、サーバー側カーソルのユーザーを置き換えることができます。この場合、通常はより多くのリソースが消費されます。 最後に、複数の操作を単一の接続で実行できるので、同じトランザクション コンテキストを共有することにより、システムのストアド プロシージャである **sp_getbindtoken** と **sp_bindsession** を使用する必要がなくなります。  
  
### <a name="example"></a>例  
次のコンソールアプリケーションは、3つの <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを持つ2つの <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトと、MARS が有効になっている1つの <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを使用する方法を示しています。 最初のコマンドオブジェクトは、信用格付けが5であるベンダーの一覧を取得します。 2番目のコマンドオブジェクトは、<xref:Microsoft.Data.SqlClient.SqlDataReader> から提供されているベンダ ID を使用して、特定のベンダのすべての製品を含む2番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> を読み込みます。 各製品レコードは、2番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> によってアクセスされます。 計算が実行され、新規 **OnOrderQty** を判定します。 3 番目のコマンド オブジェクトでは、**ProductVendor** テーブルを新しい値で更新します。 このプロセス全体は、1つのトランザクション内で実行され、最後にロールバックされます。  
  
> [!NOTE]
>  次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプルコードに示されている接続文字列は、データベースがローカルコンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、環境に合わせて接続文字列を変更します。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [複数のアクティブな結果セット (MARS)](multiple-active-result-sets-mars.md)
