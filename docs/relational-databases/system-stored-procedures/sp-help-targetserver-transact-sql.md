---
title: sp_help_targetserver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1eb9a4d1a19f54f9e57e988b350594ce6031b243
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085083"
---
# <a name="sphelptargetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべての対象サーバーを一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @server_name = ] 'server_name'` 情報を返す対象のサーバーの名前。 *server_name*は**nvarchar (30)** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 場合*server_name*が指定されていない**sp_help_targetserver**この結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|サーバーの識別番号。|  
|**server_name**|**nvarchar(30)**|サーバー名。|  
|**location**|**nvarchar(200)**|指定したサーバーの場所。|  
|**time_zone_adjustment**|**int**|グリニッジ標準時 (GMT) との時差 (時間単位)。|  
|**enlist_date**|**datetime**|指定したサーバーの参加日。|  
|**last_poll_date**|**datetime**|サーバーが最後にジョブをポーリングした日付。|  
|**status**|**int**|指定したサーバーの状態。|  
|**unread_instructions**|**int**|サーバーに未読の指示があるかどうか。 この列は、すべての行がダウンロードされている場合**0**します。|  
|**local_time**|**datetime**|ターゲット サーバーのローカル日時。これは、マスター サーバーが最後にポーリングを実行した時点のターゲット サーバーのローカル時間です。|  
|**enlisted_by_nt_user**|**nvarchar(100)**|ターゲット サーバーに参加した Microsoft Windows のユーザー。|  
|**poll_interval**|**int**|ジョブをダウンロードし、ジョブ ステータスをアップロードするために、ターゲット サーバーがマスター SQLServerAgent サービスをポーリングする頻度 (秒単位)。|  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. すべての登録された対象サーバーの情報を一覧表示する  
 次の例では、すべての登録されたターゲット サーバーの情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. 特定のターゲット サーバーの情報を一覧表示する  
 次の例は、対象サーバーの情報を一覧表示`SEATTLE2`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
