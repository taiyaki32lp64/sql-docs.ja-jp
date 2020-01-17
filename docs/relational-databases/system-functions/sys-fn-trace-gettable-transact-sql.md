---
title: sys.fn_trace_gettable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 18a6225bca9539f10c4dfea61e99d147cb188d4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059221"
---
# <a name="sysfntracegettable-transact-sql"></a>sys.fn_trace_gettable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のトレース ファイルの内容を表形式で返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>引数  
 '*filename*'  
 読み取る最初のトレース ファイルを指定します。 *ファイル名*は**nvarchar (256)** 、既定値はありません。  
  
 *number_files*  
 読み取るロールオーバー ファイルの数を指定します。 この数にはで指定された最初のファイルが含まれています*filename*します。 *number_files*は、 **int**します。  
  
## <a name="remarks"></a>コメント  
 場合*number_files*として指定されて**既定**、 **fn_trace_gettable**トレースの最後に達するまで、すべてのロール オーバー ファイルを読み取ります。 **fn_trace_gettable**指定したトレースの有効なすべての列を含むテーブルを返します。 詳細については、次を参照してください。 [sp_trace_setevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)します。  
  
 Fn_trace_gettable 関数はロール オーバー ファイルを読み取らないことに注意してください (を使用して、このオプションが指定されている場合、 *number_files*引数) 元のトレース ファイル名がアンダー スコアと数値が終了します。 ただし、この状況は、ファイルがロールオーバーされるときに自動的に追加されたアンダースコアおよび数値については該当しません。この問題に対処するには、元のファイル名のアンダースコアを削除してトレース ファイルの名前を変更します。 たとえば、元のファイルの名前は**Trace_Oct_5.trc**ロール オーバー ファイルの名前は**Trace_Oct_5_1.trc**、ファイルの名前を変更することができます**TraceOct5.trc**と**TraceOct5_1.trc**します。  
  
 この関数は、関数が実行されるインスタンス上でアクティブになっているトレースを読み取ることができます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーの ALTER TRACE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-fntracegettable-to-import-rows-from-a-trace-file"></a>A. fn_trace_gettable を使用してトレース ファイルから行をインポートする  
 次の例では`fn_trace_gettable`内で、`FROM`の句、`SELECT...INTO`ステートメント。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fntracegettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. fn_trace_gettable を使用して、SQL Server テーブルに読み込むことができる IDENTITY 列を含むテーブルを返す  
 次の例では、一部として関数を呼び出し、`SELECT...INTO`ステートメントでテーブルを返します、`IDENTITY`列をテーブルに読み込むことができます`temp_trc`。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
