---
title: dm_exec_text_query_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d23813078c2a90b18af0a1df48079b571e77a13
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983139"
---
# <a name="sysdm_exec_text_query_plan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチまたはバッチ内の特定のステートメントのプラン表示をテキスト形式で返します。 プランハンドルで指定されたクエリプランは、キャッシュまたは現在実行できます。 このテーブル値関数は、 [dm_exec_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)に似ていますが、次の点が異なります。  
  
-   クエリ プランの出力がテキスト形式で返される。  
-   クエリプランの出力のサイズは制限されていません。  
-   バッチ内の個々のステートメントを指定できます。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>引数  
*plan_handle*  
は、実行され、そのプランがプランキャッシュに存在するか、現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 *plan_handle*は**varbinary (64)** です。   

*Plan_handle*は、次の動的管理オブジェクトから取得できます。 
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
*statement_start_offset* | 0 | DEFAULT  
バッチまたは保存されるオブジェクトのテキスト内での、行が示すクエリの開始位置 (バイト単位) を示します。 *statement_start_offset*は**int**です。値0はバッチの先頭を示します。 既定値は 0 です。  
  
ステートメントの開始オフセットは、次の動的管理オブジェクトから取得できます。  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | DEFAULT  
バッチまたは保存されるオブジェクトのテキスト内で、行が示すクエリの終了位置をバイト単位で示します。  
  
*statement_start_offset*は**int**です。  
  
値 -1 はバッチの最後を表します。 既定値は-1 です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 アドホック SQL ステートメントおよび準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> 列は null 値を許容します。|  
|**objectid**|**int**|このクエリプランのオブジェクト (ストアドプロシージャやユーザー定義関数など) の ID。 アドホックバッチおよび準備されたバッチの場合、この列は**null**になります。<br /><br /> 列は null 値を許容します。|  
|**number**|**smallint**|番号付きストアドプロシージャの整数。 たとえば、 **orders**アプリケーションのプロシージャグループに**orderproc; 1**、 **orderproc; 2**のような名前を付けることができます。 アドホックバッチおよび準備されたバッチの場合、この列は**null**になります。<br /><br /> 列は null 値を許容します。|  
|**encrypted**|**bit**|対応するストアドプロシージャが暗号化されているかどうかを示します。<br /><br /> 0 = 暗号化されていない<br /><br /> 1 = 暗号化<br /><br /> 列は null 値を許容しません。|  
|**query_plan**|**nvarchar(max)**|*Plan_handle*で指定されたクエリ実行プランのコンパイル時のプラン表示表現を格納します。 プラン表示はテキスト形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアドプロシージャ呼び出し、ユーザー定義関数呼び出しなどを含むバッチごとに1つのプランが生成されます。<br /><br /> 列は null 値を許容します。|  
  
## <a name="remarks"></a>Remarks  
 次の条件下では、返されたテーブル ( **sys. dm_exec_text_query_plan**) の**Plan**列にプラン表示の出力は返されません。  
  
-   *Plan_handle*を使用して指定されたクエリプランがプランキャッシュから削除されている場合、返されるテーブルの**query_plan**列は null になります。 たとえば、プランハンドルがキャプチャされてから、 **dm_exec_text_query_plan**で使用された時間の間に遅延がある場合に、この状態が発生する可能性があります。  
  
-   一括操作ステートメントや、8 KB を超える文字列リテラルを含むステートメントなど、一部の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはキャッシュされません。 これらのステートメントのプラン表示はキャッシュに存在しないため、dm_exec_text_query_plan を使用して取得することはできません **。**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチまたはストアドプロシージャに、ユーザー定義関数への呼び出し、または EXEC (*string*) の使用などの動的 SQL の呼び出しが含まれている場合、ユーザー定義関数のコンパイル済み XML プラン表示は、バッチまたはストアドプロシージャの場合は、 **sys. dm_exec_text_query_plan**によって返されたテーブルには含まれません。 代わりに、ユーザー定義関数に対応する*plan_handle*に対して、 **dm_exec_text_query_plan**の個別の呼び出しを行う必要があります。  
  
アドホッククエリで[簡易](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)または[強制パラメーター](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)化を使用する場合、 **query_plan**列にはステートメントテキストのみが含まれ、実際のクエリプランは含まれません。 クエリプランを返すには、準備されたパラメーター化クエリのプランハンドルに対して**dm_exec_text_query_plan**を呼び出します。 クエリがパラメーター化されたかどうかを確認するには、[syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) ビューの**sql**列、または動的管理ビューの text [dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)列を参照します。  
  
## <a name="permissions"></a>アクセス許可  
 **Dm_exec_text_query_plan**を実行するには、ユーザーが**sysadmin**固定サーバーロールのメンバーであるか、サーバーに対する VIEW server STATE 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 実行速度の遅い Transact-sql クエリまたはバッチのキャッシュされたクエリプランを取得する  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッチが、特定の  との接続において長時間実行されている場合は、このクエリやバッチの実行プランを取得して、遅延の原因を調べることができます。 次の例では、実行速度の遅いクエリまたはバッチのプラン表示を取得する方法を示します。  
  
> [!NOTE]  
> この例を実行するには、 *session_id*と*plan_handle*の値を実際のサーバー固有の値に置き換えます。  
  
 まず、`sp_who` ストアド プロシージャを使用して、クエリまたはバッチを実行しているプロセスのサーバー プロセス ID (SPID) を取得します。  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 `sp_who` によって返される結果セットは、SPID が `54`であることを示します。 `sys.dm_exec_requests` 動的管理ビューで、この SPID を使用して次のクエリを実行すると、プラン ハンドルを取得できます。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 **Dm_exec_requests**によって返されるテーブルは、実行速度の遅いクエリまたはバッチのプランハンドルが `0x06000100A27E7C1FA821B10600`ことを示します。 次の例は、指定したプラン ハンドルのクエリ プランを返し、既定値 0 および -1 を使用してクエリまたはバッチ内のすべてのステートメントを返します。  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>b. プランキャッシュからすべてのクエリプランを取得する  
 プラン キャッシュにあるすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_cached_plans` 動的管理ビューに対してクエリを実行し、キャッシュにあるすべてのクエリ プランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_cached_plans` 列に格納されます。 次に、クロス適用演算子を使用して、次のように `sys.dm_exec_text_query_plan` にプランハンドルを渡します。 現在プランキャッシュにある各プランのプラン表示出力は、返されるテーブルの `query_plan` 列にあります。  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. サーバーがクエリ統計情報を収集したすべてのクエリプランをプランキャッシュから取得する  
 現在プラン キャッシュにあるクエリ プランのうち、サーバーで統計情報が収集されたすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_query_stats` 動的管理ビューに対してクエリを実行し、キャッシュにあるこれらのプランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_query_stats` 列に格納されます。 次に、クロス適用演算子を使用して、次のように `sys.dm_exec_text_query_plan` にプランハンドルを渡します。 各プランのプラン表示出力は、返されるテーブルの `query_plan` 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 平均 CPU 時間による上位5つのクエリに関する情報の取得  
 次の例では、上位5つのクエリのクエリプランと平均 CPU 時間が返されます。 Dm_exec_text_query_plan 関数は、クエリプラン内のバッチ内のすべてのステートメントを返す既定値0と-1 を指定し**ます**。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dm_exec_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
