---
title: MSdistribution_agents (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c138f2e97bf80f00f77c519bb4b9467c715f95b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907411"
---
# <a name="msdistribution_agents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdistribution_agents**テーブルには、ローカルのディストリビューターで実行されるディストリビューション エージェントごとに 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ディストリビューション エージェントの ID。|  
|**name**|**nvarchar(100)**|ディストリビューション エージェントの名前。|  
|**publisher_database_id**|**int**|パブリッシャー データベースの ID。|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**subscriber_id**|**smallint**|よく知られているエージェントだけが使用するサブスクライバーの ID。 匿名のエージェントに対しては、予約済みとなります。|  
|**@subscriber_db**|**sysname**|サブスクリプション データベースの名前。|  
|**subscription_type**|**int**|サブスクリプションの種類です。<br /><br /> **0** = プッシュ。<br /><br /> **1** = プルします。<br /><br /> **2** = 匿名です。|  
|**local_job**|**bit**|ローカル ディストリビューターで SQL Server エージェント ジョブがあるかどうかを示します。|  
|**job_id**|**binary(16)**|ジョブの識別番号。|  
|**subscription_guid**|**binary(16)**|エージェントのサブスクリプションの GUID 値。|  
|**profile_id**|**int**|ある構成 ID、 [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)テーブル。|  
|**anonymous_subid**|**uniqueidentifier**|匿名のエージェントの ID。|  
|**subscriber_name**|**sysname**|匿名のエージェントだけが使用するサブスクライバーの名前。|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|ディストリビューション エージェントまたはマージ エージェントが作成されたときの日時。|  
|**queue_id**|**sysname**|キュー更新サブスクリプションのキューを検索する識別子。 キューに置かれたサブスクリプションの場合、値は NULL です。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージ キュー ベースのパブリケーションでは、値は、サブスクリプションに使用するキューを一意に識別する GUID。 SQL Server ベースのキュー パブリケーションの場合、列が値を含む**SQL**します。<br /><br /> 注:使用して[!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージ キューは非推奨し、現在サポートされていません。|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|エージェントをリモートから起動できるかどうかを示します。<br /><br /> **0**エージェントをリモートから起動できないことを指定します。<br /><br /> **1**リモート、および示されているリモート コンピューター上にエージェントをアクティブにことを指定します、 *offload_server*プロパティ。|  
|**offload_server**|**sysname**|リモート エージェントのアクティブ化に使用するサーバーのネットワーク名。|  
|**dts_package_name**|**sysname**|DTS パッケージの名前です。 たとえば、という名前のパッケージ**DTSPub_Package**、指定`@dts_package_name = N'DTSPub_Package'`します。|  
|**dts_package_password**|**nvarchar(524)**|パッケージのパスワード。|  
|**dts_package_location**|**int**|パッケージの場所。 パッケージの場所を指定できます**ディストリビューター**または**サブスクライバー**します。|  
|**sid**|**varbinary(85)**|最初の実行時の、ディストリビューション エージェントまたはマージ エージェントのセキュリティ識別番号 (SID) です。|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|次のいずれかの値と、サブスクライバーに接続するときに、エージェントで使用されるセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 認証<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**subscriber_login**|**sysname**|サブスクライバーに接続するときに使用されるログイン。|  
|**@subscriber_password**|**nvarchar(524)**|サブスクライバーに接続するときに使用するパスワードの暗号化された値。|  
|**reset_partial_snapshot_progress**|**bit**|スナップショット全体のプロセスをもう一度開始するため、部分的にダウンロードしたスナップショットは破棄されます。|  
|**job_step_uid**|**uniqueidentifier**|SQL Server エージェント ジョブの一意の ID はステップが、エージェントを開始します。|  
|**subscriptionstreams**|**tinyint**|変更のバッチをサブスクライバーに並列的に適用するために、ディストリビューション エージェントごとに許可される接続の数を設定します。 サポートされている値の範囲は 1 ～ 64 です。|  
|**memory_optimized**|**bit**|1 は、メモリ最適化テーブルのサブスクライバーを使用できることを示します。|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar(524)**||  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
