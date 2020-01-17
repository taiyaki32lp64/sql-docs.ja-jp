---
title: sys.sp_xtp_merge_checkpoint_files (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73638d41c7a24a37c068d365771b4d0469a174d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041026"
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sys.sp_xtp_merge_checkpoint_files**指定トランザクション範囲内のすべてのデータとデルタ ファイルをマージします。  
  
 詳細については、次を参照してください。[の作成とメモリ最適化オブジェクト用ストレージの管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**注意**:このストアド プロシージャは非推奨[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]します。 これは、必要がなくなったら、使用できません開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]します。|  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 マージを呼び出す対象のデータベースの名前。 データベースにインメモリ テーブルがない場合、このプロシージャはユーザー エラーを返します。 データベースがオフラインの場合は、エラーを返します。  
  
 *lower_bound_Tid*  
 ように、データ ファイルのトランザクションの (bigint) 下限[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)マージの開始チェックポイント ファイルに対応します。 transactonId の値が無効であれば、エラーが生成されます。  
  
 *upper_bound_Tid*  
 ように、データ ファイルのトランザクションの (bigint) 上限[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)します。 transactonId の値が無効であれば、エラーが生成されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールと db_owner 固定データベース ロールが必要です。  
  
## <a name="remarks"></a>コメント  
 有効な範囲内のすべてのデータとデルタ ファイルをマージして、1 つのデータとデルタ ファイルを生成します。 このプロシージャではマージ ポリシーは無視されます。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
