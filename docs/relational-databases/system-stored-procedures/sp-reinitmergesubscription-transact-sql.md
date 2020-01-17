---
title: sp_reinitmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27c10f9d5fa04ae449bdcca84891f0f28376eeb6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075699"
---
# <a name="sp_reinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ エージェントの次回実行時に再初期化するように、マージ サブスクリプションにマークを付けます。 このストアド プロシージャは、パブリッシャー側のパブリケーション データベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は**すべて**します。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前です。 *サブスクライバー*は**sysname**、既定値は**すべて**します。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクライバー データベースの名前です。 *\@subscriber_db*は **sysname**、既定値は**すべて**します。  
  
`[ @upload_first = ] 'upload_first'` サブスクリプションを再初期化する前に、サブスクライバーでの変更をアップロードするかどうか。 *\@upload_first*は **nvarchar (5)** 、既定値は FALSE。 場合**true**変更をアップロードして、サブスクリプションを再初期化します。 場合**false**変更はアップロードされません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_reinitmergesubscription**はマージ レプリケーションで使用します。  
  
 **sp_reinitmergesubscription**マージ サブスクリプションを再初期化し、パブリッシャーから呼び出すことができます。 スナップショット エージェントを再実行することをお勧めします。  
  
 パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_reinitmergesubscription**します。  
  
## <a name="see-also"></a>関連項目  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
