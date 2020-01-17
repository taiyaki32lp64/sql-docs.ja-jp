---
title: sp_create_plan_guide_from_handle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
author: stevestein
ms.author: sstein
ms.openlocfilehash: 15fa1de65ada904ecf4b93947e1e9e9f818fd0d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108676"
---
# <a name="spcreateplanguidefromhandle-transact-sql"></a>sp_create_plan_guide_from_handle (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  プラン キャッシュ内のクエリ プランから 1 つ以上のプラン ガイドを作成します。 このストアド プロシージャを使用するには、クエリ オプティマイザーは常に指定されたクエリの特定のクエリ プランを使用するようにします。 プラン ガイドの詳細については、「 [Plan Guides](../../relational-databases/performance/plan-guides.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>引数  
 [ @name =] N'*plan_guide_name*'  
 プラン ガイドの名前を指定します。 プラン ガイド名は現在のデータベースに対して有効です。 *plan_guide_name*の規則に従っている必要があります[識別子](../../relational-databases/databases/database-identifiers.md)番号記号で始めることはできません (#)。 最大長*plan_guide_name*は 124 文字です。  
  
 [ @plan_handle = ] *plan_handle*  
 プラン キャッシュのバッチを識別します。 *plan_handle*は**varbinary (64)** します。 *plan_handle*から取得できます、 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)動的管理ビュー。  
  
 [ @statement_start_offset = ] { *statement_start_offset* | NULL } ]  
 指定したバッチ内のステートメントの開始位置を識別する*plan_handle*します。 *statement_start_offset*は**int**、既定値は NULL です。  
  
 ステートメント オフセットは statement_start_offset 列に対応する、 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)動的管理ビュー。  
  
 NULL を指定した場合や、ステートメント オフセットを指定しない場合は、指定したプラン ハンドルのクエリ プランを使用してバッチ内の各ステートメントに対してプラン ガイドが作成されます。 結果のプラン ガイドでは、プラン ガイドの USE PLAN クエリ ヒントを使用して、特定のプランを強制的に使用すると同じです。  
  
## <a name="remarks"></a>コメント  
 すべての種類のステートメントに対してプラン ガイドを作成できるわけではありません。 プラン ガイドを作成できないステートメントがバッチ内にあった場合、そのステートメントは無視されて、バッチ内の次のステートメントが処理されます。 ステートメントでは、同じバッチで複数回が発生する場合は、最後に出現する位置のプランが有効になり、ステートメントより前のプランが無効になっています。 プラン ガイドで、バッチ内のステートメントを使用されず、エラー 10532 が発生し、ステートメントは失敗します。 このエラーを回避するため、常に sys.dm_exec_query_stats 動的管理ビューからプラン ハンドルを取得することをお勧めします。  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle では、プラン キャッシュに含まれているとおりのプランに基づいてプラン ガイドが作成されます。 したがって、バッチ テキスト、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、および XML プラン表示が、プラン キャッシュから結果のプラン ガイドに文字単位で (クエリに渡されたリテラル値も含め) 取り込まれます。 これらのテキスト文字列には、データベースのメタデータに格納し、機密情報を含めることができます。 適切なアクセス許可を持つユーザーは、sys.plan_guides カタログ ビューを使用してこの情報を表示することができます、**プラン ガイド プロパティ** ダイアログ ボックスで[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。 プラン ガイドから機密情報が公開されないことを確認するには、プラン キャッシュから作成されたプラン ガイドのレビューをお勧めします。  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>クエリ プラン内の複数のステートメントに対してプラン ガイドを作成します。  
 sp_create_plan_guide_from_handle では、sp_create_plan_guide と同様に、対象となるバッチやモジュールのクエリ プランがプラン キャッシュから削除されます。 これは、新しいプラン ガイドがすべてのユーザーによって使用されるようにするための措置です。 1 つのクエリ プラン内で複数のステートメントに対してプラン ガイドを作成するときに、明示的なトランザクションですべてのプラン ガイドを作成して、キャッシュからプランの削除を延期することができます。 これにより、そのトランザクションが完了して、指定した各ステートメントのプラン ガイドが作成されるまで、プランがキャッシュに保持されます。 例 B を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。 その他、sp_create_plan_guide_from_handle を使用して作成するプラン ガイドごとに必要な個々の権限があります。 型のプラン ガイドを作成するには、オブジェクトには、参照先オブジェクトに対する ALTER 権限が必要です。 SQL または TEMPLATE 型のプラン ガイドを作成するには、現在のデータベースに対する ALTER 権限が必要です。 作成されるプラン ガイドの種類を確認するのには、次のクエリを実行します。  
  
```  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 プラン ガイドを作成するステートメントを含む行を調べて、`objtype`結果セット内の列。 値`Proc`プラン ガイドは OBJECT 型を示します。 その他の値など`AdHoc`または`Prepared`SQL 型のプラン ガイドを示します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>A. プラン キャッシュ内のクエリ プランからプラン ガイドを作成する  
 次の例では、プラン キャッシュからクエリ プランを指定して単一の SELECT ステートメントのプラン ガイドを作成します。 まず、プラン ガイドを作成する単純な `SELECT` ステートメントを実行します。 次に、動的管理ビューの `sys.dm_exec_sql_text` および `sys.dm_exec_text_query_plan` を使用してこのクエリのプランを調べます。 プラン ガイドは、クエリに関連付けられているプラン キャッシュ内のクエリ プランを指定することで、クエリの作成されます。 この例の最後のステートメントは、プラン ガイドが存在することを確認します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>B. 複数のステートメントで構成されるバッチに対して複数のプラン ガイドを作成する  
 次の例では、複数ステートメントのバッチ内の 2 つのステートメントに対してプラン ガイドを作成します。 プラン ガイドが、明示的なトランザクション内で作成されるため、最初のプラン ガイドを作成した後、バッチのクエリ プランはプラン キャッシュから削除されません。 まず、複数のステートメントで構成されるバッチを実行します。 バッチのプランは動的管理ビューを使用して調べます。 バッチ内の各ステートメントの行が返されることに注意してください。 指定して、バッチ内の最初と 3 番目のステートメントのプラン ガイドが作成し、`@statement_start_offset`パラメーター。 最後のステートメントの例では、プラン ガイドが存在することを確認します。  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [プラン ガイド](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_text_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
