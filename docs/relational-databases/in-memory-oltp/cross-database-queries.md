---
title: 複数データベースのクエリ | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93eae89743c2a4563317614a18e4bf5f46248071
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031983"
---
# <a name="cross-database-queries"></a>複数データベースにまたがるクエリ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降、メモリ最適化テーブルで複数データベースにまたがるトランザクションはサポートされません。 メモリ最適化テーブルにもアクセスする同じトランザクションまたは同じクエリから別のデータベースにアクセスすることはできません。 あるデータベースのテーブルから別のデータベースのメモリ最適化テーブルに、データを簡単にコピーすることはできません。  
  
 テーブル変数はトランザクション処理されません。 そのため、メモリ最適化テーブル変数を複数データベースにまたがるクエリで使用して、あるデータベースのデータを別のデータベースのメモリ最適化テーブルに簡単に移動できるようにすることができます。 2 つのトランザクションを使用できます。 最初のトランザクションで、リモート テーブルから変数にデータを挿入します。 2 つ目のトランザクションで、ローカルなメモリ最適化テーブルに変数からデータを挿入します。  メモリ最適化テーブルの変数の詳細については、「 [Faster temp table and table variable by using memory optimization](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)」 (メモリ最適化を使用した一時テーブルとテーブル変数の高速化) を参照してください。
  
## <a name="example"></a>例
この例は、あるデータベースから別のデータベースにあるメモリ最適化テーブルにデータを転送する方法を示しています。

1. テスト オブジェクトを作成します。  [!INCLUDE[tsql](../../includes/tsql-md.md)] で次の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を実行します。  

    ```sql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  複数のデータベースにまたがるクエリを試行します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] で次の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を実行します。
  
    ```sql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    次のエラー メッセージが表示されます。
    > メッセージ 41317、レベル 16、状態 5  
    > メモリ最適化テーブルまたはネイティブ コンパイル モジュールにアクセスするユーザー トランザクションは、複数のユーザー データベース、model データベース、および msdb データベースにはアクセスできません。また、master データベースに書き込むこともできません。

3.  メモリ最適化テーブル型を作成します。  [!INCLUDE[tsql](../../includes/tsql-md.md)] で次の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を実行します。

    ```sql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  複数のデータベースにまたがるクエリを再試行します。  今度は、ソース データが最初にメモリ最適化テーブルの変数に転送されます。  次にテーブルの変数からメモリ最適化テーブルにデータが転送されます。
    ```sql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
