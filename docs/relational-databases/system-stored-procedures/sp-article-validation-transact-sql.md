---
title: sp_article_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6f5ee076163ff3cf0f69daab7ceff115bf5876a6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769020"
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたアーティクルに対する検証の要求を開始します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行され、サブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アーティクルが存在するパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`検証するアーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @rowcount_only = ] type_of_check_requested`テーブルの行数のみを返すかどうかを指定します。 *type_of_check_requested*は**smallint**,、既定値は**1**です。  
  
 **0**の場合は、rowcount と互換性[!INCLUDE[msCoName](../../includes/msconame-md.md)]の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ある7.0 のチェックサムを実行します。  
  
 **1**の場合は、行数チェックのみを実行します。  
  
 **2**の場合は、行数とバイナリチェックサムを実行します。  
  
`[ @full_or_fast = ] full_or_fast`行数を計算するために使用されるメソッドです。 *full_or_fast*は**tinyint**,、これらの値のいずれかを指定できます。  
  
|**[値]**|**[説明]**|  
|---------------|---------------------|  
|**0**|COUNT(*) を使用してフル カウントを実行します。|  
|**1**|Sysindexes から高速カウントを実行し**ます**。 **Sysindexes**内の行のカウントは、実際のテーブルの行をカウントするよりも高速です。 ただし、 **sysindexes**は遅延して更新され、行数が正確ではない可能性があります。|  
|**2** (既定値)|最初に fast メソッドを試行して、条件付き高速カウントを実行します。 Fast メソッドが相違点を示している場合、は完全なメソッドに戻ります。 場合*expected_rowcount*ストアド プロシージャの中を NULL 値を取得する、フル カウント(\*) が常に使用します。|  
  
`[ @shutdown_agent = ] shutdown_agent`検証の完了後すぐにディストリビューションエージェントをシャットダウンするかどうかを指定します。 *shutdown_agent*は**ビット**,、既定値は**0**です。 **0**の場合、ディストリビューションエージェントはシャットダウンされません。 **1**の場合、アーティクルの検証後にディストリビューションエージェントがシャットダウンされます。  
  
`[ @subscription_level = ] subscription_level`一連のサブスクライバーによって検証が選択されるかどうかを指定します。 *subscription_level*は**ビット**,、既定値は**0**です。 **0**の場合、すべてのサブスクライバーに検証が適用されます。 **1**の場合、現在開いているトランザクションで**sp_marksubscriptionvalidation**を呼び出すことによって指定されたサブスクライバーのサブセットにのみ検証が適用されます。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーの検証を要求するときは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_article_validation**は、トランザクションレプリケーションで使用します。  
  
 **sp_article_validation**により、指定されたアーティクルで検証情報が収集され、トランザクションログに検証要求が送信されます。 ディストリビューション エージェントは、この要求を受け取ると、要求に含まれている検証の情報をサブスクライバー テーブルと比較します。 検証の結果は、レプリケーション モニターおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告に表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_article_validation**を実行できるのは、検証されるアーティクルのソーステーブルに対する SELECT ALL 権限を持つユーザーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
