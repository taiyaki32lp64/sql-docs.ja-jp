---
title: MSarticles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81598b65daf5fa7370004c890ab775e5b29b518f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132096"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSarticles**テーブルには、パブリッシャーによってレプリケートされる各アーティクルに対して 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**publication_id**|**int**|パブリケーションの ID。|  
|**article**|**sysname**|アーティクルの名前です。|  
|**article_id**|**int**|アーティクルの ID。|  
|**destination_object**|**sysname**|サブスクライバーで作成されるテーブルの名前。|  
|**source_owner**|**sysname**|パブリッシャー上の元のテーブルのスキーマの名前です。|  
|**source_object**|**sysname**|追加するアーティクルのソース オブジェクトの名前。|  
|**description**|**nvarchar (255)**|この記事の説明です。|  
|**destination_owner**|**sysname**|サブスクライバーで作成されたテーブルのスキーマの名前。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
