---
title: sp_register_custom_scripting (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c10451148c6f9b2fda231691b770bca3928517f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075755"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケーションは、ユーザー定義カスタム ストアド プロシージャに置き換える 1 つ以上のトランザクション レプリケーションで使用される既定のプロシージャを使用できます。 レプリケートされたテーブルにスキーマ変更が行われると、これらのストアド プロシージャは再作成されます。 **sp_register_custom_scripting**ストアド プロシージャを登録または[!INCLUDE[tsql](../../includes/tsql-md.md)]新しいユーザー定義カスタム ストアド プロシージャに対する定義のスクリプトにスキーマ変更が発生したときに実行されるスクリプト ファイル。 この新しいユーザー定義カスタム ストアド プロシージャには、テーブルに対する新しいスキーマを反映する必要があります。 **sp_register_custom_scripting**がパブリッシャー、パブリケーション データベースに対して実行される登録されているスクリプト ファイルまたはストアド プロシージャがスキーマ変更が発生したときに、サブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @type = ] 'type'` 登録されているカスタム ストアド プロシージャまたはスクリプトの種類。 *型*は**varchar (16)** , で、既定値はありませんは、次の値のいずれかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|**insert**|INSERT ステートメントがレプリケートされるときに、登録したカスタム ストアド プロシージャが実行されます。|  
|**update**|登録したカスタム ストアド プロシージャを、UPDATE ステートメントがレプリケートされるときに実行。|  
|**delete**|登録したカスタム ストアド プロシージャを、DELETE ステートメントがレプリケートされるときに実行。|  
|**custom_script**|スクリプトは、データ定義言語 (DDL) トリガーの最後に実行されます。|  
  
`[ @value = ] 'value'` ストアド プロシージャまたは名前と完全修飾パスの名前、[!INCLUDE[tsql](../../includes/tsql-md.md)]登録されているスクリプト ファイル。 *値*は**nvarchar (1024)** 、既定値はありません。  
  
> [!NOTE]  
>  NULL を指定する*値*パラメーターには、以前に登録されたスクリプトを実行すると同じであるが登録解除[sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)します。  
  
 ときに、値の*型*は**custom_script**の完全なパスと名前を[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト ファイルが必要です。 それ以外の場合、*値*登録済みのストアド プロシージャの名前を指定する必要があります。  
  
`[ @publication = ] 'publication'` 登録は、カスタム ストアド プロシージャまたはスクリプトをパブリケーションの名前を指定します。 *パブリケーション*は**sysname**、既定値は**NULL**します。  
  
`[ @article = ] 'article'` カスタム ストアド プロシージャまたはスクリプトが登録するアーティクルの名前。 *記事*は**sysname**、既定値は**NULL**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_register_custom_scripting**スナップショットおよびトランザクション レプリケーションで使用されます。  
  
 このストアド プロシージャは、スキーマのレプリケートされたテーブルに変更を行う前に実行する必要があります。 このストアド プロシージャの使用に関する詳細については、次を参照してください。[再生成カスタム トランザクション プロシージャのスキーマ変更の反映を](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner**固定データベース ロール、または**db_ddladmin**固定データベース ロールが実行できる**sp _register_custom_scripting**します。  
  
## <a name="see-also"></a>参照  
 [sp_unregister_custom_scripting &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
