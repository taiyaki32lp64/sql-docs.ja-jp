---
title: sp_generatefilters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_generatefilters
- sp_generatefilters_TSQL
helpviewer_keywords:
- sp_generatefilters
ms.assetid: 0aeb5b7a-89d1-4bd5-a371-c27fa924360a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 410bdf157cc4194191649e6a6e6ab6d92ea033b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124147"
---
# <a name="spgeneratefilters-transact-sql"></a>sp_generatefilters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したテーブルがレプリケートされるときに、外部キー テーブルにフィルターを作成します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_generatefilters [ @publication =] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` フィルター選択されるパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_generatefilters**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_generatefilters**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
