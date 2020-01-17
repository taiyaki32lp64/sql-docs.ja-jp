---
title: sysreplicationalerts (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6cbeab4c673390cb80300eb5ced2b4cb5c1bcf1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029738"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケーションの警告を発生を引き起こした条件についてを説明します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|アラートの ID。|  
|**status**|**int**|ユーザー定義の値です。<br /><br /> **0** = 非対処します。<br /><br /> **1** = サービスを提供します。|  
|**agent_type**|**int**|エージェントのタイプです。<br /><br /> **1** = スナップショット エージェント。<br /><br /> **2** = ログ リーダー エージェント。<br /><br /> **3** = ディストリビューション エージェント。<br /><br /> **4**マージ エージェントを = です。|  
|**agent_id**|**int**|テーブルからエージェント ID **MSsnapshot_agents**、 **MSlogreader_agents**、 **MSdistribution_agents**、または**MSmerge_agents**します。|  
|**error_id**|**int**|格納されているエラーの ID **MSrepl_errors**します。|  
|**alert_error_code**|**int**|このレコードにログインするときに発生した警告のメッセージ ID。|  
|**time**|**datetime**|レコードが挿入された時間。|  
|**publisher**|**sysname**|この警告を発生したエージェントに関係するパブリッシャー名です。|  
|**publisher_db**|**sysname**|この警告を発生したエージェントに関連付けられたパブリッシャーのデータベース。|  
|**publication**|**sysname**|この警告を発生したエージェントに関係するパブリケーションです。|  
|**publication_type**|**int**|パブリケーションの種類:<br /><br /> **0** = スナップショット。<br /><br /> **1** = トランザクション。<br /><br /> **2** = マージします。|  
|**subscriber**|**sysname**|このアラートが発生したエージェントに関連付けられているサブスクライバーの名前。|  
|**subscriber_db**|**sysname**|この警告を発生したエージェントに関連付けられたサブスクライバー データベースの名前。|  
|**article**|**sysname**|このアラートが発生したエージェントに関連付けられているアーティクルの名前。|  
|**destination_object**|**sysname**|アラートに関連付けられているサブスクリプションのテーブルの名前。|  
|**source_object**|**sysname**|アラートに関連付けられているパブリッシュされたテーブルの名前。|  
|**alert_error_text**|**ntext**|アラートのテキスト。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
