---
title: MSpeer_conflictdetectionconfigrequest (T-sql)
description: ピアツーピアパブリケーションのトポロジ全体の構成要求を追跡するために使用される MSPeer_conflictdetectionconfigurerequest ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 090236bd5e0bd0429985ff9c54039a576950ec84
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322099"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ピア ツー ピア レプリケーションで、パブリケーションに対するトポロジ全体の構成要求を追跡するために使用されます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**通り**|競合構成要求を識別します。 [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)の request_id 列には、この値が使用されます。|  
|パブリケーション (publication)|**sysname**|競合構成要求が発行されたパブリケーションの名前です。|  
|sent_date|**/**|競合構成要求が開始された日付と時刻。|  
|timeout|**通り**|すべてのピアから競合情報が返されるのをプロシージャが待機する時間です。|  
|modified_date|**/**|フェーズが完了した日付と時刻。|  
|progress_phase|**nvarchar (32)**|次のいずれかの値を使用して、処理の現在のフェーズを識別します。<br /><br /> 開始済み<br /><br /> トポロジの探索<br /><br /> 収集 (ステータスを)<br /><br /> 収集された状態|  
|phase_timed_out|**bit**|現在のフェーズがタイムアウトしたかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
