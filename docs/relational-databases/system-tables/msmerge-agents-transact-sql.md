---
title: MSmerge_agents (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
author: stevestein
ms.author: sstein
ms.openlocfilehash: 980ecd00a07e1119a64552a3f4c903434fd09029
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106441"
---
# <a name="msmerge_agents-transact-sql"></a>MSmerge_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_agents**テーブルは、サブスクライバーで実行されるマージ エージェントはごとに 1 行を格納します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|マージ エージェントの ID。|  
|**name**|**nvarchar(100)**|マージ エージェントの名前。|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**subscriber_id**|**smallint**|サブスクライバーの ID。|  
|**subscriber_db**|**sysname**|サブスクリプション データベースの名前。|  
|**local_job**|**bit**|ローカル ディストリビューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブがあるかどうかを示します。|  
|**job_id**|**binary(16)**|ジョブの識別番号。|  
|**profile_id**|**int**|ある構成 ID、 **MSagent_profiles**テーブル。|  
|**anonymous_subid**|**uniqueidentifier**|匿名のエージェントの ID。|  
|**subscriber_name**|**sysname**|サブスクライバーの名前。|  
|**creation_date**|**datetime**|日付と時刻、ディストリビューション エージェントまたはマージ エージェントが作成されたことです。|  
|**offload_enabled**|**bit**|エージェントをリモートから起動できることを指定します。<br /><br /> **0**エージェントをリモートでアクティブにできませんを指定します。<br /><br /> **1**リモート、および offload_server プロパティで指定されたリモート コンピューター上にエージェントをアクティブ化を指定します。|  
|**offload_server**|**sysname**|リモート エージェントのアクティブ化に使用するサーバーのネットワーク名を指定します。|  
|**sid**|**varbinary(85)**|最初の実行時の、ディストリビューション エージェントまたはマージ エージェントのセキュリティ識別番号 (SID) です。|  
|**subscriber_security_mode**|**smallint**|次のいずれかの値と、サブスクライバーに接続するときに、エージェントで使用されるセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**subscriber_login**|**sysname**|サブスクライバーに接続するときに使用されるログイン。|  
|**subscriber_password**|**nvarchar(524)**|サブスクライバーに接続するときに使用されるパスワードの暗号化された値。|  
|**publisher_security_mode**|**smallint**|次のいずれかの値と、パブリッシャーに接続するときに、エージェントで使用されるセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**publisher_login**|**sysname**|パブリッシャーに接続するときに使用されるログイン。|  
|**publisher_password**|**nvarchar(524)**|パブリッシャーに接続するときに使用されるパスワードの暗号化された値。|  
|**job_step_uid**|**uniqueidentifier**|エージェントが起動される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップの一意な ID|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
