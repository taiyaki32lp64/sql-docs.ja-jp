---
title: sp_articlefilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: stevestein
ms.author: sstein
ms.openlocfilehash: d90cd0ba957da820ce5a937ae687e39ca0302025
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769057"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  テーブルアーティクルに基づいてパブリッシュされたデータをフィルター処理します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アーティクルを含むパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`アーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @filter_name = ] 'filter_name'`*Filter_name*から作成されるフィルターストアドプロシージャの名前を指定します。 *filter_name*は**nvarchar (386)** ,、既定値は NULL です。 アーティクルフィルターには一意の名前を指定する必要があります。  
  
`[ @filter_clause = ] 'filter_clause'`は、水平フィルターを定義する restriction (WHERE) 句です。 制限句を入力する場合は、WHERE キーワードを省略します。 *filter_clause*は**ntext**,、既定値は NULL です。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古い形式としてマークされ、新しいスナップショットが生成されることを示します。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、アーティクルへの変更によってサブスクリプションが再初期化される必要がなくなります。 変更によってサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーでは使用できません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_articlefilter**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 既存のサブスクリプションを持つアーティクルに対して**sp_articlefilter**を実行するには、それらのサブスクリプションを再初期化する必要があります。  
  
 **sp_articlefilter**は、フィルターを作成し、 [sysarticles &#40;&#41; transact-sql](../../relational-databases/system-tables/sysarticles-transact-sql.md)テーブルの**filter**列にフィルターストアドプロシージャの ID を挿入して、restriction 句のテキストをフィルターに挿入します。 **句の列 (_s)**  
  
 水平フィルターを使用してアーティクルを作成するには、 *filter*パラメーターを指定せずに[sp_addarticle &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **Sp_articlefilter**を実行し、 *filter_clause*を含むすべてのパラメーターを指定して、 [sp_articleview &#40;&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行します。同じ*filter_clause*を含むすべてのパラメーターを指定します。 フィルターが既に存在し、 **sysarticles**の**種類**が**1** (ログベースのアーティクル) の場合は、前のフィルターが削除され、新しいフィルターが作成されます。  
  
 *Filter_name*と*filter_clause*が指定されていない場合は、前のフィルターが削除され、フィルター ID は**0**に設定されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_articlefilter**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [静的行フィルターの定義と変更](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
