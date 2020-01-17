---
title: sys.fn_stmt_sql_handle_from_sql_stmt (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92ebff45c8599e6257ad22f563da6af5067d8e3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059269"
---
# <a name="sysfnstmtsqlhandlefromsqlstmt-transact-sql"></a>sys.fn_stmt_sql_handle_from_sql_stmt (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  取得、 **stmt_sql_handle**の[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント パラメーターの型 (簡易または強制) 指定します。 使用して、クエリのストアに格納されたクエリを参照することができます、 **stmt_sql_handle**わかっている場合にそれぞれのテキスト。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.fn_stmt_sql_handle_from_sql_stmt   
(  
    'query_sql_text',   
    [ query_param_type   
) [;]  
```  
  
## <a name="arguments"></a>引数  
 *query_sql_text*  
 ハンドルをクエリ ストアでのクエリのテキストです。 *query_sql_text*は、 **nvarchar (max)** 、既定値はありません。  
  
 *query_param_type*  
 クエリのパラメーター型です。 *query_param_type*は、 **tinyint**します。 設定可能な値は、次のとおりです。  
  
-   NULL の既定値は 0  
  
-   0 - なし  
  
-   1-ユーザー  
  
-   2-シンプルです  
  
-   3-強制  
  
## <a name="columns-returned"></a>返される列  
 次の表に、列を sys.fn_stmt_sql_handle_from_sql_stmt を返します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|SQL ハンドル。|  
|**query_sql_text**|**nvarchar(max)**|テキスト、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
|**query_parameterization_type**|**tinyint**|クエリ パラメーターの型。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
  
## <a name="permissions"></a>アクセス許可  
 必要があります、 **EXECUTE** 、データベースに対する権限と**削除**クエリ ストアのカタログ ビューに対する権限。  
  
## <a name="examples"></a>使用例  
 次の例は、ステートメントを実行しを使用して、`sys.fn_stmt_sql_handle_from_sql_stmt`そのステートメントの SQL ハンドルを返します。  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 その他の動的管理ビューとクエリ ストアのデータを関連付けるために、関数を使用します。 次の例では:  
  
```  
SELECT qt.query_text_id, q.query_id, qt.query_sql_text, qt.statement_sql_handle,  
q.context_settings_id, qs.statement_context_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_id  
CROSS APPLY sys.fn_stmt_sql_handle_from_sql_stmt (qt.query_sql_text, null) AS fn_handle_from_stmt  
JOIN sys.dm_exec_query_stats AS qs   
    ON fn_handle_from_stmt.statement_sql_handle = qs.statement_sql_handle;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [sp_query_store_remove_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
