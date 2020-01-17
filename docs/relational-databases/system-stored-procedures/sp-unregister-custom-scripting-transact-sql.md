---
title: sp_unregister_custom_scripting (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe6bfe4c93ccabfaaec27739f7a1fd0e09348526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017903"
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このストアド プロシージャは、ユーザー定義カスタム ストアド プロシージャを削除または[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト ファイルを実行して登録された[sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @type = ] 'type'` カスタム ストアド プロシージャまたはスクリプトの種類を削除しています。 *型*は**varchar (16)** , で、既定値はありませんは、次の値のいずれかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|**insert**|登録済みのカスタム ストアド プロシージャまたはスクリプトは、INSERT ステートメントがレプリケートされるときに実行されます。|  
|**update**|登録済みのカスタム ストアド プロシージャまたはスクリプトは、UPDATE ステートメントがレプリケートされるときに実行されます。|  
|**delete**|登録済みのカスタム ストアド プロシージャまたはスクリプトは、DELETE ステートメントがレプリケートされるときに実行されます。|  
|**custom_script**|登録済みのカスタム ストアド プロシージャまたはスクリプトは、データ定義言語 (DDL) トリガーの最後に実行されます。|  
  
`[ @publication = ] 'publication'` カスタム ストアド プロシージャまたはスクリプトをパブリケーションの名前を削除しています。 *パブリケーション*は**sysname**、既定値は NULL です。  
  
`[ @article = ] 'article'` カスタム ストアド プロシージャまたはスクリプトをアーティクルの名前を削除しています。 *記事*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_unregister_custom_scripting**スナップショットおよびトランザクション レプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner**固定データベース ロール、または**db_ddladmin**固定データベース ロールが実行できる**sp _unregister_custom_scripting**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_register_custom_scripting &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
