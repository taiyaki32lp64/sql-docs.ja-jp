---
title: sys.dm_exec_query_plan (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d4ccd016c32e197c75026c1039e5ff4c21eef32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135180"
---
# <a name="sysdm_exec_query_plan-transact-sql"></a>sys.dm_exec_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

プラン ハンドルで指定されたバッチのプラン表示を XML 形式で返します。 プランでは、プラン ハンドルでできますキャッシュまたは現在実行されているを指定します。  
  
プラン表示の XML スキーマは公開されてで使用可能な[この Microsoft Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)します。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているディレクトリからも入手できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_exec_query_plan(plan_handle)  
```  
  
## <a name="arguments"></a>引数  
*plan_handle*  
実行されるバッチのクエリ実行プランを一意に識別するトークンと、そのプランがプラン キャッシュ内に存在または現在実行しています。 *plan_handle*は**varbinary (64)** します。   

*Plan_handle*次の動的管理オブジェクトから取得できます。
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 アドホック SQL ステートメントおよび準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> 列が null 値を許容します。|  
|**objectid**|**int**|このクエリ プランのオブジェクト (たとえば、ストアド プロシージャまたはユーザー定義関数) の ID。 アドホックおよび準備されたバッチでは、この列は**null**します。<br /><br /> 列が null 値を許容します。|  
|**number**|**smallint**|番号付きストアド プロシージャの整数。 ための手順のグループなど、**注文**アプリケーションが付けられて**orderproc; 1**、 **orderproc; 2**など。 アドホックおよび準備されたバッチでは、この列は**null**します。<br /><br /> 列が null 値を許容します。|  
|**encrypted**|**bit**|対応するストアド プロシージャを暗号化するかどうかを示します。<br /><br /> 0 = 暗号化されていません。<br /><br /> 1 = 暗号化<br /><br /> 列値が許容されません。|  
|**query_plan**|**xml**|指定されているクエリの実行プランのコンパイル時のプラン表示形式を格納して*plan_handle*します。 プラン表示は XML 形式です。 含まれているなどのアドホック バッチごとに 1 つのプランが生成された[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント、ストアド プロシージャの呼び出し、およびユーザー定義関数の呼び出し。<br /><br /> 列が null 値を許容します。|  
  
## <a name="remarks"></a>コメント  
 次の条件では、プラン表示出力が返されない、 **query_plan**の返されたテーブルの列**sys.dm_exec_query_plan**:  
  
-   場合は、クエリ プランを使用して指定*plan_handle*がプラン キャッシュから削除された、 **query_plan**返されるテーブルの列が null です。 プラン ハンドルがキャプチャされた、と共に使用された場合との間の遅延時間がある場合にこの状態が発生するなど、 **sys.dm_exec_query_plan**します。  
  
-   いくつか[!INCLUDE[tsql](../../includes/tsql-md.md)]一括操作ステートメントや 8 KB のサイズより大きい文字列リテラルを含むステートメントなど、ステートメントはキャッシュされません。 使用してこのようなステートメントの XML プラン表示を取得することはできません**sys.dm_exec_query_plan**バッチは、キャッシュが存在しないために現在実行している場合を除き、します。  
  
-   場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチまたはストアド プロシージャは、ユーザー定義関数への呼び出しやたとえば EXEC を使用して、動的 SQL への呼び出しが含まれます (*文字列*)、XML プラン表示の表に、ユーザー定義関数が含まれていないコンパイルによって返される**sys.dm_exec_query_plan**バッチやストアド プロシージャ。 代わりに、別の呼び出しを行う必要があります**sys.dm_exec_query_plan**ユーザー定義関数に対応するプラン ハンドル。  
  
 アドホック クエリは、簡易または強制パラメーター化を使用する場合、 **query_plan**ステートメント テキストのみと実際のクエリ プランではない列が含まれます。 クエリ プランを返すを呼び出す**sys.dm_exec_query_plan**準備されたパラメーター化されたクエリのプラン ハンドル。 参照することによって、クエリがパラメーター化されたかどうかを指定できます、 **sql**の列、 [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)ビューまたはの text 列、 [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)動的管理ビュー。  
  
> [!NOTE] 
> 許可される入れ子のレベルの数の制限により、 **xml**データ型、 **sys.dm_exec_query_plan**を満たす、または入れ子になった要素のレベルが 128 を超えるクエリ プランを返すことはできません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでは、この条件が原因でクエリ プランが返されず、エラー 6335 が生成されます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 および以降のバージョンで、 **query_plan**列は NULL を返します。   
> 使用することができます、 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)動的管理関数をテキスト形式でクエリ プランの出力を返します。  
  
## <a name="permissions"></a>アクセス許可  
 実行する**sys.dm_exec_query_plan**、ユーザーのメンバーである必要があります、 **sysadmin**または固定サーバー ロール、`VIEW SERVER STATE`サーバーに対する権限。  
  
## <a name="examples"></a>使用例  
 次の例を使用する方法を示して、 **sys.dm_exec_query_plan**動的管理ビュー。  
  
 XML プラン表示を表示するクエリを実行、次のクエリ エディターで[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 をクリックし、 **ShowPlanXML**で、 **query_plan**によって返されるテーブルの列**sys.dm_exec_query_plan**します。 XML プラン表示が表示されます、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]概要ペイン。 XML プラン表示をファイルに保存するを右クリックして**ShowPlanXML**で、 **query_plan**列で、をクリックして**結果に名前を付けて**の形式でファイルの名前\< *file_name*> .sqlplan。 たとえば、MyXMLShowplan.sqlplan します。  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 実行速度の遅い Transact-SQL クエリまたはバッチのキャッシュされたクエリ プランを取得します。  
 クエリのさまざまな種類のプラン[!INCLUDE[tsql](../../includes/tsql-md.md)]アドホック バッチ、ストアド プロシージャ、およびユーザー定義関数などのバッチがプラン キャッシュと呼ばれるメモリ領域にキャッシュされます。 各キャッシュされたクエリ プランは、プラン ハンドルと呼ばれる一意の識別子によって識別されます。 このプラン ハンドルを指定することができます、 **sys.dm_exec_query_plan**特定の実行プランを取得する動的管理ビュー[!INCLUDE[tsql](../../includes/tsql-md.md)]クエリまたはバッチです。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッチが、特定の  との接続において長時間実行されている場合は、このクエリやバッチの実行プランを取得して、遅延の原因を調べることができます。 次の例では、実行速度の遅いクエリまたはバッチの XML プラン表示を取得する方法を示します。  
  
> [!NOTE]  
>  この例を実行するには、値を置き換えます*session_id*と*plan_handle*サーバーに特定の値を使用します。  
  
 まず、`sp_who` ストアド プロシージャを使用して、クエリまたはバッチを実行しているプロセスのサーバー プロセス ID (SPID) を取得します。  
  
```sql  
USE master;  
GO  
exec sp_who;  
GO  
```  
  
 によって返される結果セット`sp_who`、spid の値があることを示します`54`します。 `sys.dm_exec_requests` 動的管理ビューで、この SPID を使用して次のクエリを実行すると、プラン ハンドルを取得できます。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 によって返されるテーブル**sys.dm_exec_requests**実行速度の遅いクエリまたはバッチのプラン ハンドルがあることを示します`0x06000100A27E7C1FA821B10600`、として指定できますが、 *plan_handle* 引数`sys.dm_exec_query_plan`を次のように XML 形式での実行プランを取得します。 実行速度の遅いクエリまたはバッチの XML 形式での実行プランに含まれている、 **query_plan**によって返されるテーブルの列`sys.dm_exec_query_plan`します。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. すべてのクエリ プランをプラン キャッシュから取得します。  
 プラン キャッシュにあるすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_cached_plans` 動的管理ビューに対してクエリを実行し、キャッシュにあるすべてのクエリ プランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_cached_plans` 列に格納されます。 CROSS APPLY 演算子を使用し、プラン ハンドルを渡す`sys.dm_exec_query_plan`次のようにします。 現在プラン キャッシュにある各プランの XML プラン表示の出力は、返されるテーブルの `query_plan` 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 対象のサーバーは、プラン キャッシュからクエリの統計情報を収集がすべてのクエリ プランを取得します。  
 現在プラン キャッシュにあるクエリ プランのうち、サーバーで統計情報が収集されたすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_query_stats` 動的管理ビューに対してクエリを実行し、キャッシュにあるこれらのプランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_query_stats` 列に格納されます。 CROSS APPLY 演算子を使用し、プラン ハンドルを渡す`sys.dm_exec_query_plan`次のようにします。 XML プラン表示の出力をサーバーが、現在プラン キャッシュ内の統計情報を収集する各プランは、`query_plan`返されるテーブルの列。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 平均 CPU 時間に基づく上位 5 つのクエリに関する情報を取得する  
 次の例では、プランと、上位 5 つのクエリの平均 CPU 時間を返します。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
