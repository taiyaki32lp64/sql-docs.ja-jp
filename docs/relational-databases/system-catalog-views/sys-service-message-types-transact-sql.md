---
title: sys.service_message_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: stevestein
ms.author: sstein
ms.openlocfilehash: 560ee8a4ccc03f747df2b475394af092db589e7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078740"
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このカタログ ビューには、service broker に登録されているメッセージの種類ごとに 1 行が含まれています。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|メッセージ型の名前。データベース内で一意です。 Null を許容しません。|  
|**message_type_id**|**int**|メッセージ型の識別子。データベース内で一意です。 Null を許容しません。|  
|**principal_id**|**int**|このメッセージ型を所有するデータベース プリンシパルの識別子。 NULL 値を許容します。|  
|**validation**|**char(2)**|この種類のメッセージを送信する前にブローカーで実行される検証。 Null を許容しません。 次のいずれかです。<br /><br /> N = なし<br /><br /> X = XML<br /><br /> E = 空|  
|**validation_desc**|**nvarchar(60)**|この型のメッセージを送信する前に、ブローカーで実行される検証の説明。 NULL 値を許容します。 次のいずれかです。<br /><br /> なし<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|XML スキーマを使用する検証の場合、使用されるスキーマ コレクションの識別子。<br /><br /> それ以外の場合は NULL です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
