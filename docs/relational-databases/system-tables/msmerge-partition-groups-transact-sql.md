---
title: MSmerge_partition_groups (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: stevestein
ms.author: sstein
ms.openlocfilehash: 362735d33f835c7b66e4f0994fd5c4ff6f084f15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102193"
---
# <a name="msmerge_partition_groups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_partition_groups**テーブルでは、それぞれ特定のデータベースでパーティションを事前計算済みの 1 行が格納されます。 示されている列、だけでなく、1 つの列は、パラメーター化された行フィルターで使用される各関数は、このテーブルに追加されます。 たとえば、という名前の列**HOST_NAME**フィルターを使用している場合に、テーブルに追加、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)関数。 このパブリッシャーと同期された関数値の一意のセットごとに 1 つの行が格納されます。 これらの関数のすべてのまったく同じ値との同期、2 つ以上のサブスクライバーがこのテーブル内の同じ行を共有し、したがってすべて共有と同じパーティション id。このテーブルは、パブリケーション データベース内に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|事前計算済みパーティションの一意な ID 番号を示す ID 列です。|  
|**publication_number**|**smallint**|格納されているパブリケーションの番号**sysmergepublications**します。|  
|**maxgen_whenadded**|**bigint**|このテーブルに行が挿入される時点で、パブリッシャーで把握している最も古い generation 値です。|  
|**using_partition_groups**|**bit**|パーティションがこれらの値のいずれか、事前計算済みパーティションを使用するパブリケーションに属しているかどうかを示します。<br /><br /> **0** = パブリケーションは事前計算済みパーティションを使用しません。<br /><br /> **1**パブリケーションは事前計算済みパーティションを =<br /><br /> 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。|  
|**HOST_NAME_FN**|**nvarchar(128)**|パラメーター化された行フィルターを使用してパーティションを生成するときに指定された値。 詳しくは、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
