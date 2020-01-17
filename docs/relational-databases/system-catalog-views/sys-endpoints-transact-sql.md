---
title: sys.endpoints (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: b814f8cb0013a202f88aba76b99cf52c49dd1c1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061409"
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  システムで作成されたエンドポイントごとに 1 行が含まれています。 システムの 1 つのエンドポイントは常にします。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|エンドポイントの名前。 サーバー内で一意です。 NULL 値は許可されません。|  
|**endpoint_id**|**int**|エンドポイントの ID。 サーバー内で一意です。 65536 より小さい ID のエンドポイントは、システム エンドポイントです。 NULL 値は許可されません。|  
|**principal_id**|**int**|作成してこのエンドポイントを所有しているサーバー プリンシパルの ID。 NULL 値が許可されます。|  
|**protocol**|**tinyint**|エンドポイントのプロトコル。<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = 名前付きパイプ<br /><br /> 4 = 共有メモリ<br /><br /> 5 = 仮想インターフェイス アダプター (VIA)<br /><br /> NULL 値は許可されません。|  
|**protocol_desc**|**nvarchar(60)**|エンドポイントのプロトコルの説明です。 NULL 値を許容します。 次のいずれかの値です。<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **使用して**に注意してください。VIA プロトコルは非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**type**|**tinyint**|エンドポイントのペイロードの種類。<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> NULL 値は許可されません。|  
|**type_desc**|**nvarchar(60)**|エンドポイント ペイロードの種類の説明です。 NULL 値が許可されます。 次のいずれかの値です。<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**state**|**tinyint**|エンドポイントの状態。<br /><br /> 0 = STARTED、リッスンしていると、要求を処理します。<br /><br /> 1 = STOPPED、リッスンしている場合が、要求を処理しません。<br /><br /> 2 = 無効、リッスンしていません。<br /><br /> 既定の状態には 1 です。 NULL 値が許可されます。|  
|**state_desc**|**nvarchar(60)**|エンドポイントの状態の説明です。<br /><br /> 開始 = リスニングおよび要求を処理します。<br /><br /> STOPPED = 要求のリスニング中で、処理は行っていません。<br /><br /> DISABLED = リスニングしていません。<br /><br /> 既定の状態は STOPPED です。<br /><br /> NULL 値が許可されます。|  
|**is_admin_endpoint**|**bit**|エンドポイントを使用して管理するかどうかを示します。<br /><br /> 0 = 管理者用以外のエンドポイント。<br /><br /> 1 = エンドポイントは、管理エンドポイントです。<br /><br /> NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
