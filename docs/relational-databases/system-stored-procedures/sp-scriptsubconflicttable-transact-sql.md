---
title: sp_scriptsubconflicttable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: stevestein
ms.author: sstein
ms.openlocfilehash: 806209b4f881576c680c14b0bc17ec4fd04a086c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126368"
---
# <a name="spscriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  キューに登録されたサブスクリプション アーティクルのサブスクライバー上に競合テーブルを作成するためのスクリプトを生成します。 生成されたスクリプトは、サブスクライバー側でサブスクリプション データベースについて実行されます。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを含むパブリケーションの名前です。 名前は、データベース内で一意である必要があります。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'` サブスクリプション アーティクルの名前です。 *記事*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar (4000)**|キューに登録されたサブスクリプション アーティクルのサブスクライバー上に競合テーブルを作成するための [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを返します。 このスクリプトは、サブスクライバー側でサブスクリプション データベースで実行されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_scriptsubconflicttable**を初期スナップショットが手動でに適用されるサブスクリプションを持つサブスクライバーに使用します。 競合テーブルは、サブスクライバーで省略可能なテーブルです。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_scriptsubconflicttable**します。  
  
## <a name="see-also"></a>関連項目  
 [キュー更新における競合の検出と解決](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
