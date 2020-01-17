---
title: MSmerge_generation_partition_mappings (T-sql)
description: マージパブリケーションのパーティションに対する変更を追跡するために使用される MSmerge_generation_partition_mappings ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_generation_partition_mappings_TSQL
- MSmerge_generation_partition_mappings
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_generation_partition_mappings system table
ms.assetid: 443a4024-ce48-4772-9ee5-95bd6fb6476b
author: stevestein
ms.author: sstein
ms.openlocfilehash: a43f4b3fac5f237904d0160ccfbde4b88f9a3616
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322112"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_generation_partition_mappings**テーブルは、マージパブリケーションのパーティションに対する変更を追跡するために使用されます。 このテーブルは、パブリケーションデータベースおよび scubscription データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|マージ パブリケーションを識別します。|  
|**generation**|**bigint**|生成値。|  
|**partition_id**|**通り**|パーティションを識別します。|  
|**changecount**|**通り**|パーティションが変更された回数。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
