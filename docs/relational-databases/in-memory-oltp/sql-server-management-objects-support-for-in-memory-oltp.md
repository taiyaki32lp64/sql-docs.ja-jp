---
title: SQL Server 管理オブジェクトのサポート - インメモリ OLTP
description: インメモリ OLTP をサポートする SQL Server 管理オブジェクト (SMO) の項目について説明します。
ms.custom: seo-dt-2019
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2b67292d-6d8e-4016-9063-a97461ffe57a
author: CarlRabeler
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a49c0a75a67e524475a8a1db7c4905c6490c85fc
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412538"
---
# <a name="sql-server-management-objects-support-for-in-memory-oltp"></a>インメモリ OLTP に対する SQL Server 管理オブジェクトのサポート
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
このトピックでは、インメモリ OLTP をサポートする SQL Server 管理オブジェクト (SMO) の項目について説明します。  

## <a name="smo-types-and-members"></a>SMO の型とメンバー

次の型とメンバーは、名前空間 **Microsoft.SqlServer.Management.Smo** 内にあり、インメモリ OLTP をサポートしています。

- **<xref:Microsoft.SqlServer.Management.Smo.DurabilityType>** (列挙体)
- FileGroup. **<xref:Microsoft.SqlServer.Management.Smo.FileGroup.FileGroupType%2A>** (プロパティ)
- FileGroup. **<xref:Microsoft.SqlServer.Management.Smo.FileGroup.%23ctor%2A>** (コンストラクター)
- **<xref:Microsoft.SqlServer.Management.Smo.FileGroupType>** (列挙体)
- Index. **<xref:Microsoft.SqlServer.Management.Smo.Index.BucketCount%2A>** (プロパティ)
- IndexType. **<xref:Microsoft.SqlServer.Management.Smo.IndexType.NonClusteredHashIndex>** (列挙体メンバー)
- Index. **<xref:Microsoft.SqlServer.Management.Smo.Index.IsMemoryOptimized%2A>** (プロパティ)
- Server. **<xref:Microsoft.SqlServer.Management.Smo.Server.IsXTPSupported%2A>** (プロパティ)
- StoredProcedure. **<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.IsNativelyCompiled%2A>** (プロパティ)
- StoredProcedure. **<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.IsSchemaBound%2A>** (プロパティ)
- Table. **<xref:Microsoft.SqlServer.Management.Smo.Table.Durability%2A>** (プロパティ)
- Table. **<xref:Microsoft.SqlServer.Management.Smo.Table.IsMemoryOptimized%2A>** (プロパティ)
- UserDefinedTableType. **<xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType.IsMemoryOptimized%2A>** (プロパティ)

## <a name="c-code-example"></a>C# コード例

#### <a name="assemblies-referenced-by-the-compiled-code-example"></a>コンパイル済みのコード サンプルで参照されているアセンブリ

- Microsoft.SqlServer.ConnectionInfo.dll
- Microsoft.SqlServer.Management.Sdk.Sfc.dll
- Microsoft.SqlServer.Smo.dll
- Microsoft.SqlServer.SqlEnum.dll

#### <a name="actions-taken-in-the-code-example"></a>コード サンプルで実行されるアクション

1. メモリ最適化ファイル グループとメモリ最適化ファイルが含まれるデータベースを作成します。  
2. 主キー、非クラスター化インデックス、および非クラスター化ハッシュ インデックスが設定された持続性のあるメモリ最適化テーブルを作成します。  
3. 列とインデックスを作成します。  
4. ユーザー定義のメモリ最適化テーブル型を作成します。  
5. ネイティブ コンパイル ストアド プロシージャを作成します。

#### <a name="source-code"></a>ソース コード
  
