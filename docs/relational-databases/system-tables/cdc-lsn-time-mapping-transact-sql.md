---
title: cdc.lsn_time_mapping (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1e89e67b49498320e4500b99332fc5584d5f38d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066669"
---
# <a name="cdclsn_time_mapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更テーブルの行を持つトランザクションごとに 1 つの行を返します。 このテーブルは、トランザクションのコミット ログ シーケンス番号 (LSN) コミットの値と時刻の間でマップを使用します。 エントリが記録されますの変更テーブル エントリはありません。 これにより、変更アクティビティが少ないか、まったくない場合に、LSN 処理の完了をテーブルに記録できます。  
  
 システム テーブルに対して直接クエリを実行することは、できるだけ避けてください。 代わりに、実行、 [sys.fn_cdc_map_lsn_to_time &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)と[sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)システム関数。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|コミットされたトランザクションの LSN。|  
|**tran_begin_time**|**datetime**|LSN に関連付けられているトランザクションの開始時刻。|  
|**tran_end_time**|**datetime**|トランザクションの終了時刻。|  
|**tran_id**|**varbinary(10)**|トランザクションの ID。|  
  
## <a name="see-also"></a>関連項目  
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [cdc.&#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
