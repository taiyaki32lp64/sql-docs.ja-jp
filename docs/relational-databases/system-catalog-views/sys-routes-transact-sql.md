---
title: sys.routes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bfdd322107da1a08edb3933aee9d5b79b6c2b47a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904434"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  このカタログ ビューには、ルートごとに 1 行が含まれています。 Service Broker では、ルートを使用してサービスのネットワーク アドレスを特定します。   

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|ルートは、データベース内で一意の名前です。 Null を許容しません。|  
|**route_id**|**int**|ルートの識別子です。 Null を許容しません。|  
|**principal_id**|**int**|ルートを所有するデータベース プリンシパルの識別子。 NULL 値を許容します。|  
|**remote_service_name**|**nvarchar (256)**|リモート サービスの名前。 NULL 値を許容します。|  
|**broker_instance**|**nvarchar(128)**|リモート サービスをホストしているブローカーの識別子です。 NULL 値を許容します。|  
|**lifetime**|**datetime**|日付と、ルートの有効期限が切れる時刻。 この値がローカル タイム ゾーンを使用しないことに注意してください。 代わりに、値は、UTC の有効期限の時間を示します。 NULL 値を許容します。|  
|**address**|**nvarchar (256)**|Service Broker リモート サービスのメッセージを送信する先のネットワーク アドレス。 NULL 値を許容します。 SQL Database マネージ インスタンスのアドレスをローカルにある必要があります。|  
|**mirror_address**|**nvarchar (256)**|ネットワーク アドレスで指定されたサーバーのミラーリング パートナーのアドレス。 NULL 値を許容します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
