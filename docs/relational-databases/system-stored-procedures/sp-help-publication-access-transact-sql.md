---
title: sp_help_publication_access (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7c562c039b65f99f1d3d9915f0dd00b93dc95860
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770991"
---
# <a name="sp_help_publication_access-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリケーションに対して許可されているすべてのログインの一覧を返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アクセスするパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @return_granted = ] 'return_granted'`ログイン ID を示します。 *return_granted*は**ビット**,、既定値は1です。 **0**を指定し[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、認証を使用する場合、パブリッシャーで表示され、ディストリビューターでは使用できないログインが返されます。 **0**を指定し、Windows 認証を使用する場合、パブリッシャーまたはディストリビューターでのアクセスが明示的に拒否されていないログインが返されます。  
  
`[ @login = ] 'login'`標準的なセキュリティログイン ID を示します。 *login*は**sysname**,、既定値 **%** はです。  
  
`[ @initial_list = ] initial_list`パブリケーションアクセス権を持つすべてのメンバーを返すか、または新しいメンバーがリストに追加される前にアクセスしたメンバーのみを返すかを指定します。 *initial_list*はビット,、既定値は**0**です。  
  
 **1**は、 **sysadmin**固定サーバーロールのすべてのメンバーについて、パブリケーションの作成時に存在していた有効なログインと、現在のログインに関する情報を返します。  
  
 **0**を指定すると、 **sysadmin**固定サーバーロールのすべてのメンバーについての情報が返されます。これは、パブリケーションの作成時に存在していたディストリビューターでの有効なログインと、sysadmin に属さないパブリケーションアクセスリスト内のすべてのユーザーです。固定サーバーロール。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar (256)**|実際のログイン名。|  
|**Isntname**|**int**|**0** = ログインは Windows ユーザーではありません。<br /><br /> **1** = ログインは Windows ユーザーです。|  
|**Isntgroup**|**int**|**0** = ログインは Windows グループではありません。<br /><br /> **1** = ログインは Windows グループです。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_help_publication_access**は、すべての種類のレプリケーションで使用されます。  
  
 結果セットの**Isntname**と**Isntgroup**の両方が**0**の場合は、ログインが[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインであると見なされます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_help_publication_access**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
