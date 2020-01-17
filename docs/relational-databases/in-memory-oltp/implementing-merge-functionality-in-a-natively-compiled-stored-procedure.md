---
title: MERGE 機能 - ネイティブ コンパイル ストアド プロシージャ
ms.custom: seo-dt-2019
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 811b3dfbd79e60d5fb626f814f7b4bf38272fd19
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412643"
---
# <a name="implementing-merge-functionality-in-a-natively-compiled-stored-procedure"></a>ネイティブ コンパイル ストアド プロシージャに MERGE 機能を実装する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
このセクションに収録した Transact-SQL のコード サンプルでは、ネイティブ コンパイル モジュールで T-SQL の MERGE ステートメントをシミュレートする方法を示します。 サンプルでは、ID 列を持つテーブル変数を使用してテーブル変数内の行を反復処理し、各行について、条件が一致した場合は更新を、条件が一致しない場合は挿入を実行します。
  
ネイティブ プロセス内でサポートして、コード サンプルでシミュレートする、T-SQL の MERGE ステートメントを次に示します。  
  
  
  
  
    MERGE INTO dbo.Table1 t  
        USING @tvp v  
        ON t.Column1 = v.c1  
        WHEN MATCHED THEN   
            UPDATE SET Column2 = v.c2  
        WHEN NOT MATCHED THEN  
            INSERT (Column1, Column2) VALUES (v.c1, v.c2);  
  
  
  
  
回避策を実現し、MERGE をシミュレートする T-SQL を次に示します。  
  
  
  
  
    DROP PROCEDURE IF EXISTS dbo.usp_merge1;  
    go  
    DROP TYPE IF EXISTS dbo.Type1;  
    go  
    DROP TABLE IF EXISTS dbo.Table1;  
    go  
    -----------------------------  
    -- target table and table type used for the workaround
    -----------------------------  
  
    CREATE TABLE dbo.Table1  
    (  
        Column1  INT  NOT NULL  PRIMARY KEY NONCLUSTERED,  
        Column2  INT  NOT NULL  
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
  
    CREATE TYPE dbo.Type1 AS TABLE  
    (  
        c1  INT  NOT NULL,  
        c2  INT  NOT NULL,  
  
        RowID    INT  NOT NULL  IDENTITY(1,1),  
        INDEX ix_RowID HASH (RowID) WITH (BUCKET_COUNT=1024)  
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
    -----------------------------  
    -- stored procedure implementing the workaround
    -----------------------------  
  
    CREATE PROCEDURE dbo.usp_merge1   
        @tvp1 dbo.Type1 READONLY  
        WITH  
        NATIVE_COMPILATION, SCHEMABINDING  
    AS   
    BEGIN ATOMIC  
        WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
              LANGUAGE = N'us_english')  

        DECLARE  @i INT = 1,  @c1 INT,  @c2 INT;  
    
        WHILE @i > 0  
        BEGIN  
            SELECT @c1 = c1, @c2 = c2  
                FROM @tvp1  
                WHERE RowID = @i;  
    
            --test whether the row exists in the TVP; if not, we end the loop
            IF @@ROWCOUNT=0  
                SET @i = 0
            ELSE
            BEGIN
                -- try the update
                UPDATE dbo.Table1  
                    SET   Column2 = @c2  
                    WHERE Column1 = @c1;  
    
                -- if there was no row to update, we insert
                IF @@ROWCOUNT=0  
                    INSERT INTO dbo.Table1 (Column1, Column2)  
                        VALUES (@c1, @c2);  
    
                SET @i += 1
            END
        END  
    END  
    go  
    -----------------------------  
    -- test to validate the functionality
    -----------------------------  
  
    INSERT dbo.Table1 VALUES (1,2);  
    go  
  
    SELECT N'Before-MERGE' AS [Before-MERGE], Column1, Column2  
        FROM dbo.Table1;  
    go  
  
    DECLARE @tvp1 dbo.Type1;  
  
    INSERT @tvp1 (c1, c2) VALUES (1,33), (2,4);  
    EXECUTE dbo.usp_merge1 @tvp1;  
    go  
  
    SELECT N'After--MERGE' AS [After--MERGE], Column1, Column2  
        FROM dbo.Table1;  
    go  
    -----------------------------  

  
    /****  Actual output:  
  
    Before-MERGE   Column1   Column2  
    Before-MERGE      1         2  
  
    After--MERGE   Column1   Column2  
    After--MERGE      1        33  
    After--MERGE      2         4  
    ****/  
  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [インメモリ OLTP でサポートされていない Transact-SQL の構造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
