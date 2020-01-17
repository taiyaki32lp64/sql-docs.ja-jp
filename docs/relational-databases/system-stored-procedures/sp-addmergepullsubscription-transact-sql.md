---
title: sp_addmergepullsubscription (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b0a20e2bc7a167698353db31e7c0411fb1a6961
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769140"
---

# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  マージパブリケーションにプルサブスクリプションを追加します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *Publisher*は**sysname**で、既定値はローカルサーバー名です。 パブリッシャーは有効なサーバーである必要があります。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db*は**sysname**,、既定値は NULL です。  
  
`[ @subscriber_type = ] 'subscriber_type' サブスクライバーの種類を示します。 *subscriber_type* は **nvarchar (15)**、**global**、**local** または **anonymous** にすることができます。 以降[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のバージョンでは、ローカルサブスクリプションはクライアントサブスクリプションと呼ばれ、グローバルサブスクリプションはサーバーサブスクリプションと呼ばれます。  
  
`[ @subscription_priority = ] subscription_priority`サブスクリプションの優先度です。 *subscription_priority*は**real**,、既定値は NULL です。 ローカルサブスクリプションと匿名サブスクリプションの場合、優先度は**0.0**です。 既定の競合回避モジュールでは、競合が検出された場合に優先される優先順位を使用します。 グローバルサブスクライバーの場合、サブスクリプションの優先度は、パブリッシャーの優先度である100未満である必要があります。  
  
`[ @sync_type = ] 'sync_type'`サブスクリプションの同期の種類を示します。 *sync_type* は**nvarchar (15)**、既定値は **automatic** です。 **Automatic** または **none** を指定できます。 **automatic** の場合、パブリッシュされたテーブルのスキーマと初期データが最初にサブスクライバーに転送されます。 存在しない場合は、パブリッシュされたテーブルのスキーマと初期データがサブスクライバーに既に存在していると見なされます。 システム テーブルとデータは常に転送されます。  
  
> [!NOTE]  
>  値**none**を指定することはお勧めしません。  
  
`[ @description = ] 'description'`このプルサブスクリプションの簡単な説明です。 *説明*は**nvarchar (255)** ,、既定値は NULL です。 この値は、レプリケーションモニターの **[フレンドリ名]** 列に表示されます。この列を使用して、監視されるパブリケーションのサブスクリプションを並べ替えることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addmergepullsubscription**は、マージレプリケーションに使用します。  
  
 エージェントを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用してサブスクリプションを同期する場合は、サブスクライバーで[sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)ストアドプロシージャを実行して、パブリケーションと同期するエージェントとジョブを作成する必要があります。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergepullsubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
