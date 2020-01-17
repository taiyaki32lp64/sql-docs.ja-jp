---
title: MSagentparameterlist (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0ba22c75e36cc927fbd923af25aad48b3d02801
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119249"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagentparameterlist**テーブルがレプリケーション エージェント パラメーターの情報を保持し、特定のエージェントの種類に設定できるパラメーターを指定するために使用します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|エージェントの種類:<br /><br /> **1** = スナップショット エージェント。<br /><br /> **2** = ログ リーダー エージェント。<br /><br /> **3** = ディストリビューション エージェント。<br /><br /> **4**マージ エージェントを = です。<br /><br /> **9** = キュー リーダー エージェント。|  
|**parameter_name**|**sysname**|有効なエージェント パラメーターの名前です。|  
|**default_value**|**nvarchar (4000)**|NULL がこのような値が存在しないことを示す、エージェント パラメーターの既定値。|  
|**min_value**|**int**|NULL に下限示しますなしに、エージェント パラメーターの下限の境界を設定します。|  
|**max_value**|**int**|エージェント パラメーターの上限を設定します。NULL は上限がないことを示します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
