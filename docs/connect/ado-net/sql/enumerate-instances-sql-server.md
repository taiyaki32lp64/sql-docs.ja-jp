---
title: SQL Server のインスタンスの列挙 (ADO.NET)
description: SQL Server のアクティブなインスタンスを一覧化する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d6c83ffd407a9b27a04b254fb3e9e5673a600417
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452205"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>SQL Server のインスタンスの列挙 (ADO.NET)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server を使うと、アプリケーションは現在のネットワーク内の SQL Server インスタンスを検索できます。 <xref:System.Data.Sql.SqlDataSourceEnumerator> クラスは、この情報をアプリケーション開発者に公開し、表示されているすべてのサーバーに関する情報を含む <xref:System.Data.DataTable> を提供します。 このときに返されるテーブルには、ユーザーが新しい接続を作成しようとして、 **[接続プロパティ]** ダイアログ ボックスで、利用可能なすべてのサーバーが含まれたドロップダウン リストを展開したときに表示されるリストと一致するサーバー インスタンスのリストが含まれています。 表示される結果は、必ずしも完全ではありません。  
  
> [!NOTE]
>  ほとんどの Windows サービスと同様に、最小限の特権で SQL Browser サービスを実行することをお勧めします。 SQL Browser サービスの詳細および SQL Browser サービスの動作を管理する方法については、SQL Server オンライン ブックを参照してください。  
  
## <a name="retrieving-an-enumerator-instance"></a>列挙子インスタンスを取得する  
使用可能な SQL Server インスタンスに関する情報を含むテーブルを取得するには、まず、共有プロパティまたは静的プロパティである <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> プロパティを使用して列挙子を取得する必要があります。  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
静的インスタンスを取得したら、<xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> メソッドを呼び出すことができます。このメソッドは、使用可能なサーバーに関する情報を含む <xref:System.Data.DataTable> を返します。  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
メソッド呼び出しから返されたテーブルには、次の列が含まれています。すべての列には `string` 値が含まれています。  
  
|[列]|[説明]|  
|------------|-----------------|  
|**ServerName**|サーバー名。|  
|**InstanceName**|サーバーインスタンスの名前。 サーバーが既定のインスタンスとして実行されている場合は空白になります。|  
|**IsClustered**|サーバーがクラスターの一部であるかどうかを示します。|  
|**Version**|サーバーのバージョン。 例:<br /><br /> -   9.00.x (SQL Server 2005)<br />-10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>列挙の制限事項  
使用可能なすべてのサーバーが一覧に表示される場合と表示されない場合があります。 この一覧は、タイムアウトやネットワークトラフィックなどの要因によって異なります。 これにより、2回の連続した呼び出しでリストが異なる場合があります。 同じネットワーク上のサーバーのみが表示されます。 ブロードキャストパケットは通常、ルーターをスキャンしません。そのため、サーバーが一覧に表示されない場合がありますが、呼び出し全体で安定します。  
  
一覧表示されたサーバーには、`IsClustered` やバージョンなどの追加情報が含まれている場合があります。 これは、リストの取得方法によって異なります。 SQL Server Browser サービスを介して一覧に表示されるサーバーには、一覧に名前しか表示されない、Windows インフラストラクチャを介して検索されたサーバーより多くの詳細情報が含まれています。  
  
> [!NOTE]
>  サーバー列挙は、完全信頼で実行されている場合にのみ使用できます。 部分的に信頼された環境で実行されているアセンブリは、<xref:Microsoft.Data.SqlClient.SqlClientPermission> コードアクセスセキュリティ (CAS) のアクセス許可を持っている場合でも、使用できません。  
  
SQL Server では、SQL Browser という名前の外部の Windows サービスを利用して、<xref:System.Data.Sql.SqlDataSourceEnumerator> に情報を提供します。 このサービスは既定で有効になっていますが、管理者はこのサービスを無効または無効にして、サーバーインスタンスがこのクラスに表示されないようにすることができます。  
  
## <a name="example"></a>例  
次のコンソール アプリケーションは、表示可能なすべての SQL Server インスタンスに関する情報を取得し、その情報をコンソール ウィンドウに表示します。  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
