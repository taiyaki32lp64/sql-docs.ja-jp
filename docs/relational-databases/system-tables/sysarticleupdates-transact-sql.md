---
title: sysarticleupdates (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d2e710bdbe8f026624ea71357afb6d204b333c91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130492"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  即時更新サブスクリプションをサポートするアーティクルごとに 1 つの行が含まれています。 このテーブルは、レプリケートされたデータベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルの一意な ID 番号を示す ID 列。|  
|**pubid**|**int**|そのアーティクルが属するパブリケーションの ID です。|  
|**sync_ins_proc**|**int**|挿入同期トランザクションを処理するストアド プロシージャの ID。|  
|**sync_upd_proc**|**int**|更新プログラムの同期トランザクションを処理するストアド プロシージャの ID。|  
|**sync_del_proc**|**int**|削除同期トランザクションを処理するストアド プロシージャの ID。|  
|**autogen**|**bit**|ストアド プロシージャが自動的に生成されることを示します。<br /><br /> **0** = false、自動ではありません。<br /><br /> **1**自動 = true、します。|  
|**sync_upd_trig**|**int**|アーティクル テーブルで、自動バージョン トリガーの ID。|  
|**conflict_tableid**|**int**|競合テーブルの ID。|  
|**ins_conflict_proc**|**int**|競合を書き込むために使用するプロシージャの ID、 **conflict_table**します。|  
|**identity_support**|**bit**|キュー更新を使用する場合、自動 id 範囲処理が有効にするかどうかを指定します。 **0**サポートの範囲は id がないことを意味します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
