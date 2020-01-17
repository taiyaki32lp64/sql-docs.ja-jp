---
title: MSreplication_objects (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 058e1948fa79ed2ba250a4f4d504f95201d1e254
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079078"
---
# <a name="msreplication_objects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_objects**テーブルには、サブスクライバー データベースのレプリケーションに関連付けられているオブジェクトごとに 1 つの行が含まれています。 このテーブルは、サブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**object_name**|**sysname**|オブジェクトの名前。|  
|**object_type**|**char(2)**|オブジェクトの種類:<br /><br /> **u**テーブルを = です。<br /><br /> **t** = トリガーします。<br /><br /> **p**ストアド プロシージャを = です。|  
|**article**|**sysname**|オブジェクトが関連付けられているアーティクルの名前。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
