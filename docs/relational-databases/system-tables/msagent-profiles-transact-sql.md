---
title: MSagent_profiles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5147ef1f482850b55a5d01a476b1981dfa012e5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021048"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_profiles**テーブルに定義されているレプリケーション エージェントのプロファイルごとに 1 つの行が含まれています。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|プロファイルの id です。|  
|**profile_name**|**sysname**|エージェントの種類に固有のプロファイル名です。|  
|**agent_type**|**int**|エージェントの種類:<br /><br /> **1** = スナップショット エージェント<br /><br /> **2** = ログ リーダー エージェント<br /><br /> **3** = ディストリビューション エージェント<br /><br /> **4** = マージ エージェント<br /><br /> **9** = キュー リーダー エージェント|  
|**type**|**int**|プロファイルの種類です。<br /><br /> **0** = システム**1** = カスタム|  
|**description**|**nvarchar(3000)**|プロファイルの説明。|  
|**def_profile**|**bit**|このプロファイルは、このエージェントの種類の既定値であるかどうかを指定します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
