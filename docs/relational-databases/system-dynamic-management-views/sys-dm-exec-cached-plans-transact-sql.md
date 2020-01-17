---
title: sys.dm_exec_cached_plans (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe53a1d912ce03ab2eedb66b72b4de947466b313
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263943"
---
# <a name="sysdmexeccachedplans-transact-sql"></a>sys.dm_exec_cached_plans (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  クエリ実行を高速化するため [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でキャッシュされた各クエリ プランについての行を返します。 この動的管理ビューを使用して、キャッシュされたクエリ プラン、キャッシュされたクエリ テキスト、キャッシュされたプランは、およびキャッシュされたプランの再利用回数によって取得されるメモリの量を検索することができます。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。さらに、列の値**memory_object_address**と**pool_id**フィルター処理され、列の値は NULL に設定されます。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_exec_cached_plans**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|エントリをキャッシュするハッシュ バケットの ID。 値の範囲は、0 からキャッシュの種類によって決まっているハッシュ テーブルのサイズまでです。<br /><br /> SQL プランおよびオブジェクト プランのキャッシュでは、最大 10007 32 ビット システムと 64 ビット システムで最大 40009 ですが、ハッシュ テーブルのサイズにできます。 Bound Trees のキャッシュのハッシュ テーブルのサイズは最大 1009、32 ビット システムと 64 ビット システムで最大 4001 を指定できます。 拡張ストアド プロシージャのキャッシュでは、ハッシュ テーブルのサイズが 32 ビット システムでも 64 ビット システムでも 127 です。|  
|refcounts|**int**|このキャッシュ オブジェクトを参照しているキャッシュ オブジェクトの数。 **Refcounts**エントリがキャッシュ内の 1 以上である必要があります。|  
|usecounts|**int**|キャッシュ オブジェクトが検索された回数。 パラメーター化クエリがキャッシュでプランを検索するときは増加しません。 プラン表示を使用しているときは複数回増加できます。|  
|size_in_bytes|**int**|キャッシュ オブジェクトによって使用されたバイト数。|  
|memory_object_address|**varbinary(8)**|キャッシュ エントリのメモリ アドレス。 この値で使用できる[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)およびキャッシュされたプランのメモリ内訳を取得する[sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)とエントリをキャッシュするコストを取得します。|  
|cacheobjtype|**nvarchar(34)**|キャッシュ内のオブジェクトの種類。 値は次のいずれかになります。<br /><br /> コンパイル済みプラン<br /><br /> コンパイル済みプランのスタブ<br /><br /> Parse Tree<br /><br /> 拡張プロシージャ<br /><br /> CLR コンパイル Func<br /><br /> CLR コンパイル プロシージャ|  
|objtype|**nvarchar(16)**|オブジェクトの種類。 使用可能な値とその対応する説明を次に示します。<br /><br /> プロシージャ:ストアド プロシージャ<br />準備。準備済みステートメント<br />Adhoc:アドホック クエリ。 指す[!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、言語イベントとして送信された**osql**または**sqlcmd**の代わりにリモート プロシージャ呼び出しとして。<br />ReplProc:レプリケーション フィルター プロシージャ<br />トリガー:トリガー<br />ビュー:表示<br />既定値:既定<br />UsrTab:ユーザー テーブル<br />SysTab:システム テーブル<br />確認してください。CHECK 制約<br />ルール:Rule|  
|plan_handle|**varbinary(64)**|メモリ内のプランの識別子。 この識別子は、一時的なプランをキャッシュに保持している間だけ一定のまま。 この値は、次の動的管理関数で使用できます。<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|このプランのメモリ使用量の大部分を占めるリソース プールの ID。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. 再利用されたキャッシュ エントリのバッチ テキストを返す  
 次の例では、複数回使用されているすべてのキャッシュされたエントリの SQL テキストを返します。  
  
```sql  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>B. すべてのキャッシュされたトリガーのクエリ プランを取得します。  
 次の例では、すべてのキャッシュされたトリガーのクエリ プランを返します。  
  
```sql  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. プランをコンパイルした SET オプションを返す  
 次の例は、プランをコンパイルした SET オプションを返します。 `sql_handle`でプランが返されることもできます。 PIVOT 演算子が使用される出力に、`set_options`と`sql_handle`属性の行ではなく列として。 戻り値の詳細については`set_options`を参照してください[sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)します。  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. すべてのキャッシュされたコンパイル済みプランのメモリ内訳を取得します。  
 次の例では、キャッシュ内のすべてのコンパイル済みプランで使用されるメモリの内訳を返します。  
  
```sql  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [sys.dm_os_memory_cache_entries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  


