---
title: Transact-SQL によるインメモリ OLTP のサポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db4c6895fb499458c198008319302a25b8cd34b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156209"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Transact-SQL によるインメモリ OLTP のサポート
  Transact-SQL クエリまたは DML ステートメント (SELECT、INSERT、UPDATE、または DELETE)、アドホック ステートメント、および SQL モジュール (ストアド プロシージャ、テーブル-値関数、スカラー関数、トリガー、ビューなど) を使用して、メモリ最適化テーブルにアクセスできます。 詳細については、次を参照してください。[したテーブルを使用して解釈された TRANSACT-SQL](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)します。  
  
 メモリ最適化テーブルのみを参照するストアド プロシージャは、マシン コードにネイティブ コンパイルできます。これにより、一般に、インタープリタ式の (ディスク ベースの) ストアド プロシージャよりも大幅に高いパフォーマンスが得られます。 メモリ最適化テーブル アクセスを最適化するには、ネイティブ コンパイル ストアド プロシージャを使用します。 詳細については、[ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)を参照してください。  
  
 データベース オブジェクト (DDL ステートメント) を作成および変更する場合に、次のステートメントが修正されました。  
  
-   [ALTER DATABASE の File および Filegroup オプション&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (を参照してください`MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-database-sql-server-transact-sql) (を参照してください`MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE PROCEDURE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-procedure-transact-sql) (を参照してください`NATIVE_COMPILATION`、 `SCHEMABINDING`、 `EXECUTE AS`、および`BEGIN ATOMIC`)  
  
-   [CREATE TABLE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) (を参照してください`MEMORY_OPTIMIZED`、 `DURABILITY`、 `BUCKET_COUNT`、 `INDEX`、および`HASH`)  
  
-   [CREATE TYPE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql) (を参照してください`MEMORY_OPTIMIZED`、 `BUCKET_COUNT`、 `INDEX`、および`HASH`)  
  
-   [宣言@local_variable &#40;TRANSACT-SQL&#41; ](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (を参照してください`NULL`  |  `NOT NULL`)  
  
 メモリ最適化テーブルは、`PRIMARY KEY` および `NOT NULL` の制約をサポートしています。 サポートされていない制約を実装する方法の詳細については、次を参照してください。[移行を確認し、外部キー制約](../../database-engine/migrating-check-and-foreign-key-constraints.md)します。  
  
 サポートされていない機能の詳細については、「[インメモリ OLTP でサポートされていない Transact-SQL の構造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [サポートされるデータ型](supported-data-types-for-in-memory-oltp.md)  
  
-   [解釈された Transact-SQL を使用したメモリ最適化テーブルへのアクセス](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [インメモリ OLTP 向けのシステム ビュー、ストアド プロシージャ、DMV、待機の種類](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](migration-issues-for-natively-compiled-stored-procedures.md)   
 [サポートされている SQL Server の機能](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
