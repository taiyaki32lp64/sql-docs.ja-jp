---
title: sp_helppeerrequests (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b9e2a370c9acc9c22dac7e5e60ceb10e08e46ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137630"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ピア ツー ピア レプリケーション トポロジでは、これらの要求を実行することによって開始された場所で参加者が受信したすべての状態要求に関する情報を返します[sp_requestpeerresponse &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)いつでもトポロジでパブリッシュされたデータベース。 このストアド プロシージャは、ピア ツー ピア レプリケーション トポロジに参加しているパブリッシャーでパブリケーション データベースで実行されます。 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 状態要求を送信したピア ツー ピア トポロジ内のパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @description = ] 'description'` 呼び出すときに提供される情報を定義したユーザーに基づいて、返された応答をフィルター選択できる、個々 の状態要求を識別するために使用できる値[sp_requestpeerresponse &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)します。 *説明*は**nvarchar (4000)** 、既定値は **%** します。 既定では、パブリケーションのすべての状態要求が返されます。 指定された値に一致する説明で状態要求のみを返すためにこのパラメーターを使用します*説明*を使用して文字の文字列が一致する、[など&#40;TRANSACT-SQL&#41; ](../../t-sql/language-elements/like-transact-sql.md)。句。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|要求を識別します。|  
|**publication**|**sysname**|状態要求の送信をパブリケーションの名前です。|  
|**sent_date**|**datetime**|日付と状態要求が送信された時刻。|  
|**description**|**nvarchar (4000)**|ユーザーは、個々 の状態要求を識別するために使用できる情報を定義します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helppeerrequests**はピア ツー ピア トランザクション レプリケーションで使用します。  
  
 **sp_helppeerrequests**ピア ツー ピア トポロジでパブリッシュされたデータベースを復元するときに使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_helppeerrequests**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
