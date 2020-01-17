---
title: dm_exec_compute_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d749b9a7d9689426bffafe20ee7ab46ce199ffbb
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254609"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>dm_exec_compute_pools (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|コンピューティングプールの名前。 NULL 値は許可されません。 既定`default`のコンピューティングプールに対してを返します。 |
|compute_pool_id|`int`|プールの一意の識別子。 このビューのキー。|  
|location|`sysname`|SQL ビッグデータクラスター内のコントローラーへのエンドポイント。 NULL 値は許可されません。 |

## <a name="permissions"></a>アクセス許可

で[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]は、 `VIEW SERVER STATE`権限が必要です。

## <a name="see-also"></a>参照

[概要[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)
