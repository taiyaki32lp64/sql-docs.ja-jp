---
title: sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b230fb659b41f16541fd841f1ff8b6f03d19cee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120036"
---
# <a name="sysspxtpcheckpointforcegarbagecollection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  マークが不要な後のログ シーケンス番号 (LSN) とマージ操作で使用されるファイルのソースし、するガベージ コレクションのことができます。 また、関連付けられている LSN がファイルストリーム ガベージ コレクションにログの切り捨てポイントよりも低いファイルを移動します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>構文  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 ガベージ コレクションが実行されるデータベース。 既定値は現在のデータベースです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0。 エラーの 0 以外の値。  
  
## <a name="result-set"></a>結果セット  
 返される行には次の情報が含まれます。  
  
|[列]|説明|  
|------------|-----------------|  
|num_collected_items|ファイルストリーム ガベージ コレクションに移動されたファイルの数を示します。 これらのファイルのログ シーケンス番号 (LSN) は、ログの切り捨てポイントの LSN よりも小さい値になっています。|  
|num_marked_for_collection_items|LSN がログ末尾の LSN のログ ブロック Id で更新されたデータ/デルタ ファイルの数を示します。|  
|last_collected_xact_seqno|ファイルストリーム ガベージ コレクションにこれまで、ファイルが移動された最後の対応する LSN を返します。|  
  
## <a name="permissions"></a>アクセス許可  
 データベース所有者の権限が必要です。  
  
## <a name="sample"></a>サンプル  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
