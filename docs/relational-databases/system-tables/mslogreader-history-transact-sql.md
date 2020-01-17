---
title: MSlogreader_history (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9fbd2240bdeba50d8ae41bce8d3a8d58b28de036
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907296"
---
# <a name="mslogreader_history-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSlogreader_history**テーブルは、ローカル ディストリビューターに関連付けられているログ リーダー エージェントの履歴行を保持します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ログ リーダー エージェントの ID。|  
|**runstatus**|**int**|実行ステータスです。<br /><br /> 1 = 開始します。<br /><br /> 2 = 成功。<br /><br /> 3 = 実行中<br /><br /> 4 = Idle します。<br /><br /> 5 = 再試行<br /><br /> 6 = 失敗|  
|**start_time**|**datetime**|ジョブの実行開始時刻です。|  
|**time**|**datetime**|メッセージが記録された時刻。|  
|**duration**|**int**|メッセージ セッションの実行時間 (秒) です。|  
|**comments**|**nvarchar (255)**|メッセージ テキストです。|  
|**xact_seqno**|**varbinary(16)**|最後に処理されたトランザクション シーケンス番号です。|  
|**delivery_time**|**int**|時間の最初のトランザクションが配信されます。|  
|**delivered_transactions**|**int**|セッションに配信されたトランザクション数の合計。|  
|**delivered_commands**|**int**|セッションに配信されたコマンド数の合計。|  
|**average_commands**|**int**|セッションで配信される平均コマンド数。|  
|**delivery_rate**|**float**|配信されたコマンドを 1 秒あたりの平均です。|  
|**delivery_latency**|**int**|パブリッシュされたデータベースとディストリビューション データベースに入力されているコマンドまでの待機時間。 単位はミリ秒。|  
|**error_id**|**int**|内のエラーの ID、 **MSrepl_error**システム テーブル。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
|**updateable_row**|**bit**|設定**1**履歴行を上書きできる場合。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
