---
title: sp_articlecolumn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
ms.openlocfilehash: acbbd043080b107a5d545408fabe271d62015e54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105085"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パブリッシュされたテーブルでのデータを垂直方向にフィルター処理するアーティクルに含まれる列を指定するために使用します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` この記事を含むパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'` アーティクルの名前です。 *記事*は**sysname**、既定値はありません。  
  
`[ @column = ] 'column'` 追加または削除する列の名前です。 *列*は**sysname**、既定値は NULL です。 NULL の場合は、すべての列がパブリッシュされます。  
  
`[ @operation = ] 'operation'` 追加またはアーティクルに列を削除するかどうかを指定します。 *操作*は**nvarchar (5)** 、既定値は add です。 **追加**レプリケーションする列をマークします。 **drop**列のマークを解除します。  
  
`[ @refresh_synctran_procs = ] refresh_synctran_procs` レプリケートされた列の数と一致する即時更新サブスクリプションをサポートするストアド プロシージャを再生成するかどうかを指定します。 *refresh_synctran_procs*は**ビット**、既定値は**1**します。 場合**1**、ストアド プロシージャが再生成します。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターに接続しなくてもこのストアド プロシージャが実行されるかどうかを示します。 *ignore_distributor*は**ビット**、既定値は**0**します。 場合**0**パブリッシング用のデータベースを有効にする必要があります、アーティクルによってレプリケートされた新しい列を反映するようにアーティクル キャッシュを更新する必要があります。 場合**1**アーティクルの列はパブリッシュされていないデータベースの回復の状況でのみ使用する必要がありますをアーティクルに対して削除を許可します。  
  
`[ @change_active = ] change_active` サブスクリプションを持つパブリケーション内の列を変更できます。 *@change_active*は、 **int** 、既定値は**0**します。 場合**0**列は変更されません。 場合**1**列を追加またはサブスクリプションを持つアクティブなアーティクルから削除されることができます。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアド プロシージャが実行する操作が既存のスナップショットが無効になることを確認します。 *更によって*は、**ビット**、既定値は**0**します。  
  
 **0**スナップショットが無効であることをアーティクルへの変更が発生しないことを指定します。 ストアド プロシージャは、変更は、新しいスナップショットを必要になることを検出する場合は、エラーが発生し、変更は行われません。  
  
 **1**アーティクルへの変更はスナップショットが無効であることがあり、新しいスナップショットを必要とする既存のサブスクリプションがある場合は、アクセス許可を付与 obsolete としてマーク済みである既存のスナップショットを新しいスナップショットを生成を指定します。  
  
 [ **@force_reinit_subscription =** ]*更によって*  
 このストアド プロシージャが実行されるアクションでは、既存のサブスクリプションの再初期化される場合がありますかを確認します。 *更によって*は、**ビット**、既定値は**0**します。  
  
 **0**アーティクルへの変更では、サブスクリプションを再初期化するのには発生しないことを指定します。 ストアド プロシージャが、変更がサブスクリプションの再初期化する必要になることを検出した場合は、エラーが発生し、変更は行われません。 **1**アーティクルへの変更が発生する既存のサブスクリプションを再初期化することを指定します。 サブスクリプションの再初期化を許可します。  
  
`[ @publisher = ] 'publisher'` 以外を指定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャー*では使用できません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
`[ @internal = ] 'internal'` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_articlecolumn**スナップショット レプリケーションおよびトランザクション レプリケーションで使用されます。  
  
 使用して、サブスクライブされていないアーティクルのみをフィルター処理すること**sp_articlecolumn**します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_articlecolumn**します。  
  
## <a name="see-also"></a>関連項目  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Define and Modify a Column Filter](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [パブリッシュされたデータのフィルター処理](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
