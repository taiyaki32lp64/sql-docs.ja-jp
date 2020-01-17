---
title: sp_marksubscriptionvalidation (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: stevestein
ms.author: sstein
ms.openlocfilehash: bb8c38d24fbf6c96c61a7b2e83874d15218797c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092673"
---
# <a name="spmarksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定のサブスクライバーのサブスクリプション レベル検証トランザクションであることを現在開いているトランザクションをマークします。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前です。 *サブスクライバー*が sysname で、既定値はありません。  
  
`[ @destination_db = ] 'destination_db'` 転送先データベースの名前です。 *destination_db*は**sysname**、既定値はありません。  
  
`[ @publisher = ] 'publisher'` 以外を指定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャー*が属しているパブリケーションの使わないで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_marksubscriptionvalidation**はトランザクション レプリケーションで使用します。  
  
 **sp_marksubscriptionvalidation**はサポートされません以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバー。  
  
 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]実行することはできません、発行元**sp_marksubscriptionvalidation**から明示的なトランザクション。 これは、明示的なトランザクションはパブリッシャーにアクセスするために使用するリンク サーバー接続経由でサポートされていません。  
  
 **sp_marksubscriptionvalidation**と同時に使用する必要があります[sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)の値を指定する**1**の*subscription_level*、およびその他の呼び出しで使用できる**sp_marksubscriptionvalidation**他のサブスクライバーの現在開いているトランザクションをマークします。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_marksubscriptionvalidation**します。  
  
## <a name="example"></a>例  
 次のクエリは、サブスクリプションレベルの検証コマンドを通知するために、パブリッシング データベースに適用できます。 これらのコマンドは、指定されたサブスクライバーのディストリビューション エージェントによって取得されます。 最初のトランザクションがアーティクルを検証することに注意してください '**art1**'、2 番目に、トランザクションを検証します**art2**'。 またを注意への呼び出し**sp_marksubscriptionvalidation**と[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)トランザクションにカプセル化されました。 1 つだけの呼び出しをお勧め[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) (トランザクションあたり)。 これは、ため[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 、トランザクションの実行中のソース テーブルで、共有テーブル ロックを保持します。 コンカレンシーを最大限に高めるために、トランザクションは短くしてください。  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
