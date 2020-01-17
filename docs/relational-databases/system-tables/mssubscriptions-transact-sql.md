---
title: MSsubscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca4364709462eee9df62baa8193dec9f8ea36241
ms.sourcegitcommit: 722f2ec5a1af334f5bcab8341bc744d16a115273
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74866044"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Mssubscriptions**テーブルには、ローカルディストリビューターによってサービスが提供されるサブスクリプション内のパブリッシュされたアーティクルごとに1行のレコードが含まれます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**通り**|パブリッシャーデータベースの ID。|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**publication_id**|**通り**|パブリケーションの ID です。|  
|**article_id**|**通り**|アーティクルの ID です。|  
|**subscriber_id**|**smallint**|サブスクライバーの ID です。|  
|**subscriber_db**|**sysname**|サブスクリプションデータベースの名前。|  
|**subscription_type**|**通り**|サブスクリプションの種類。<br /><br /> **0** = プッシュ。<br /><br /> **1** = プル。<br /><br /> **2** = 匿名。|  
|**sync_type**|**tinyint**|同期の種類。<br /><br /> **1** = 自動。<br /><br /> **2** = 同期なし。|  
|**オンライン**|**tinyint**|サブスクリプションの状態。<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = サブスクライブ済み。<br /><br /> **2** = アクティブ。|  
|**subscription_seqno**|**varbinary(16)**|スナップショットトランザクションのシーケンス番号です。|  
|**snapshot_seqno_flag**|**bit**|スナップショットトランザクションのシーケンス番号のソースを示します。値が**1**の場合、 **subscription_seqno**がスナップショットのシーケンス番号であることを意味します。|  
|**independent_agent**|**bit**|このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうかを示します。|  
|**subscription_time**|**/**|内部使用のみです。|  
|**loopback_detection**|**bit**|双方向トランザクションレプリケーショントポロジの一部であるサブスクリプションに適用されます。 ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **1** = を返しません。<br /><br /> **0** = 返送します。<br /><br />|  
|**agent_id**|**通り**|エージェントの ID。|  
|**update_mode**|**tinyint**|更新の種類。|  
|**publisher_seqno**|**varbinary(16)**|このサブスクリプションに対するパブリッシャー側のトランザクションのシーケンス番号。|  
|**ss_cplt_seqno**|**varbinary(16)**|同時実行スナップショット処理の完了を示すために使用するシーケンス番号。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
