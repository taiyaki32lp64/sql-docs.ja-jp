---
title: MSpeer_originatorid_history (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_originatorid_history_TSQL
- MSpeer_originatorid_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_originatorid_history
ms.assetid: c1f53d0f-4080-43ff-be38-2b10395c68c9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 95c641e094e9df405d1674c3c3c81ffa43da9d7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069047"
---
# <a name="mspeer_originatorid_history-transact-sql"></a>MSpeer_originatorid_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トポロジに定義された発信元 ID ごとに 1 行のデータを格納します。 これには、アクティブではなくなったノードの ID が含まれています。 このテーブルは、競合検出の対象とする新しいノードを構成する際、指定した発信元 ID が既に使用されていないかどうかを確認するために使用されます。 このテーブルは、パブリケーション データベース内に保存されます。 競合の検出の詳細については、次を参照してください。[ピア ツー ピア レプリケーションにおける競合検出](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|originator_publication|**sysname**|発信者 ID が指定されたパブリケーションです。|  
|originator_id|**int**|競合検出のためにトポロジの各ノードを識別する数値です。|  
|originator_node|**sysname**|発信者 ID が指定されたサーバー インスタンスです。|  
|originator_db|**sysname**|発信者 ID が指定されたパブリケーション データベースです。|  
|originator_db_version|**int**|発信元のデータベースのバージョン番号識別子。|  
|originator_version|**int**|パブリッシャーのバージョン番号を識別します。|  
|inserted_date|**datetime**|発信元 ID の行がこのテーブルに挿入された日時です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
