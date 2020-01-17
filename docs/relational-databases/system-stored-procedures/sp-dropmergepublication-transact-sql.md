---
title: sp_dropmergepublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: stevestein
ms.author: sstein
ms.openlocfilehash: b675b07466464f706b6503f3d017acd34822b2c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933901"
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ パブリケーションとその関連するスナップショット エージェントを削除します。 マージ パブリケーションを削除する前に、すべてのサブスクリプションを削除しておく必要があります。 パブリケーションのアーティクルが自動的に削除されます。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 削除するパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。 場合**すべて**、それらに関連付けられているスナップショット エージェント ジョブおよびすべての既存のマージ パブリケーションが削除されます。 特定の値を指定する場合*パブリケーション*、そのパブリケーションのみとその関連付けられているスナップショット エージェント ジョブが削除されます。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターでクリーンアップ タスクを実行せず、パブリケーションを削除するために使用します。 *ignore_distributor*は**ビット**、既定値は**0**します。 このパラメーターは、ディストリビューターを再インストールするときにも使用されます。  
  
`[ @reserved = ] reserved` 将来使用するために予約されています。 *予約済み*は**ビット**、既定値は**0**します。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropmergepublication**はマージ レプリケーションで使用します。  
  
 **sp_dropmergepublication**再帰的には、パブリケーションに関連付けられているすべてのアーティクルを削除し、後、パブリケーション自体が削除されます。 1 つまたは複数のサブスクリプションがある場合、パブリケーションを削除できません。 サブスクリプションを削除する方法については、次を参照してください。 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)と[Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)します。  
  
 実行**sp_dropmergepublication**パブリケーションを削除するオブジェクトは削除されませんパブリッシュされたパブリケーション データベースまたはサブスクリプション データベースから対応するオブジェクト。 ドロップを使用して\<オブジェクト > に必要な場合は、これらのオブジェクトを手動で削除します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_dropmergepublication**します。  
  
## <a name="see-also"></a>参照  
 [パブリケーションを削除します](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
