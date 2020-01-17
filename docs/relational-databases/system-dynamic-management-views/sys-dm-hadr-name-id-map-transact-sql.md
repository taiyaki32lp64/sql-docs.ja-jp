---
title: sys.dm_hadr_name_id_map (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4fc446efc410ff13d5697c7ab195e3e3895b4839
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900432"
---
# <a name="sysdmhadrnameidmap-transact-sql"></a>sys.dm_hadr_name_id_map (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Always On 可用性グループのマッピングを示していますの現在のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が 3 つの一意の Id に参加して: 可用性グループ ID、WSFC リソース ID、および WSFC グループ id。 このマッピングの目的は、WSFC リソースまたは WSFC グループの名前が変更されるシナリオを処理することです。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar (256)**|可用性グループの名前。 これは、ユーザー指定の名前で、Windows Server フェールオーバー クラスター (WSFC) クラスター内で一意である必要があります。|  
|**ag_id**|**uniqueidentifier**|可用性グループの一意の識別子 (GUID)。|  
|**ag_resource_id**|**nvarchar (256)**|WSFC クラスターのリソースとしての可用性グループの一意な ID。|  
|**ag_group_id**|**nvarchar (256)**|可用性グループの一意な WSFC グループ ID。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
