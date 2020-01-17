---
title: MSmerge_sessions (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 041b8a9123781ca270c3970a04c620b691e85230
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106352"
---
# <a name="msmerge_sessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_sessions**テーブルに履歴行以前のマージ エージェント ジョブ セッションの結果にはが含まれています。 このテーブルには、マージ エージェントが実行されるたびに、新しい行が追加されます。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージ エージェント ジョブ セッションの ID。|  
|**agent_id**|**int**|マージ エージェントの ID。|  
|**start_time**|**datetime**|ジョブの実行時に開始しました。|  
|**end_time**|**datetime**|ジョブの実行完了時刻。|  
|**duration**|**int**|累積的な期間 (秒)、このジョブ セッションのです。|  
|**delivery_time**|**int**|変更のバッチを適用するために要する秒数です。|  
|**upload_time**|**int**|変更をパブリッシャーにアップロードするために要する秒数です。|  
|**download_time**|**int**|変更をサブスクライバーにダウンロードするにかかった秒数です。|  
|**delivery_rate**|**float**|配信されたコマンド 1 秒あたりの平均数。|  
|**time_remaining**|**int**|アクティブなセッションのままに推定される秒数。|  
|**percent_complete**|**decimal**|アクティブなセッションで既に配信された総変更数の推定パーセンテージ。|  
|**upload_inserts**|**int**|パブリッシャーで適用される挿入の数。|  
|**upload_updates**|**int**|パブリッシャーで適用された更新数。|  
|**upload_deletes**|**int**|パブリッシャー側で適用される削除の数です。|  
|**upload_conflicts**|**int**|パブリッシャー側で変更を適用する間に発生した競合の数です。|  
|**upload_conflicts_resolved**|**int**|解決済みで、パブリッシャー側での変更を適用中に発生した競合の数。|  
|**upload_rows_retried**|**int**|パブリッシャーにアップロードされた行数のうち、再試行された行数。|  
|**download_inserts**|**int**|サブスクライバー側で適用される挿入の数です。|  
|**download_updates**|**int**|サブスクライバーで適用される更新プログラムの数。|  
|**download_deletes**|**int**|サブスクライバー側で適用される削除の数です。|  
|**download_conflicts**|**int**|サブスクライバーの変更を適用するときに発生した競合の数。|  
|**download_conflicts_resolved**|**int**|解決済みのサブスクライバーの変更を適用するときに発生した競合の数。|  
|**download_rows_retried**|**int**|サブスクライバーにダウンロードされた行数のうち、再試行された行数。|  
|**schema_changes**|**int**|セッション中に適用されたスキーマ変更の数。|  
|**metadata_rows_cleanedup**|**int**|メタデータの行の数クリーンアップ、セッション中にします。|  
|**runstatus**|**int**|実行ステータスです。<br /><br /> **1** = 開始します。<br /><br /> **2** = 成功します。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態です。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗します。|  
|**estimated_upload_changes**|**int**|推定数は、パブリッシャーで適用する必要を変更します。|  
|**estimated_download_changes**|**int**|サブスクライバーで適用する必要がある変更の推定数。|  
|**connection_type**|**int**|アップロード中に使用される接続。<br /><br /> **1** = ローカル エリア ネットワーク (LAN)。<br /><br /> **2** = ダイヤルアップ ネットワーク接続。<br /><br /> **3** = web 同期します。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
