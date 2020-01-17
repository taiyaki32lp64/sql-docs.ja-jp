---
title: sysmergesubscriptions (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd32e7224b66c012d3422a3754cb0b4e0ca325b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029773"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既知のサブスクライバーごとに 1 つの行が含まれていて、パブリッシャー側でのローカル テーブルです。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|サーバーの ID です。 サブスクリプション データベースのコピーを別のサーバーに移行するときに、サーバー固有の値を srvid フィールドをマップするために使用します。|  
|db_name|**sysname**|サブスクライブするデータベースの名前。|  
|pubid|**uniqueidentifier**|現在のサブスクリプションの作成元となるパブリケーションの ID。|  
|datasource_type|**int**|データ ソースの種類:<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** jet OLE DB を = です。|  
|subid|**uniqueidentifier**|サブスクリプションの一意な ID 番号です。|  
|replnickname|**[バイナリ]**|レプリカの圧縮されたニックネームです。|  
|replicastate|**uniqueidentifier**|特定の値をパブリッシャー、サブスクライバーで値を比較することで、前回の同期が成功したかどうかに使用される一意の識別子。|  
|status|**tinyint**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブです。<br /><br /> **1** = アクティブ。<br /><br /> **2** = を削除します。|  
|subscriber_type|**int**|サブスクライバーの種類。<br /><br /> **1**グローバル =。<br /><br /> **2**ローカルを = です。<br /><br /> **3** = 匿名です。|  
|subscription_type|**int**|サブスクリプションの種類です。<br /><br /> **0** = プッシュ。<br /><br /> **1** = プルします。<br /><br /> **2** = 匿名です。|  
|sync_type|**tinyint**|同期の種類。<br /><br /> **1** = 自動。<br /><br /> **2** = 同期なし。|  
|description|**nvarchar (255)**|サブスクリプションの簡単な説明。|  
|priority|**real**|サブスクリプションの優先度を指定し、優先度に基づく競合解決を実装できるようにします。 等しい**0.00**のすべてのローカルまたは匿名サブスクリプションです。|  
|recgen|**bigint**|最後に受信した生成結果の数。|  
|recguid|**uniqueidentifier**|前回受信した generation 値の一意な ID です。|  
|sentgen|**bigint**|最後に送信された生成結果の数。|  
|sentguid|**uniqueidentifier**|最後に送信された生成結果の一意の ID。|  
|schemaversion|**int**|前回受信したスキーマの数。|  
|される|**uniqueidentifier**|前回受信したスキーマの一意な ID です。|  
|last_validated|**datetime**|**Datetime**サブスクライバー データの最後に正常に検証します。|  
|attempted_validate|**datetime**|最後の**datetime**サブスクリプションの検証が試行されたことです。|  
|last_sync_date|**datetime**|**Datetime**同期します。|  
|last_sync_status|**int**|サブスクリプションの状態です。<br /><br /> **0** = すべてのジョブが開始を待機しています。<br /><br /> **1** = 1 つまたは複数のジョブを開始します。<br /><br /> **2** = すべてのジョブが正常に実行されました。<br /><br /> **3** = 少なくとも 1 つジョブを実行します。<br /><br /> **4** = すべてのジョブがスケジュールされ、アイドル状態です。<br /><br /> **5** = 少なくとも 1 つジョブが前回のエラーの後に実行しようとしています。<br /><br /> **6** = 少なくとも 1 つが正常に実行するジョブが失敗しました。|  
|last_sync_summary|**sysname**|最後の同期の結果の説明です。|  
|metadatacleanuptime|**datetime**|最後の**datetime**その有効期限が切れたメタデータがマージ レプリケーション システム テーブルから削除されました。|  
|partition_id|**int**|サブスクリプションが所属する事前計算済みパーティションを識別します。|  
|cleanedup_unsent_changes|**bit**|未送信の変更をサブスクライバー側でクリーンアップされているは、そのメタデータを識別します。|  
|replica_version|**int**|サブスクリプションが所属するサブスクライバー用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンを識別します。次のいずれかの値になります。<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|内部使用のみです。|  
|application_name|**nvarchar(128)**|内部使用のみです。|  
|subscriber_number|**int**|内部使用のみです。|  
|last_makegeneration_datetime|**datetime**|最後の**datetime** makegeneration プロセスがパブリッシャーに対して実行されました。 詳細については、-makegenerationinterval パラメーターを参照してください。 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
