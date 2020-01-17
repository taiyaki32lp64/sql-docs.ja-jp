---
title: sp_resetsnapshotdeliveryprogress (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc6205eb5487b89db55488bcdf36fbb036595d57
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129647"
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  スナップショットの配信が再起動できるように、プル サブスクリプションのスナップショット配信処理をリセットします。 サブスクライバー側でサブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @verbose_level = ] verbose_level` 返される情報量を指定します。 *verbose_level*は**int**、既定値は**1**します。 値**1**で必要なロックを取得できないかどうかにエラーがあることを意味が返される、 **MSsnapshotdeliveryprogress**テーブル、および**0**エラーが返されないことを意味します。  
  
`[ @drop_table = ] 'drop_table'` 削除するか、スナップショットのテーブルを含むの進行状況の情報を切り捨てるかどうかです。*drop_table*は**nvarchar (5)** 、既定値は**FALSE**します。 false は、テーブルが切り捨てられることと、true は、テーブルが削除されることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_resetsnapshotdeliveryprogress**のすべての行を削除、 **MSsnapshotdeliveryprogress**テーブル。 これは実質的になくなりますすべて残されたメタデータをサブスクリプション データベースのスナップショットの配信プロセスで以前進行しています。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_resetsnapshotdeliveryprogress**します。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
