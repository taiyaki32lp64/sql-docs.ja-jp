---
title: sys.sp_xtp_control_proc_exec_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 14c45f5ba725ef8d9cc498b1049c5a71c80a6d7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909220"
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  インスタンスのネイティブ コンパイル ストアド プロシージャの統計コレクションを有効にします。  
  
 ネイティブ コンパイル ストアド プロシージャのクエリ レベルで統計コレクションを有効にするのを参照してください。 [sys.sp_xtp_control_query_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>引数  
 @new_collection_value = *value*  
 プロシージャ レベルの統計コレクションがオン (1) かどうかを決定します。 または off (0)。  
  
 @new_collection_value 0 に設定されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]したり、データベースを起動します。  
  
 @old_collection_value = *value*  
 現在の状態を返します。  
  
## <a name="return-code"></a>リターン コード  
 成功した場合は 0。 エラーの 0 以外の値。  
  
## <a name="permissions"></a>アクセス許可  
 固定 sysadmin ロールのメンバーシップが必要です。  
  
## <a name="code-samples"></a>コード サンプル  
 設定する@new_collection_valueとクエリの値を @new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
