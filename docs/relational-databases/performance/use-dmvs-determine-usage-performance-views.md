---
title: DMV - ビューの使用統計とパフォーマンス
description: DMV を使用してビューの使用統計とパフォーマンスを確認する
ms.custom: seo-dt-2019
author: julieMSFT
ms.author: jrasnick
ms.date: 09/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.openlocfilehash: e80ba0a8252881b7447dda721f02fc9c3e545917
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165891"
---
# <a name="use-dmvs-to-determine-usage-statistics-and-performance-of-views"></a>DMV を使用してビューの使用統計とパフォーマンスを確認する
この記事では、**ビューを使用するクエリのパフォーマンス**に関する情報を取得するために使用する方法とスクリプトについて説明します。 これらのスクリプトの目的は、データベース内のさまざまなビューの使用とパフォーマンスのインジケーターを提供することです。 

## <a name="sysdm_exec_query_optimizer_info"></a>sys.dm_exec_query_optimizer_info
DMV [sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md) では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーによって行われた最適化に関する統計情報が公開されます。 これらの値は累積的であり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に記録を開始します。 クエリ オプティマイザーの詳細については、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)」を参照してください。   

次の common_table_expression (CTE) では、この DMV を使用して、ビューを参照するクエリの割合など、ワークロードに関する情報を提供します。 このクエリによって返される結果では、パフォーマンスの問題自体は示されませんが、クエリのパフォーマンスが悪いというユーザーの不満と組み合わせることで、基になる問題が明らかになります。 

```sql
WITH CTE_QO AS
(
  SELECT
    occurrence
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    ([counter] = 'optimizations')
),
QOInfo AS
(
  SELECT
    [counter]
    ,[%] = CAST((occurrence * 100.00)/(SELECT occurrence FROM CTE_QO) AS DECIMAL(5, 2))
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    [counter] IN ('optimizations'
                  ,'trivial plan'
                  ,'no plan'
                  ,'search 0'
                  ,'search 1'
                  ,'search 2'
                  ,'timeout'
                  ,'memory limit exceeded'
                  ,'insert stmt'
                  ,'delete stmt'
                  ,'update stmt'
                  ,'merge stmt'
                  ,'contains subquery'
                  ,'view reference'
                  ,'remote query'
                  ,'dynamic cursor request'
                  ,'fast forward cursor request'
             )
)
SELECT
  [optimizations] AS [optimizations %]
  ,[trivial plan] AS [trivial plan %]
  ,[no plan] AS [no plan %]
  ,[search 0] AS [search 0 %]
  ,[search 1] AS [search 1 %]
  ,[search 2] AS [search 2 %]
  ,[timeout] AS [timeout %]
  ,[memory limit exceeded] AS [memory limit exceeded %]
  ,[insert stmt] AS [insert stmt %]
  ,[delete stmt] AS [delete stmt]
  ,[update stmt] AS [update stmt]
  ,[merge stmt] AS [merge stmt]
  ,[contains subquery] AS [contains subquery %]
  ,[view reference] AS [view reference %]
  ,[remote query] AS [remote query %]
  ,[dynamic cursor request] AS [dynamic cursor request %]
  ,[fast forward cursor request] AS [fast forward cursor request %]
FROM
  QOInfo
PIVOT (MAX([%]) FOR [counter] 
  IN ([optimizations]
      ,[trivial plan]
      ,[no plan]
      ,[search 0]
      ,[search 1]
      ,[search 2]
      ,[timeout]
      ,[memory limit exceeded]
      ,[insert stmt]
      ,[delete stmt]
      ,[update stmt]
      ,[merge stmt]
      ,[contains subquery]
      ,[view reference]
      ,[remote query]
      ,[dynamic cursor request]
      ,[fast forward cursor request])) AS p;
GO
```

このクエリの結果と、システム ビュー [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md) の結果を組み合わせて、クエリ統計、クエリ テキスト、およびキャッシュされた実行プランを識別します。 

## <a name="sysviews"></a>sys.views
次の CTE では、実行の数、合計実行時間、メモリから読み取られたページ数に関する情報が提供されます。 結果を使用して、最適化の候補となる可能性のあるクエリを識別できます。 
  
> [!NOTE]
> このクエリの結果は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって異なることがあります。  


```sql
WITH CTE_VW_STATS AS
(
  SELECT
    SCHEMA_NAME(vw.schema_id) AS schemaname
    ,vw.name AS viewname
    ,vw.object_id AS viewid
  FROM
    sys.views AS vw
  WHERE
    (vw.is_ms_shipped = 0)
  INTERSECT
  SELECT
    SCHEMA_NAME(o.schema_id) AS schemaname
    ,o.Name AS name
    ,st.objectid AS viewid
  FROM
    sys.dm_exec_cached_plans cp
  CROSS APPLY
    sys.dm_exec_sql_text(cp.plan_handle) st
  INNER JOIN
    sys.objects o ON st.[objectid] = o.[object_id]
  WHERE
    st.dbid = DB_ID()
)
SELECT
  vw.schemaname
  ,vw.viewname
  ,vw.viewid
  ,DB_NAME(t.databaseid) AS databasename
  ,t.databaseid
  ,t.*
FROM
  CTE_VW_STATS AS vw
CROSS APPLY
  (
    SELECT
      st.dbid AS databaseid
      ,st.text
      ,qp.query_plan
      ,qs.*
    FROM
      sys.dm_exec_query_stats AS qs
    CROSS APPLY
      sys.dm_exec_sql_text(qs.plan_handle) AS st
    CROSS APPLY
      sys.dm_exec_query_plan(qs.plan_handle) AS qp
    WHERE
      (CHARINDEX(vw.schemaname, st.text, 1) > 0)
      AND (st.dbid = DB_ID())
  ) AS t;
GO
```

## <a name="sysdmv_exec_cached_plans"></a>sys.dmv_exec_cached_plans
最後のクエリでは、DMV [sys.dmv_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) を使用して、未使用のビューに関する情報が提供されます。 ただし、実行プランのキャッシュは動的であり、結果は異なることがあります。 そのため、ある程度の期間についてこのクエリを使用し、ビューが実際に使用されているかどうかを判断します。 

```sql
SELECT
  SCHEMA_NAME(vw.schema_id) AS schemaname
  ,vw.name AS name
  ,vw.object_id AS viewid
FROM
  sys.views AS vw
WHERE
  (vw.is_ms_shipped = 0)
EXCEPT
SELECT
  SCHEMA_NAME(o.schema_id) AS schemaname
  ,o.name AS name
  ,st.objectid AS viewid
FROM
  sys.dm_exec_cached_plans cp
CROSS APPLY
  sys.dm_exec_sql_text(cp.plan_handle) st
INNER JOIN
  sys.objects o ON st.[objectid] = o.[object_id]
WHERE
  st.dbid = DB_ID();
GO
```

## <a name="see-also"></a>参照
[動的管理ビューおよび関数](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 
