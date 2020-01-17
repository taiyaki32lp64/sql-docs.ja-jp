---
title: sys.conversation_priorities (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_priorities_TSQL
- conversation_priorities
- sys.conversation_priorities_TSQL
- sys.conversation_priorities
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], priorities
- Service Broker, conversations
- sys.conversation_priorities catalog view
ms.assetid: 7cbb9171-3310-4aae-8458-755c882d6462
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a1278426b6774c8f5c2d9bb13577e1499930c13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109469"
---
# <a name="sysconversationpriorities-transact-sql"></a>sys.conversation_priorities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに作成されたメッセージ交換の優先度ごとに 1 行のデータを格納します。この行の内容を次の表に示します。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|Priority_id|**int**|メッセージ交換の優先度を一意に識別する番号。 Null を許容しません。|  
|NAME|**sysname**|メッセージ交換の優先度の名前。 Null を許容しません。|  
|service_contract_id|**int**|メッセージ交換の優先度に指定されているコントラクトの識別子。 この列は、sys.service_contracts の service_contract_id 列に結合できます。 NULL 値を許容します。|  
|local_service_id|**int**|メッセージ交換の優先度のローカル サービスとして指定されているサービスの識別子。 この列は、sys.services の service_id 列に結合できます。 NULL 値を許容します。|  
|remote_service_name|**nvarchar (256)**|メッセージ交換の優先度のリモート サービスとして指定されているサービスの名前。 NULL 値を許容します。|  
|priority|**tinyint**|このメッセージ交換の優先度で指定されている優先順位。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、結合を使用してコントラクト名とローカル サービス名を表示することで、メッセージ交換の優先度を一覧表示します。  
  
```  
SELECT scp.name AS priority_name,  
       ssc.name AS contract_name,  
       ssvc.name AS local_service_name,  
       scp.remote_service_name,  
       scp.priority AS priority_level  
FROM sys.conversation_priorities AS scp  
    INNER JOIN sys.service_contracts AS ssc  
       ON scp.service_contract_id = ssc.service_contract_id  
    INNER JOIN sys.services AS ssvc  
       ON scp.local_service_id = ssvc.service_id  
ORDER BY priority_name, contract_name,  
         local_service_name, remote_service_name;  
  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.services &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)   
 [結合する&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-contracts-transact-sql.md)  
  
  
