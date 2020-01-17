---
title: IHsubscriptions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: stevestein
ms.author: sstein
ms.openlocfilehash: b677e0f6c9be058650a46aee3465811b8f3eecc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990147"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHsubscriptions**システム テーブルが含まれていますサブスクリプションごとに 1 つの行にはパブリケーションから、SQL Server 以外のパブリッシャー、現在のディストリビューターを使用します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|パブリッシュされたアーティクルを一意に識別します。|  
|**srvid**|**smallint**|サブスクライバーのサーバー ID。|  
|**dest_db**|**sysname**|転送先データベースの名前|  
|**login_name**|**sysname**|サブスクリプションを追加するときに使用するログイン名です。|  
|**distribution_jobid**|**binary(16)**|ディストリビューション エージェントのジョブ ID です。|  
|**timestamp**|**timestamp**|サブスクリプションを作成した日付と時刻。|  
|**queued_reinit**|**bit**|アーティクルが初期化または再初期化の対象としてマークされているかどうかを指定します。 値**1**サブスクライブされるアーティクルが初期化または再初期化のマークされているを指定します。|  
|**status**|**tinyint**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブです。<br /><br /> **1** = サブスクライブします。<br /><br /> **2** = アクティブ。|  
|**sync_type**|**tinyint**|初期同期の種類。<br /><br /> **1** = 自動。<br /><br /> **2** = none。|  
|**subscription_type**|**int**|サブスクリプションの種類です。<br /><br /> **0** = プッシュ、ディストリビューション エージェントがサブスクライバーで実行されます。<br /><br /> **1** = プル、ディストリビューション エージェントがディストリビューターで実行されます。|  
|**update_mode**|**tinyint**|更新モード。<br /><br /> **0** = 読み取り専用です。<br /><br /> **1** = 即時更新します。|  
|**loopback_detection**|**bit**|双方向トランザクション レプリケーション トポロジの一部であるサブスクリプションに適用されます。 ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **0** = 戻す。<br /><br /> **1** = は送信しません。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
