---
title: MSrepl_queuedtraninfo (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a94163e2fe4a1ed5be77dd4ae99f43d03cc35121
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079181"
---
# <a name="msrepl_queuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queuedtraninfo** SQL ベースのキューに置かれた更新を使用している、キューに置かれたすべての更新サブスクリプションによって発行されたキューに登録されたコマンドに関する情報を格納する、テーブルがレプリケーション プロセスによって使用されます。 このテーブルは、サブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**tranid**|**sysname**|キューに入れられたコマンドが実行されたときのトランザクション ID。|  
|**maxorderkey**|**bigint**|内部使用のみ。|  
|**commandcount**|**bigint**|内部使用のみ。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
