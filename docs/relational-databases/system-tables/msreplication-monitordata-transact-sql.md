---
title: MSreplication_monitordata (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 886240176188fdcea0c104ca366ec5451528312a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079140"
---
# <a name="msreplication_monitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_monitordata**テーブルには、監視対象サブスクリプションごとに 1 つの行で、レプリケーション モニターによって使用されるキャッシュ データが含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|日付とモニターのデータが更新された時刻。|  
|**computetime**|**int**|モニターのデータを計算する時間 (秒) が取得されます。|  
|**publication_id**|**int**|パブリケーション ID|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_srvid**|**int**|パブリッシャーのサーバー ID です。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_type**|**int**|パブリケーションで、これらの値のいずれかの種類:<br /><br /> **0** = トランザクション パブリケーション<br /><br /> **1** = スナップショット パブリケーション<br /><br /> **2** = マージ パブリケーション|  
|**agent_type**|**int**|レプリケーション エージェントの種類です。次のいずれかの値をとります。<br /><br /> **1** = スナップショット エージェント<br /><br /> **2** = ログ リーダー エージェント<br /><br /> **3** = ディストリビューション エージェント<br /><br /> **4** = マージ エージェント<br /><br /> **9** = キュー リーダー エージェント|  
|**agent_id**|**int**|レプリケーション エージェントの ID。|  
|**agent_name**|**sysname**|レプリケーション エージェント ジョブの名前。|  
|**job_id**|**uniqueidentifier**|レプリケーション エージェント ジョブの GUID です。|  
|**status**|**int**|これらの値のいずれかのレプリケーション エージェントの状態です。<br /><br /> **1** = 開始<br /><br /> **2** = に成功しました<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル状態<br /><br /> **5** = 再試行<br /><br /> **6** = に失敗しました|  
|**isagentrunningnow**|**bit**|かどうか、エージェント ジョブが現在実行中の値を示すフラグ**1**ジョブが実行されていることを意味します。|  
|**warning**|**int**|サブスクリプションによって生成されるしきい値警告です。次の 1 つ以上の値の論理和演算をとります。<br /><br /> **1** = の有効期間 - トランザクション パブリケーションに対するサブスクリプションが保有期間のしきい値を超えるによって保有期間のパーセンテージを超えました。<br /><br /> **2** = 待機時間、トランザクション パブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間 (秒)、しきい値を超えています。<br /><br /> **4** mergeexpiration = マージ パブリケーションに対するサブスクリプションが保有期間のしきい値を超えるによって、保有期間のパーセンテージを超えました。 8 = mergefastrunduration - マージ サブスクリプションの同期の完了にかかった時間、高速ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **16** = mergeslowrunduration - マージ サブスクリプションの同期の完了にかかった時間、低速またはダイヤルアップ ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **32** = mergefastrunspeed - 配信率マージ サブスクリプションの同期中の行が高速ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。<br /><br /> **64** mergeslowrunspeed - 配信率 = マージ サブスクリプションの同期中の行が低速またはダイヤルアップ ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。|  
|**last_distsync**|**datetime**|最後の日付と、ディストリビューション エージェントが実行された時刻が必要です。|  
|**agentstoptime**|**datetime**|エージェントが停止された日時です。|  
|**distdb**|**sysname**|サブスクリプションのディストリビューション データベースの名前。|  
|**retention**|**int**|パブリケーションの保有期間。|  
|**time_stamp**|**datetime**|内部使用のみ。|  
|**worst_latency**|**int**|トランザクション パブリケーションのログ リーダーまたはディストリビューション エージェントによって反映されるデータの変更を秒単位で最大待ち時間。|  
|**best_latency**|**int**|秒単位のトランザクション パブリケーションのログ リーダーまたはディストリビューション エージェントによって反映されるデータ変更で最も短い。|  
|**avg_latency**|**int**|平均待機時間、トランザクション パブリケーションのログ リーダーまたはディストリビューション エージェントによって反映されるデータの変更 (秒)。|  
|**cur_latency**|**int**|現在の実行中に、ログ リーダーまたはディストリビューション エージェントによって反映されるデータ変更を秒単位の待ち時間。|  
|**worst_runspeedPerf**|**int**|マージ パブリケーションの最長同期時間|  
|**best_runspeedPerf**|**int**|マージ パブリケーションの最短同期時間|  
|**average_runspeedPerf**|**int**|マージ パブリケーションの平均同期時間|  
|**mergePerformance**|**int**|サブスクリプションに対するすべての同期と比較した前回の同期のパフォーマンスです。前回の同期の配信速度を前回までのすべての配信速度の平均で割った値に基づいて算出されます。|  
|**mergelatestsessionrunduration**|**int**|実行、最新のマージ エージェントの継続時間。|  
|**mergelatestsessionrunspeed**|**float(53)**|実行、最新のマージ エージェントの配信率です。|  
|**mergelatestsessionconnectiontype**|**int**|接続のため、最新のマージ エージェントのセッションは、次の値のいずれかを指定できます。<br /><br /> **1** = ローカル エリア ネットワーク (LAN)<br /><br /> **2** = ダイヤルアップ ネットワーク接続|  
|**retention_period_unit**|**tinyint**|保有期間を定義するときに使用する単位を指定します。次のいずれかの値をとります。<br /><br /> **1** = 週<br /><br /> **2** = 月<br /><br /> **3** = 年|  
  
## <a name="see-also"></a>関連項目  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
