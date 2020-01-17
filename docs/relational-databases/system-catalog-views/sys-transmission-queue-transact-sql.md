---
title: sys.transmission_queue (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bd461a677a7bfab145846baaf09c0a8a62d6f8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022597"
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このカタログ ビューは、転送キュー内のメッセージごとに 1 行のデータを格納します。ビューの内容を次の表に示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|このメッセージが属するメッセージ交換の識別子。 Null を許容しません。|  
|**to_service_name**|**nvarchar (256)**|このメッセージには、サービスの名前です。 NULL 値を許容します。|  
|**to_broker_instance**|**nvarchar(128)**|このメッセージがサービスをホストするブローカーの識別子。 NULL 値を許容します。|  
|**from_service_name**|**nvarchar (256)**|このメッセージはサービスの名前です。 NULL 値を許容します。|  
|**service_contract_name**|**nvarchar (256)**|このメッセージのメッセージ交換が従うコントラクトの名前です。 NULL 値を許容します。|  
|**enqueue_time**|**datetime**|メッセージがキューになった時刻。 この値には、インスタンスのローカルのタイム ゾーンに関係なく UTC が使用されます。 Null を許容しません。|  
|**message_sequence_number**|**bigint**|メッセージのシーケンス番号。 Null を許容しません。|  
|**message_type_name**|**nvarchar (256)**|メッセージのメッセージ型名。 NULL 値を許容します。|  
|**is_conversation_error**|**bit**|かどうかこのメッセージは、エラー メッセージです。<br /><br /> 0 = エラー メッセージではありません。<br /><br /> 1 = エラー メッセージです。<br /><br /> Null を許容しません。|  
|**is_end_of_dialog**|**bit**|かどうか、メッセージ交換の最後のメッセージです。 Null を許容しません。<br /><br /> 0 = メッセージ交換のメッセージの最後ではありません。<br /><br /> 1 = メッセージ交換の最後のメッセージです。<br /><br /> Null を許容しません。|  
|**message_body**|**varbinary(max)**|メッセージの本文。 NULL 値を許容します。|  
|**transmission_status**|**nvarchar (4000)**|メッセージがキューにある理由。 これは通常、メッセージ送信が失敗した理由を示すエラー メッセージです。 空白の場合、メッセージはまだ送信されていません。 NULL 値を許容します。|  
|**priority**|**tinyint**|このメッセージに割り当てられている優先度レベル。 Null を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
