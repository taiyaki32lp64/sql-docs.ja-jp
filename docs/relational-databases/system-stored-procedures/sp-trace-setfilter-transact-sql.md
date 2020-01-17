---
title: sp_trace_setfilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f48f7e8dd6e7d8fa57868994f9bcabb66777e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095937"
---
# <a name="sptracesetfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トレースにフィルターを適用します。 **sp_trace_setfilter**停止している既存のトレースに対してのみ実行できます (*状態*は**0**)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このストアド プロシージャが存在しないトレースまたはで実行される場合はエラーを返します*状態*ない**0**します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` フィルターが設定されているトレースの ID です。 *trace_id*は**int**、既定値はありません。 ユーザーがこれを採用して*trace_id*識別、変更、およびトレースを制御する値。  
  
`[ @columnid = ] column_id` フィルターが適用されている列の ID です。 *column_id*は**int**、既定値はありません。 場合*column_id*が null の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定されたトレースに対してすべてのフィルターをクリアします。  
  
`[ @logical_operator = ] logical_operator` 指定するかどうか AND (**0**) または OR (**1**) 演算子が適用されます。 *logical_operator*は**int**、既定値はありません。  
  
`[ @comparison_operator = ] comparison_operator` する比較の種類を指定します。 *comparison_operator*は**int**、既定値はありません。 テーブルには、比較演算子とその代表的な値が含まれています。  
  
|値|比較演算子|  
|-----------|-------------------------|  
|**0**|= (等しい)|  
|**1**|<> (等しくない)|  
|**2**|> (より大きい)|  
|**3**|< (より小さい)|  
|**4**|> = (より大きいまたは等しい)|  
|**5**|< = (以下)|  
|**6**|LIKE|  
|**7**|パターンに一致しない|  
  
`[ @value = ] value` フィルター処理する値を指定します。 データ型*値*フィルター処理する列のデータ型に一致する必要があります。 たとえば、あるオブジェクトの ID 列にフィルターが設定されている場合、 **int**データ型、*値*必要があります**int**します。場合*値*は**nvarchar**または**varbinary**8000 の最大長を持つことができます。  
  
 比較演算子は、LIKE または NOT LIKE、論理演算子は、「%」または LIKE 演算に適したその他のフィルターを含めることができます。  
  
 場合は NULL を指定する*値*NULL 列の値を持つイベントを除外します。 のみ**0** (= 等号) と**1** (<> 等しくない) 演算子は NULL で有効です。 この場合、これらの演算子は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の IS NULL 演算子および IS NOT NULL 演算子と等価です。  
  
 列の値の範囲内のフィルターを適用する**sp_trace_setfilter**実行する必要が 2 回 - 1 回、大きい-よりも-または-equals を ('> =') 比較演算子、および、小さいよりも-または--equals で別の時間 ('< =') 演算子.  
  
 データ列のデータ型の詳細については、次を参照してください。、 [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|0|エラーなし。|  
|1|不明なエラー。|  
|2|トレースは現在実行中です。 この結果、エラーが発生したときにトレースを変更します。|  
|4|指定された列が無効です。|  
|5|指定した列にはフィルターを適用できません。 のみこの値が返される**sp_trace_setfilter**します。|  
|6|指定した比較演算子は無効です。|  
|7|指定した論理演算子は無効です。|  
|9|指定したトレース ハンドルは無効です。|  
|13|メモリ不足。 指定したアクションを実行するための十分なメモリがない場合に返されます。|  
|16|関数は、このトレースは無効です。|  
  
## <a name="remarks"></a>コメント  
 **sp_trace_setfilter**は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンで使用可能な拡張のストアド プロシージャで実行される操作の多くを実行するストアド プロシージャ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 使用**sp_trace_setfilter**の代わりに、 **xp_trace_set\*フィルター**を作成するストアド プロシージャを拡張するには、適用、削除、またはトレースのフィルターを操作します。 詳細については、次を参照してください。[トレースをフィルター処理](../../relational-databases/sql-trace/filter-a-trace.md)します。  
  
 特定の列のすべてのフィルターは、1 回実行でまとめて有効にする必要があります**sp_trace_setfilter**します。 たとえば場合は、ユーザーがアプリケーション名の列と 1 つのフィルターを username 列に 2 つのフィルターを適用しようとすると、ユーザー必要がありますフィルターを指定、アプリケーション名のシーケンスで。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ユーザーが 1 つのストアド プロシージャの呼び出しでアプリケーション名でフィルターを指定する場合で、後にフィルターをユーザー名、アプリケーション名の後に別のフィルターを返します。  
  
 パラメーターのすべての SQL トレース ストアド プロシージャ (**sp_trace_xx**) は厳密に型指定されます。 これらのパラメーターが、引数の説明で指定されている正しいデータ型で呼び出されないと、このストアド プロシージャではエラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER TRACE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、トレースの 3 つのフィルターを設定する`1`します。 フィルター`N'SQLT%'`と`N'MS%'`1 つの列を操作 (`AppName`、値`10`) を使用して、"`LIKE`"比較演算子。 フィルター `N'joe'` は、"`UserName`" 比較演算子を使用して別の列 (`11`、値 `EQUAL`) に適用されます。  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>参照  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
