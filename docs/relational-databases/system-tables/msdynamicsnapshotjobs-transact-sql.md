---
title: MSdynamicsnapshotjobs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8822b0e7c56fe109a251365050f5aed9cdef178
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907366"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotjobs**テーブルは、フィルター選択されたデータ スナップショットの生成に適用されるパラメーター化された行フィルターの情報を追跡します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|フィルター選択されたデータ スナップショット ジョブの ID。|  
|**name**|**sysname**|フィルター選択されたデータ スナップショット ジョブの名前。|  
|**pubid**|**uniqueidentifier**|このパブリケーションの一意な識別番号です。|  
|**job_id**|**uniqueidentifier**|ディストリビューターで SQL Server エージェント ジョブの ID。|  
|**agent_id**|**int**|SQL Server エージェントの ID。|  
|**dynamic_filter_login**|**sysname**|評価するために使用される値、 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)パブリケーションに対して定義されているパラメーター化された行フィルター内の関数。|  
|**dynamic_filter_hostname**|**sysname**|評価するために使用される値、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)パブリケーションに対して定義されているパラメーター化された行フィルター内の関数。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|場所、スナップショット ファイルが読み取られる場合からフィルター選択されたデータ スナップショット フォルダーへのパスが使用されます。|  
|**partition_id**|**int**|ジョブが属しているデータのパーティションの ID。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
