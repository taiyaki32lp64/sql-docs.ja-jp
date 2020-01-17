---
title: dm_exec_query_statistics_xml (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 35f9cdfcc40d417a6aed19a3abe0e590061b2eb7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256014"
---
# <a name="sysdm_exec_query_statistics_xml-transact-sql"></a>dm_exec_query_statistics_xml (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

インフライト要求のクエリ実行プランを返します。 この DMV を使用すると、一時的な統計情報を含む showplan XML を取得できます。 

## <a name="syntax"></a>構文

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>引数 
*session_id*  
 検索するバッチを実行するセッション id を指定します。 *session_id*は**smallint**です。 *session_id*は、次の動的管理オブジェクトから取得できます。  
  
-   [dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>返されるテーブル

|列名|データ型|説明|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|セッションの ID。 Null 値は許容されません。|
|request_id|**通り**|要求の ID。 Null 値は許容されません。|
|sql_handle|**varbinary (64)**|クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。 NULL 値は許可されます。|
|plan_handle|**varbinary (64)**|現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 NULL 値は許可されます。|
|query_plan|**xml**|部分統計を含む*plan_handle*で指定されたクエリ実行プランのランタイム Showplan 表現を格納します。 プラン表示は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアド プロシージャ コール、ユーザー定義関数コールなどを含むバッチごとに、1 つのプランが生成されます。 NULL 値は許可されます。|

## <a name="remarks"></a>コメント
このシステム関数は、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降で使用できます。 KB [3190871](https://support.microsoft.com/help/3190871)を参照

このシステム関数は、**標準**および**簡易**クエリ実行統計プロファイルインフラストラクチャの両方で動作します。 詳細については、「[クエリプロファイリングインフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。  

次の条件下では、 **sys. dm_exec_query_statistics_xml**について返されたテーブルの**query_plan**列には、プラン表示の出力は返されません。  
  
-   指定された*session_id*に対応するクエリプランが実行されなくなった場合、返されるテーブルの**query_plan**列は null になります。 たとえば、プランハンドルがキャプチャされてから、 **dm_exec_query_statistics_xml**で使用された時間の間に遅延がある場合に、この状態が発生する可能性があります。  
    
**Xml**データ型で許可されている入れ子になったレベルの数に制限があるため、 **dm_exec_query_statistics_xml**は入れ子になった要素の128レベル以上のクエリプランを返すことができません。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでは、この条件が原因でクエリ プランが返されず、エラー 6335 が生成されます。 Service [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Pack 2 以降のバージョンでは、 **query_plan**列には NULL が返されます。   

## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW SERVER STATE` 権限が必要です。  

## <a name="examples"></a>例  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 実行中のバッチのライブクエリプランと実行統計を確認する  
 次の例では、 **dm_exec_requests**を照会して、興味深いクエリ`session_id`を検索し、出力からをコピーします。  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 次に、ライブクエリプランと実行統計を取得するには、 `session_id`システム関数**sys. dm_exec_query_statistics_xml**でコピーしたを使用します。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 または、実行中のすべての要求に対して結合されます。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>参照
  [トレースフラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Transact-sql&#41;&#40;の動的管理ビューおよび関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

