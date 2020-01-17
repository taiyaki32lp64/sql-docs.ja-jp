---
title: sys.sp_xtp_control_query_exec_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd8ee38dc4ac1a8fd3a729d94744d3fd98f78875
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017849"
---
# <a name="sysspxtpcontrolqueryexecstats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  インスタンスに関するすべてのネイティブ コンパイル ストアド プロシージャ、または特定のネイティブ コンパイル ストアド プロシージャのクエリごとの統計コレクションを有効にします。  
  
 統計コレクションを有効にすると、パフォーマンスが低下します。 のみ、1 つまたはいくつかのネイティブ コンパイル ストアド プロシージャのトラブルシューティングを行う必要がある場合に、これらのいくつかネイティブ コンパイル ストアド プロシージャの統計コレクションを有効にすることができます。  
  
 すべてのネイティブ コンパイル ストアド プロシージャのプロシージャ レベルで統計コレクションを有効にするのを参照してください。 [sys.sp_xtp_control_proc_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>引数  
 @new_collection_value = *value*  
 プロシージャ レベルの統計コレクションがオン (1) かどうかを決定します。 または off (0)。  
  
 @new_collection_value 0 に設定されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を開始します。  
  
 @database_id = = *database_id*、 @xtp_object_id = *procedure_id*  
 ネイティブ コンパイル ストアド プロシージャのデータベース ID とオブジェクト ID。 インスタンスの統計コレクションが有効になっている場合 ([sys.sp_xtp_control_proc_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md))、ネイティブ コンパイル ストアド プロシージャの統計情報が収集されます。 インスタンスで統計コレクションを無効にすることも、個々 のネイティブ コンパイル ストアド プロシージャの統計情報の収集をオフは有効になりません。  
  
 使用[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)、 [sys.procedures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)、 [DB_ID &#40;TRANSACT-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)、または[OBJECT_ID &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/object-id-transact-sql.md)データベースとストアド プロシージャの Id を取得します。  
  
 @old_collection_value = *value*  
 現在の状態を返します。  
  
## <a name="return-code"></a>リターン コード  
 成功した場合は 0。 エラーの 0 以外の値。  
  
## <a name="permissions"></a>アクセス許可  
 固定 sysadmin ロールのメンバーシップが必要です。  
  
## <a name="code-sample"></a>コード サンプル  
 次のコード サンプルでは、すべてのネイティブ コンパイル ストアド プロシージャのインスタンスのしてから、特定のネイティブ コンパイル ストアド プロシージャの統計コレクションを有効にする方法を示します。  
  
```sql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
