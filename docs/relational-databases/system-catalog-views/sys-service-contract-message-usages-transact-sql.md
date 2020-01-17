---
title: sys.service_contract_message_usages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
author: stevestein
ms.author: sstein
ms.openlocfilehash: bca839c61a59c69a7f6cf7e659ad940864fcee37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132929"
---
# <a name="sysservicecontractmessageusages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  (コントラクト、メッセージの種類) ごとに 1 行を格納するカタログ ビューのペア。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|メッセージ型を使用するコントラクトの識別子。 Null を許容しません。|  
|**message_type_id**|**int**|コントラクトで使用されるメッセージの種類の識別子です。 Null を許容しません。|  
|**is_sent_by_initiator**|**bit**|メッセージの種類は、メッセージ交換の発信側から送信できます。 Null を許容しません。|  
|**is_sent_by_target**|**bit**|メッセージの種類は、交換の発信先で送信できます。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
