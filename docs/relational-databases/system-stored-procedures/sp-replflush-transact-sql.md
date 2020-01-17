---
title: sp_replflush (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
author: stevestein
ms.author: sstein
ms.openlocfilehash: a6745589616dec5b129992cc555e1238cd62b545
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771592"
---
# <a name="spreplflush-transact-sql"></a>sp_replflush (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  アーティクルキャッシュをフラッシュします。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]  
>  このプロシージャを手動で実行する必要はありません。 **sp_replflush**はレプリケーションのトラブルシューティングを行う場合にのみ使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replflush**は、トランザクションレプリケーションで使用します。  
  
 効率を上げるため、アーティクル定義がキャッシュに格納されます。 **sp_replflush**は、アーティクル定義が変更または削除されるたびに、他のレプリケーションストアドプロシージャによって使用されます。  
  
 特定のデータベースに対するログリーダーアクセス権を持つことができるのは、1つのクライアント接続のみです。 クライアントがデータベースへのログリーダーアクセス権を持っている場合、 **sp_replflush**を実行すると、クライアントはそのアクセスを解放します。 その他のクライアントは、 **sp_replcmds**または**sp_replshowcmds**を使用して、トランザクションログをスキャンできます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replflush**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
