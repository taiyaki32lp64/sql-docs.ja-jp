---
title: MSsubscription_articles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8518c787f876152787ee30a20b9f25f936b9fa86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139777"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_articles**テーブルには、キュー サブスクリプション内のアーティクルに関する情報が含まれています。 このテーブルは、レプリケーションの種類がキュー更新の場合と、フェールオーバーとしてキュー更新を行う即時更新の場合にのみ設定されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|アーティクルを処理するエージェントの ID|  
|**artid**|**int**|アーティクル ID を**sysarticles**テーブル。|  
|**article**|**sysname**|アーティクルの名前、 **sysarticles**テーブル。|  
|**dest_table**|**sysname**|変換先テーブルの名前、 **sysarticles**テーブル。|  
|**owner**|**sysname**|サブスクリプションの所有者|  
|**cft_table**|**sysname**|このアーティクルは、キュー更新レプリケーションの種類の競合テーブルの名前。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
