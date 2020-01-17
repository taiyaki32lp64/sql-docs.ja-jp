---
title: sys.services (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.services
- services
- services_TSQL
- sys.services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.services catalog view
ms.assetid: 16d0b0c5-5cce-469b-aa3d-4b9248e0c085
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19e65117a03de6b473eced3c7c1379943c851a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078663"
---
# <a name="sysservices-transact-sql"></a>sys.services (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このカタログ ビューには、データベース内の各サービスに 1 行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サービスの名前。大文字と小文字が区別されます。データベース内で一意です。 Null を許容しません。|  
|**service_id**|**int**|サービスの識別子です。 Null を許容しません。|  
|**principal_id**|**int**|このサービスを所有するデータベース プリンシパルの識別子。 NULL 値を許容します。|  
|**service_queue_id**|**int**|このサービスが使用するキューのオブジェクト id。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
