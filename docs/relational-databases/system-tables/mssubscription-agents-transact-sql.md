---
title: MSsubscription_agents (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3354f69f92cbbbaa9d60ae8ed6352a0b3be6ab52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139792"
---
# <a name="mssubscription_agents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_agents**テーブルは、ディストリビューション エージェントおよび更新可能なサブスクリプションのトリガーによってサブスクリプションのプロパティを追跡するために使用されます。 このテーブルは、サブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|行の ID。|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**subscription_type**|**int**|サブスクリプションのタイプです。<br /><br /> 0 = プッシュ。<br /><br /> 1 = プル<br /><br /> 2 = プル匿名です。|  
|**queue_id**|**sysname**|ID、[!INCLUDE[msCoName](../../includes/msconame-md.md)]パブリッシャー側でキューのメッセージします。 *queue_id*に設定されている**SQL**の SQL ベースのキューを更新しています。|  
|**update_mode**|**tinyint**|更新の種類:<br /><br /> **0** = 読み取り専用です。<br /><br /> **1** = 即時更新します。<br /><br /> **2** = メッセージ キューを使用するキュー更新。<br /><br /> **3**イミディ エイト = メッセージ キューを使用してフェールオーバーとしてキュー更新で更新します。<br /><br /> **4** = SQL Server キューを使用するキュー更新。<br /><br /> **5** = SQL Server キューを使用して、キュー更新フェールオーバーを行う即時更新します。|  
|**failover_mode**|**bit**|更新のフェールオーバー タイプが選択された場合、そのタイプは次のいずれかです。<br /><br /> **0** = 即時更新が使用されています。 フェールオーバーが有効になっていません。<br /><br /> **1** = キュー更新が使用されています。 フェールオーバーが有効になっているとします。 フェールオーバーに使用されているキューがで指定された、 *update_mode*値。|  
|**spid**|**int**|現在実行中または稼動した直後のディストリビューション エージェントによって使用される接続のシステム プロセス ID。|  
|**login_time**|**datetime**|日付と時刻が現在実行中、または稼動した直後のディストリビューション エージェント接続の。|  
|**allow_subscription_copy**|**bit**|サブスクリプション データベースをコピーすることが許可されているかどうかを指定します。|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|アタッチされたサブスクリプションのバージョンを表す一意の識別子。|  
|**last_sync_status**|**int**|現在実行中、または稼動した直後のディストリビューション エージェントの最終実行状態。 ステータスの値が示す内容は次のとおりです。<br /><br /> **1** = 開始します。<br /><br /> **2** = に成功しました。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態です。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗します。|  
|**last_sync_summary**|**sysname**|現在実行中、または稼動した直後のディストリビューション エージェントの最後のメッセージ。 ステータスの値が示す内容は次のとおりです。<br /><br /> **開始します。**<br /><br /> **成功しました。**<br /><br /> **進行中です。**<br /><br /> **アイドル状態です。**<br /><br /> **再試行してください。**<br /><br /> **失敗します。**|  
|**last_sync_time**|**datetime**|日付と時刻を*last_sync_summary*と*last_sync_status*列が更新されました。 プルまたは匿名ディストリビューション エージェントが sql Server エージェント サービス ジョブとして実行されているこれらの列を更新できません。 この場合、履歴情報がジョブ履歴テーブルに代わりに記録されます。|  
|**queue_server**|**sysname**|内部使用のみです。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
