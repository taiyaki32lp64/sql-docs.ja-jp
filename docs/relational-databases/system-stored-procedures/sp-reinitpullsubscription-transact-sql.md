---
title: sp_reinitpullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitpullsubscription_TSQL
- sp_reinitpullsubscription
helpviewer_keywords:
- sp_reinitpullsubscription
ms.assetid: 7d9abe49-ce92-47f3-82c9-aea749518c91
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6f9021ec9b71694fc6567db5edf79965e09fd3c0
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304917"
---
# <a name="sp_reinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  次回ディストリビューションエージェントが実行されたときに再初期化するために、トランザクションプルサブスクリプションまたは匿名サブスクリプションにマークを付けます。 このストアド プロシージャは、サブスクライバー側でプル サブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname** 、既定値はありません。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication*は**sysname**で、既定値は all です。これはすべてのサブスクリプションに再初期化のマークを付けます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitpullsubscription**は、トランザクションレプリケーションで使用します。  
  
 **sp_reinitpullsubscription**は、ピアツーピアトランザクションレプリケーションではサポートされていません。  
  
 ディストリビューションエージェントの次回の実行時に、サブスクリプションを再初期化するために、サブスクライバーから**sp_reinitpullsubscription**を呼び出すことができます。  
  
 **\@immediate_sync**の値が**false**で作成されたパブリケーションに対するサブスクリプションは、サブスクライバーから再初期化することはできません。  
  
 プルサブスクリプションを再初期化するには、サブスクライバーで**sp_reinitpullsubscription**を実行するか、パブリッシャーで**sp_reinitsubscription**します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_reinitpullsubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
