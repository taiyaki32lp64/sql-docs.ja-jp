---
title: sp_query_store_unforce_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SP_QUERY_STORE_UNFORCE_PLAN_TSQL
- SP_QUERY_STORE_UNFORCE_PLAN
- SYS.SP_QUERY_STORE_UNFORCE_PLAN
- SYS.SP_QUERY_STORE_UNFORCE_PLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_unforce_plan
- sp_query_store_unforce_plan
ms.assetid: a52f91d0-ff1e-46ad-ba36-b32d9623c9ab
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9cff3bb0491db53e195a692014b74a08c4fdcdee
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207711"
---
# <a name="sp_query_store_unforce_plan-transact-sql"></a>sp_query_store_unforce_plan (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  特定のクエリに対して以前に強制されたプランの強制を解除できるようにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_query_store_unforce_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>引数  
`[ @query_id = ] query_id` はクエリの id です。 *query_id*は**bigint**,、既定値はありません。  
  
`[ @plan_id = ] plan_id` は、適用されなくなるクエリプランの id です。 *plan_id*は**bigint**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する**ALTER**権限が必要です。
  
## <a name="examples"></a>使用例  
 次の例では、クエリストア内のクエリに関する情報を返します。  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 強制解除する query_id と plan_id を特定したら、次の例を使用してプランを強制解除します。  
  
```sql  
EXEC sp_query_store_unforce_plan 3, 3;  
```  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_query_store_force_plan](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)  
 [sp_query_store_remove_plan &#40;transct-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [transact-sql &#40;  の&#41; sp_query_store_remove_query](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_query_store_reset_exec_stats](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_query_store_flush_db](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [クエリストア    を使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [クエリ ストアを使用する際の推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md#CheckForced)     
  
