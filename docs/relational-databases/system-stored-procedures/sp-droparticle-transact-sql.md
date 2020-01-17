---
title: sp_droparticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droparticle_TSQL
- sp_droparticle
helpviewer_keywords:
- sp_droparticle
ms.assetid: 09fec594-53f4-48a5-8edb-c50731c7adb2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 882c57c552d9666ec3ef308f63a6c5058c21e8e2
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768931"
---
# <a name="spdroparticle-transact-sql"></a>sp_droparticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  スナップショットパブリケーションまたはトランザクションパブリケーションからアーティクルを削除します。 1 つでもサブスクリプションがあると、そのアーティクルは削除できません。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_droparticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @from_drop_publication = ] from_drop_publication ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`削除するアーティクルを含むパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`削除するアーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古い形式としてマークされ、新しいスナップショットが生成されることを示します。  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでアーティクルの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロパティを変更する場合は、パブリッシャーを使用しないでください。  
  
`[ @from_drop_publication = ] from_drop_publication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_droparticle**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 行方向にフィルター選択されたアーティクルの場合、 **sp_droparticle**は[ &#40;sysarticles transact-sql&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)テーブルのアーティクルの**type**列を調べて、ビューまたはフィルターも削除する必要があるかどうかを判断します。 ビューまたはフィルターが自動生成された場合は、アーティクルによって削除されます。 手動で作成された場合は、削除されません。  
  
 **Sp_droparticle**を実行してパブリケーションからアーティクルを削除しても、パブリケーションデータベースからオブジェクトが削除されたり、サブスクリプションデータベースから対応するオブジェクトが削除されることはありません。 これらのオブジェクトは、必要に応じて `DROP <object>` を使用して手動で削除します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_droparticle**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [アーティクルの削除](../../relational-databases/replication/publish/delete-an-article.md)   
 [既存のパブリケーションでのアーティクルの追加と削除](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
