---
title: sys.service_queue_usages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_queue_usages
- sys.service_queue_usages_TSQL
- service_queue_usages
- service_queue_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queue_usages catalog view
ms.assetid: d58dcdaf-f82d-43d9-941b-f520581442bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8b1cd1c1688922404b882069d9e100504dfbcb14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078715"
---
# <a name="sysservicequeueusages-transact-sql"></a>sys.service_queue_usages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サービスとサービス キュー間の参照ごとに 1 行のデータを返すカタログ ビューです。 1 つのサービスは 1 つのキューにのみ関連付けることができます。 キューは、複数のサービスに関連付けることができます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|サービスの識別子です。 データベース内で一意です。 Null を許容しません。|  
|**service_queue_id**|**int**|サービスによって使用されるサービス キューの識別子。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [sys.services &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)  
  
  
