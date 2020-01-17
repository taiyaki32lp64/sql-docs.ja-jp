---
title: sp_deletepeerrequesthistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1af3aad1f66f3de7dd2fce44990718980018d3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111944"
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  要求の履歴を含むパブリケーション状態要求に関連する履歴を削除します ([MSpeer_request &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) と応答履歴 ([MSpeer_response &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md))。このストアド プロシージャは、ピア ツー ピア レプリケーション トポロジに参加しているパブリッシャーでパブリケーション データベースで実行されます。 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 状態要求が行われたパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @request_id = ] request_id` この要求に応答するすべてが削除されるように、個々 の状態要求を指定します。 *request_id*は**int**既定値は NULL です。  
  
`[ @cutoff_date = ] cutoff_date` 以前のすべての応答レコードが削除される前に、終了日を指定します。 *cutoff_date*は**datetime**既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_deletepeerrequesthistory**ピア ツー ピア トランザクション レプリケーション トポロジで使用されます。 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 実行時に**sp_deletepeerrequesthistory**, か、 *request_id*または*cutoff_date*指定する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_deletepeerrequesthistory**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_helppeerrequests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
