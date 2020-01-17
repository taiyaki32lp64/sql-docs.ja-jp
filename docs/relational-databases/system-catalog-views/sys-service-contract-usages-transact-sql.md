---
title: sys.service_contract_usages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contract_usages
- sys.service_contract_usages
- sys.service_contract_usages_TSQL
- service_contract_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_usages catalog view
ms.assetid: 20af425e-1152-4a46-b1ac-94cff5fc9f02
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc2a41cb5f7bbd8e5b0b76ed7b571ffdf80a939f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132877"
---
# <a name="sysservicecontractusages-transact-sql"></a>sys.service_contract_usages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このカタログ ビューにはごとに 1 行が含まれています (サービス、コントラクト) のペア。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|コントラクトを使用してサービスの識別子です。 Null を許容しません。|  
|**service_contract_id**|**int**|サービスによって使用されるコントラクトの識別子。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
