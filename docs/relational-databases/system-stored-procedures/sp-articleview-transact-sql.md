---
title: sp_articleview (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7cc40187ccafebee672214a0926a3ca0d0bc4176
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768994"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  テーブルが列または行でフィルター選択されている場合に、パブリッシュされたアーティクルを定義するビューを作成します。 このビューは、出力先のテーブル用にフィルター選択されたスキーマやデータのソースとして使用されます。 このストアドプロシージャで変更できるのは、サブスクライブされていないアーティクルだけです。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アーティクルを含むパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`アーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @view_name = ] 'view_name'`パブリッシュされたアーティクルを定義するビューの名前を指定します。 *view_name*は**nvarchar (386)** ,、既定値は NULL です。  
  
`[ @filter_clause = ] 'filter_clause'`は、水平フィルターを定義する restriction (WHERE) 句です。 Restriction 句を入力するときは、WHERE キーワードを省略します。 *filter_clause*は**ntext**,、既定値は NULL です。  
  
`[ @change_active = ] change_active`サブスクリプションを持つパブリケーションの列を変更できます。 *change_active*は、 **int**、既定値は**0**します。 **0**の場合、列は変更されません。 **1**の場合、サブスクリプションを持つアクティブなアーティクルに対して、ビューの作成または再作成を行うことができます。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古い形式としてマークされ、新しいスナップショットが生成されることを示します。  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_`このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**で、既定値は**0**です。  
  
 **0**に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によってサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーからパブリッシュする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーを使用しないでください。  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs`レプリケーションの同期に使用するストアドプロシージャが自動的に再作成されるかどうかを示します。 *refreshsyncの proc*は**ビット**,、既定値は1です。  
  
 **1**は、ストアドプロシージャが再作成されることを示します。  
  
 **0**の場合、ストアドプロシージャは再作成されません。  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_articleview**は、パブリッシュされたアーティクルを定義するビューを作成し、このビューの ID を[sysarticles &#40;transact-sql&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)テーブルの**sync_objid**列に挿入し、restriction 句のテキストをに挿入します。**filter_clause**列です。 すべての列がレプリケートされ、 **filter_clause**がない場合、 [sysarticles &#40;&#41; transact-sql](../../relational-databases/system-tables/sysarticles-transact-sql.md)テーブルの**sync_objid**はベーステーブルの ID に設定され、 **sp_articleview**の使用は必須ではありません。  
  
 行方向にフィルター選択されたテーブルをパブリッシュする (つまり、列をフィルター処理する) 場合は、 *sync_object*パラメーターを指定せずに**sp_addarticle**を実行し、レプリケートする各列に対して[sp_articlecolumn &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を1回実行します ([列フィルター]) をクリックし、 **sp_articleview**を実行して、パブリッシュされたアーティクルを定義するビューを作成します。  
  
 行方向にフィルター選択されたテーブルをパブリッシュする (つまり、行をフィルター処理する) には、 *filter*パラメーターを指定せずに[sp_addarticle &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 [ &#40;Sp_articlefilter&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)を実行し、 *filter_clause*を含むすべてのパラメーターを指定します。 次に、 **sp_articleview**を実行して、同じ*filter_clause*を含むすべてのパラメーターを指定します。  
  
 垂直方向および水平方向にフィルター選択されたテーブルをパブリッシュするには、 [sp_addarticle &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)パラメーターを使用せずに transact-sql を実行します。 レプリケートする各列に対して[sp_articlecolumn &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を1回実行し、 [ &#40;sp_articlefilter&#41; transact-sql](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)と**sp_articleview**を実行します。  
  
 パブリッシュされたアーティクルを定義するビューが既にアーティクルに存在する場合、 **sp_articleview**は既存のビューを削除し、新しいビューを自動的に作成します。 ビューが手動で作成された場合[( &#40;sysarticles transact-sql&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)は**5**)、既存のビューは削除されません。  
  
 カスタムフィルターストアドプロシージャと、パブリッシュされたアーティクルを手動で定義するビューを作成する場合は、 **sp_articleview**を実行しないでください。 代わりに、これらを*フィルター*と*sync_object*パラメーターとして[sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)に、適切な*型*の値として指定します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_articleview**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [静的行フィルターの定義と変更](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
