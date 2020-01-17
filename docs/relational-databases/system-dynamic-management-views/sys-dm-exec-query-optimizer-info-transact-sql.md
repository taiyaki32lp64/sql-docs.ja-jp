---
title: sys.dm_exec_query_optimizer_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6195ee80fb851a9875e4a95a6e5aab87deb905e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255353"
---
# <a name="sysdmexecqueryoptimizerinfo-transact-sql"></a>sys.dm_exec_query_optimizer_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーの操作に関する詳細な統計を返します。 クエリの最適化問題や改善点を識別するために、ワークロードのチューニング時にこのビューを使用できます。 たとえば、最適化の合計数、所要時間、および最終的なコストを使用して、現在のワークロードのクエリの最適化と、チューニング処理中に確認された変更を比較できます。 一部のカウンターでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部診断で使用するためだけに適用されるデータを提供します。 このようなカウンターには、"内部使用のみ" と記載してあります。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_exec_query_optimizer_info**します。  
  
|名前|データの種類|説明|  
|----------|---------------|-----------------|  
|**counter**|**nvarchar (4000)**|オプティマイザーの統計イベントの名前。|  
|**occurrence**|**bigint**|このカウンターに関する最適化イベントの出現回数。|  
|**value**|**float**|イベントの発生ごとの平均プロパティ値です。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
    
## <a name="remarks"></a>コメント  
 **sys.dm_exec_query_optimizer_info**次のプロパティ (カウンター) が含まれています。 すべてのオカレンス値は、累積的なシステムの再起動時に 0 に設定されます。 値フィールドのすべての値は、システムの再起動で NULL に設定されます。 平均を示す列のすべての値では、平均計算の分母として、同一行を基にした発生回数の値が使用されます。 すべてのクエリの最適化のときに測定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への変更が決定**dm_exec_query_optimizer_info**、両方のユーザーとシステムによって生成されたクエリを含みます。 既にキャッシュされている計画の実行がの値を変更していない**dm_exec_query_optimizer_info**、専用の最適化が重要です。  
  
|カウンター|個数|値|  
|-------------|----------------|-----------|  
|最適化|最適化の合計数。|適用なし|  
|elapsed time|最適化の合計数。|個別のステートメント (クエリ) の最適化ごとの平均経過時間 (秒単位)。|  
|最終的なコスト|最適化の合計数。|内部コスト単位での最適なプランの推定コストの平均です。|  
|単純なプラン|内部使用のみ|内部使用のみ|  
|タスク|内部使用のみ|内部使用のみ|  
|no plan|内部使用のみ|内部使用のみ|  
|0 を検索します。|内部使用のみ|内部使用のみ|  
|search 0 time|内部使用のみ|内部使用のみ|  
|search 0 tasks|内部使用のみ|内部使用のみ|  
|1 を検索します。|内部使用のみ|内部使用のみ|  
|1 回を検索します。|内部使用のみ|内部使用のみ|  
|1 個のタスクを検索します。|内部使用のみ|内部使用のみ|  
|2 を検索します。|内部使用のみ|内部使用のみ|  
|search 2 time|内部使用のみ|内部使用のみ|  
|2 つのタスクを検索します。|内部使用のみ|内部使用のみ|  
|gain stage 0 to stage 1|内部使用のみ|内部使用のみ|  
|gain stage 1 to stage 2|内部使用のみ|内部使用のみ|  
|timeout|内部使用のみ|内部使用のみ|  
|memory limit exceeded|内部使用のみ|内部使用のみ|  
|stmt を挿入します。|INSERT ステートメントに対する最適化の数。|適用なし|  
|stmt を削除します。|DELETE ステートメントに対する最適化の数。|適用なし|  
|update stmt|UPDATE ステートメントに対する最適化の数。|適用なし|  
|contains subquery|少なくとも 1 つのサブクエリを含むクエリの最適化の数。|適用なし|  
|unnest failed|内部使用のみ|内部使用のみ|  
|tables|最適化の合計数。|最適化された 1 つのクエリあたりの、参照テーブルの平均数。|  
|ヒント|ヒントが指定された回数。 カウントされるヒントは次のとおりです。結合、グループ、共用体、および FORCE ORDER クエリ ヒント、FORCE PLAN 設定オプション、および結合ヒント。|適用なし|  
|order hint|FORCE ORDER ヒントが指定された回数。|適用なし|  
|結合ヒント|結合ヒントによって結合アルゴリズムが強制された回数。|適用なし|  
|view reference|ビューがクエリで参照された回数。|適用なし|  
|remote query|クエリで 4 部構成の名前または OPENROWSET の結果を含むテーブルなど少なくとも 1 つのリモート データ ソースが参照される最適化の数。|適用なし|  
|最大 DOP|最適化の合計数。|最適なプランの有効な MAXDOP 値を平均します。 既定では、有効な MAXDOP が続く、**並列処理の最大限度**サーバー構成オプション、および特定のクエリの MAXDOP クエリ ヒントの値によってオーバーライドできます。|  
|maximum recursion level|クエリ ヒントで 0 より大きい MAXRECURSION レベルが指定された最適化の数。|クエリ ヒントで最大再帰レベルが指定されている最適化における MAXRECURSION レベルの平均です。|  
|indexed views loaded|内部使用のみ|内部使用のみ|  
|indexed views matched|1 つ以上のインデックス付きビューが一致した、最適化の数。|ビューの平均数が一致します。|  
|インデックス付きビューの使用|出力プラン内で照合された後に 1 つ以上のインデックス付きビューが使用されている、最適化の数。|使用されたビューの平均数。|  
|インデックス付きビューの更新|1 つ以上のインデックス付きビューを管理するプランを作成する DML ステートメントの最適化の数。|管理されるビューの平均数。|  
|動的カーソルの要求|動的カーソルの要求が指定された最適化の数。|適用なし|  
|高速順方向カーソルの要求|高速順方向カーソルの要求が指定された最適化の数。|適用なし|  
|stmt をマージします。|MERGE ステートメントに対する最適化の数。|適用なし|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>A. オプティマイザー実行における統計を表示  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対する、現在のオプティマイザー実行の統計を表示します。  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>B. 最適化の合計数を表示します。  
 最適化の数が実行されますか。  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>C. 最適化ごとの平均経過時間  
 最適化ごとの平均経過時間を表示します。  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>D. サブクエリを含む最適化の割合  
 サブクエリを含む最適化されたクエリの割合を表示します。  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


