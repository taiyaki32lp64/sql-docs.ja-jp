---
title: メモリ最適化テーブルの統計 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42b42356331d91683811472b420e656560a77d79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086257"
---
# <a name="statistics-for-memory-optimized-tables"></a>メモリ最適化テーブルの統計
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  クエリ オプティマイザーでは、クエリのパフォーマンスを向上させるクエリ プランを作成するために列に関する統計を使用します。 統計はデータベースのテーブルから収集され、データベース メタデータに格納されます。  
  
 統計は自動的に作成されますが、手動で作成することもできます。 たとえば、統計は、インデックスの作成時にインデックス キー列に対して自動的に作成されます。 統計の作成の詳細については、「 [Statistics](../../relational-databases/statistics/statistics.md)」を参照してください。  
  
 テーブル データは通常、時間の経過に伴い、行が挿入、更新、または削除されて変化します。 これは、統計を定期的に更新する必要があることを意味します。 既定では、テーブルの統計は、統計が古くなったとクエリ オプティマイザーが判断したときに自動的に更新されます。  
  
 メモリ最適化テーブルの統計に関する考慮事項を次に示します。  
  
-   SQL Server 2016 以降、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、データベース互換性レベル 130 以上を使用している場合、メモリ最適化テーブルに対する統計の自動更新がサポートされます。 「 [ALTER DATABASE 互換性レベル (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。 これより低い互換性レベルを使用して以前に作成されたテーブルがデータベースにある場合、今後統計の自動更新を有効にするには、1 回統計を手動で更新する必要があります。
  
-   ネイティブ コンパイル ストアド プロシージャの場合、プロシージャのコンパイル時にプロシージャ内のクエリの実行プランが最適化されます。コンパイルは作成時に実行されます。 統計の更新時に自動的に再コンパイルされることはありません。 したがって、プロシージャが作成される前に、テーブルに代表的なデータのセットが含まれている必要があります。  
  
-   ネイティブ コンパイル ストアド プロシージャは、 [sp_recompile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)を使用して手動で再コンパイルできます。さらに、データベースがオフラインになってからもう一度オンラインに戻った場合、データベース フェールオーバーの場合、またはサーバーが再起動された場合に、自動的に再コンパイルされます。  
  
## <a name="enabling-automatic-update-of-statistics-in-existing-tables"></a>既存のテーブル内の統計の自動更新を有効にする

互換性レベルが 130 以上のデータベース内にテーブルが作成されると、そのテーブル上のすべての統計に対して統計の自動更新が有効になり、それ以上の操作は何も必要ありません。

旧バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成された、あるいは互換性レベルが 130 未満のメモリ最適化テーブルがデータベースにある場合、今後自動更新を有効にするには、1 回統計を手動で更新する必要があります。

前の互換性レベルで作成されたメモリ最適化テーブルに対して統計の自動更新を有効にするには、次の手順を実行します。

1. 次のように、データベースの互換性レベルを更新します。 `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. メモリ最適化テーブルの統計を手動で更新します。 同じ作業を実行するサンプル スクリプトを以下に示します。

3. 更新した統計を活用するように、ネイティブ コンパイル ストアド プロシージャを手動で再コンパイルします。

*統計の 1 回限りのスクリプト:* 下位互換性レベルで作成されたメモリ最適化テーブルに対して、次の Transact-SQL スクリプトを 1 回実行してすべてのメモリ最適化テーブルの統計を更新し、それ以降、統計の自動更新を有効にすることができます (データベースに対して AUTO_UPDATE_STATISTICS が有効になっている必要があります)。

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```

*自動更新が有効になっているかどうかの確認:* 次のスクリプトは、メモリ最適化テーブル上の統計に対して自動更新が有効になっているかどうかを確認します。 前述のスクリプトの実行後、すべての統計オブジェクトについて、 `1` 列に `auto-update enabled` が返されます。

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## <a name="guidelines-for-deploying-tables-and-procedures"></a>テーブルとプロシージャの配置に関するガイドライン  
 クエリ オプティマイザーでクエリ プランを作成するときに最新の統計が使用されるように、次の 4 つの手順を使用して、メモリ最適化テーブルと、そのテーブルにアクセスするネイティブ コンパイル ストアド プロシージャを配置します。  
  
1.  データベースの互換性レベルが 130 以上であることをご確認ください。 「 [ALTER DATABASE 互換性レベル (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。

2.  テーブルとインデックスを作成します。 インデックスは、 **CREATE TABLE** ステートメントにインラインで指定する必要があります。  
  
3.  テーブルにデータを読み込みます。  
  
4.  テーブルにアクセスするストアド プロシージャを作成します。  
  
 データを読み込んでからネイティブ コンパイル ストアド プロシージャを作成することにより、オプティマイザーで統計をメモリ最適化テーブル用に使用できます。 これによって、プロシージャをコンパイルすると効率的なクエリ プランが作成されます。  

## <a name="see-also"></a>参照  
 [メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