```csharp
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   static void Main(string[] args) {  
      Server server = new Server("(local)");  
  
      // Create a database with memory-optimized filegroup and memory-optimized file.
      Database db = new Database(server, "MemoryOptimizedDatabase");  
      db.Create();  
      FileGroup fg = new FileGroup(
         db,
         "memOptFilegroup",
         FileGroupType.MemoryOptimizedDataFileGroup);  
      db.FileGroups.Add(fg);  
      fg.Create();  
      // Change this path if needed.
      DataFile file = new DataFile(
         fg,
         "memOptFile",
         @"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\MSSQLmemOptFileName");  
      file.Create();  
  
      // Create a durable memory-optimized table with primary key, nonclustered index and nonclustered hash index.
      // Define the table as memory optimized and set the durability.
      Table table = new Table(db, "memOptTable");  
      table.IsMemoryOptimized = true;  
      table.Durability = DurabilityType.SchemaAndData;  
  
      // Create columns.
      Column col1 = new Column(table, "col1", DataType.Int);  
      col1.Nullable = false;  
      table.Columns.Add(col1);  
      Column col2 = new Column(table, "col2", DataType.Float);  
      col2.Nullable = false;  
      table.Columns.Add(col2);  
      Column col3 = new Column(table, "col3", DataType.Decimal(2, 10));  
      col3.Nullable = false;  
      table.Columns.Add(col3);  
  
      // Create indexes.
      Index pk = new Index(table, "PK_memOptTable");  
      pk.IndexType = IndexType.NonClusteredIndex;  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      pk.IndexedColumns.Add(new IndexedColumn(pk, col1.Name));  
      table.Indexes.Add(pk);  
  
      Index ixNonClustered = new Index(table, "ix_nonClustered");  
      ixNonClustered.IndexType = IndexType.NonClusteredIndex;  
      ixNonClustered.IndexKeyType = IndexKeyType.None;  
      ixNonClustered.IndexedColumns.Add(
         new IndexedColumn(ixNonClustered, col2.Name));  
      table.Indexes.Add(ixNonClustered);  
  
      Index ixNonClusteredHash = new Index(table, "ix_nonClustered_Hash");  
      ixNonClusteredHash.IndexType = IndexType.NonClusteredHashIndex;  
      ixNonClusteredHash.IndexKeyType = IndexKeyType.None;  
      ixNonClusteredHash.BucketCount = 1024;  
      ixNonClusteredHash.IndexedColumns.Add(
         new IndexedColumn(ixNonClusteredHash, col3.Name));  
      table.Indexes.Add(ixNonClusteredHash);  
  
      table.Create();  
  
      // Create a user-defined memory-optimized table type.
      UserDefinedTableType uDTT = new UserDefinedTableType(db, "memOptUDTT");  
      uDTT.IsMemoryOptimized = true;  
  
      // Add columns.
      Column udTTCol1 = new Column(uDTT, "udtCol1", DataType.Int);  
      udTTCol1.Nullable = false;  
      uDTT.Columns.Add(udTTCol1);  
      Column udTTCol2 = new Column(uDTT, "udtCol2", DataType.Float);  
      udTTCol2.Nullable = false;  
      uDTT.Columns.Add(udTTCol2);  
      Column udTTCol3 = new Column(uDTT, "udtCol3", DataType.Decimal(2, 10));  
      udTTCol3.Nullable = false;  
      uDTT.Columns.Add(udTTCol3);  
  
      // Add index.
      Index ix = new Index(uDTT, "IX_UDT");  
      ix.IndexType = IndexType.NonClusteredHashIndex;  
      ix.BucketCount = 1024;  
      ix.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      ix.IndexedColumns.Add(new IndexedColumn(ix, udTTCol1.Name));  
      uDTT.Indexes.Add(ix);  
  
      uDTT.Create();  
  
      // Create a natively compiled stored procedure.
      StoredProcedure sProc = new StoredProcedure(db, "nCSProc");  
      sProc.TextMode = false;  
      sProc.TextBody = "--Type body here";  
      sProc.IsNativelyCompiled = true;  
      sProc.IsSchemaBound = true;  
      sProc.ExecutionContext = ExecutionContext.Owner;  
      sProc.Create();  
   }  
}  
```  
  
## <a name="see-also"></a>参照  

- [SQL Server によるインメモリ OLTP のサポート](sql-server-support-for-in-memory-oltp.md)
- [SMO の概要](../server-management-objects-smo/overview-smo.md)
