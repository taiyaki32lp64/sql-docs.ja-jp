---
title: MSqreader_history (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
author: stevestein
ms.author: sstein
ms.openlocfilehash: f21873e8db662bc77bd1acbb5d48c6af49aba404
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032530"
---
# <a name="msqreader_history-transact-sql"></a>MSqreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSqreader_history**テーブルは、ローカル ディストリビューターに関連付けられているキュー リーダー エージェントの履歴行を保持します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|キュー リーダー エージェントの ID|  
|**publication_id**|**int**|パブリケーションの ID。|  
|**runstatus**|**int**|エージェントの実行状態。<br /><br /> **1** = 開始します。<br /><br /> **2** = 成功します。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態です。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗します。|  
|**start_time**|**datetime**|日付とエージェントのセッションが開始された時刻。|  
|**time**|**datetime**|最後にメッセージがログに記録された日時。|  
|**duration**|**int**|秒単位で、ログに記録されたセッション アクティビティの経過時間。|  
|**comments**|**nvarchar (255)**|説明のテキスト。|  
|**transaction_id**|**nvarchar(40)**|該当する場合は、メッセージが格納されているトランザクション ID。|  
|**transaction_status**|**int**|トランザクションの状態です。|  
|**transactions_processed**|**int**|セッションで処理されたトランザクションの累積数。|  
|**commands_processed**|**int**|セッション中に処理されたコマンド数の累計。|  
|**delivery_rate**|**float(53)**|1 秒あたりに配信される平均コマンド数。|  
|**transaction_rate**|**float(53)**|処理されたトランザクションの比率。|  
|**subscriber**|**sysname**|サブスクライバーの名前。|  
|**subscriberdb**|**sysname**|サブスクリプション データベースの名前。|  
|**error_id**|**int**|場合は 0、その番号を表す、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラー メッセージ。|  
|**timestamp**|**timestamp**|テーブルのタイムスタンプ列。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
