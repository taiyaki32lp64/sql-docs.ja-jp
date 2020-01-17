---
title: MSmerge_metadataaction_request (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
author: stevestein
ms.author: sstein
ms.openlocfilehash: 09f3fa61a1f79e98b8cd3330a03361b1b6a5c507
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106369"
---
# <a name="msmerge_metadataaction_request-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_metadataaction_request**テーブルには、必要な各補正アクションに対して 1 行が格納されます。 エントリを作成し、Web 同期を使用して、エラーが発生し、同期を再試行する必要がある場合、 **MSmerge_metadataaction_request**します。 以降のマージのアップロード フェーズでは、同期されているパブリケーションに属するすべてのアーティクルに対して要求がこのテーブルから取得され、アップロードされます。 同期が正常に完了すると、対応する行で、 **MSmerge_metadataaction_request**テーブルを削除します。 このテーブルは、パブリケーション データベースでパブリッシャーとサブスクライバー側でサブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネームです。|  
|**rowguid**|**uniqueidentifier**|特定の行の行識別子。|  
|**action**|**tinyint**|必要な補正アクションの識別子。|  
|**generation**|**bigint**|補正アクションを必要とする生成の値。|  
|**changed**|**int**|内部使用のみ。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [マージ レプリケーションの Web 同期](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
