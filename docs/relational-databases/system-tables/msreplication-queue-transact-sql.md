---
title: MSreplication_queue (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: stevestein
ms.author: sstein
ms.openlocfilehash: 914cf3ad65c881383a6d625c07d4fb5ed028b36a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080015"
---
# <a name="msreplication_queue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queue** SQL ベースを使用するキュー更新サブスクリプションのキューに置かれたすべてによって発行されたキューに登録されたコマンドを格納する、テーブルがレプリケーション プロセスによって使用されます。 このテーブルは、サブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**tranid**|**sysname**|キューに入れられたコマンドが実行されたときのトランザクション ID。|  
|**data**|**varbinary(8000)**|キューに登録されたコマンドに関する情報を格納するパック バイト ストリームです。|  
|**datalen**|**int**|データのバイト単位の長さ。|  
|**commandtype**|**int**|キューに登録されるコマンドのタイプです。<br /><br /> 1 = トランザクション内のユーザー コマンド。<br /><br /> 2 = サブスクリプション同期コマンド|  
|**insertdate**|**datetime**|挿入日時です。|  
|**orderkey**|**bigint**|単調に増加する id 列です。|  
|**cmdstate**|**bit**|コマンドの状態:<br /><br /> 0 = 完了します。<br /><br /> 1 = 部分です。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
