---
title: 大きな UDT
description: SQL Server 2008 で導入された大きな値の Udt からデータを取得する方法を示します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4ea2c0002ceb01606cdf51f04246abcdc74429e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452155"
---
# <a name="large-udts"></a>大きな UDT

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ユーザー定義型 (UDT) を利用することで、開発者は共通言語ランタイム (CLR) のオブジェクトを SQL Server データベースに格納することによってサーバーのスカラー型システムを拡張できます。 UDT は複数の要素を持つことができ、動作を定義できます。この点は、1 つの SQL Server システム データ型から構成される従来の別名データ型と異なります。  
  
従来、UDT のサイズは最大 8 KB に制限されていました。 SQL Server 2008 では、<xref:Microsoft.Data.SqlClient.Server.Format.UserDefined> 形式の UDT では、この制限が廃止されています。  
  
ユーザー定義型の完全なドキュメントについては、「SQL Server オンラインブックの[CLR ユーザー定義型](https://go.microsoft.com/fwlink/?LinkId=98366)」を参照してください。
  
## <a name="retrieving-udt-schemas-using-getschema"></a>GetSchema を使用した UDT スキーマの取得  
<xref:Microsoft.Data.SqlClient.SqlConnection> の <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> メソッドは、<xref:System.Data.DataTable> 内のデータベーススキーマ情報を返します。
  
### <a name="getschematable-column-values-for-udts"></a>Udt の GetSchemaTable 列の値  
<xref:Microsoft.Data.SqlClient.SqlDataReader> の <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> メソッドは、列のメタデータを記述する <xref:System.Data.DataTable> を返します。 次の表では、SQL Server 2005 と SQL Server 2008 の間の大きな Udt の列メタデータの違いについて説明します。  
  
|SqlDataReader 列|SQL Server 2005|SQL Server 2008 以降|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|場合により異なる|場合により異なる|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|UDT インスタンス|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|UDT インスタンス|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|3 つの部分から成る名前 (*Database.SchemaName.TypeName* として指定)|  
|`IsLong`|場合により異なる|場合により異なる|  
  
## <a name="sqldatareader-considerations"></a>SqlDataReader に関する考慮事項  
SQL Server 2008 以降、<xref:Microsoft.Data.SqlClient.SqlDataReader> は大きな UDT 値を取得できるように拡張されました。 <xref:Microsoft.Data.SqlClient.SqlDataReader> によって処理される UDT 値の大きさは、接続文字列で指定されている `Type System Version` に加えて、使用している SQL Server のバージョンによって異なります。 詳細については、「 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>に評価されるまで、タスクを繰り返します。  
  
次の <xref:Microsoft.Data.SqlClient.SqlDataReader> のメソッドは、`Type System Version` が SQL Server 2005 に設定されている場合に、UDT ではなく <xref:System.Data.SqlTypes.SqlBinary> を返します。  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
次のメソッドは、`Type System Version` が SQL Server 2005 に設定されている場合に、UDT ではなく `Byte[]` の配列を返します。  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
現在のバージョンの ADO.NET の変換は行われないことに注意してください。  
  
## <a name="specifying-sqlparameters"></a>SqlParameters の指定  
次の <xref:Microsoft.Data.SqlClient.SqlParameter> プロパティは、大きな Udt で動作するように拡張されています。  
  
|SqlParameter プロパティ|[説明]|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|パラメーターの値を表すオブジェクトを取得または設定します。 既定値は null です。 このプロパティは、`SqlBinary`、`Byte[]`、またはマネージド オブジェクトになります。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|パラメーターの値を表すオブジェクトを取得または設定します。 既定値は null です。 このプロパティは、`SqlBinary`、`Byte[]`、またはマネージド オブジェクトになります。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|解決するパラメーター値のサイズを取得または設定します。 既定値は 0 です。 プロパティには、パラメーター値のサイズを表す整数を指定できます。 大きな UDT の場合は UDT の実際のサイズに、不明な場合は -1 になります。|  
  
## <a name="retrieving-data-example"></a>データの取得の例  
次のコードフラグメントは、大きな UDT データを取得する方法を示しています。 `connectionString` 変数は、SQL Server データベースへの有効な接続を想定しています。 `commandString` 変数は、主キー列が最初に指定された有効な SELECT ステートメントであることを前提としています。  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-large-value-data.md)
