---
title: syscollector_collection_items (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78e8211c10d019c3b2a8c2435c5ddde8f8182a14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060412"
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクション セット内のアイテムに関する情報を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|コレクション セットを識別します。 NULL 値は許可されません。|  
|**collection_item_id**|**int**|コレクション セット内のアイテムを識別します。 NULL 値は許可されません。|  
|**collector_type_uid**|**uniqueidentifier**|コレクター型の識別に使用する GUID です。 NULL 値は許可されません。|  
|**name**|**nvarchar (4000)**|コレクション セットの名前です。 NULL 値が許可されます。|  
|**frequency**|**int**|コレクション アイテムでデータを収集する頻度です。 NULL 値は許可されません。|  
|**parameters**|**xml**|コレクション アイテムに関連付けられたコレクター型のパラメーター化を定義します。 このコレクション アイテムの XML スキーマが検証されると、XML スキーマ (XSD) に格納されている、 **parameter_schema**の特定のコレクター型。 NULL 値が許可されます。 詳細については、次を参照してください。 [syscollector_collector_types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)します。|  
  
## <a name="permissions"></a>アクセス許可  
 SELECT 権限が必要**dc_operator**、 **dc_proxy**します。  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
