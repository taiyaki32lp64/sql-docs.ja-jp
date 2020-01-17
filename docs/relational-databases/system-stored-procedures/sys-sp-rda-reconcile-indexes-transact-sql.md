---
title: sys.sp_rda_reconcile_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0e439a04e55816f25cae318a8451452bf09dee0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905046"
---
# <a name="syssprdareconcileindexes-transact-sql"></a>sys.sp_rda_reconcile_indexes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  リモート テーブルのインデックスを調整するスキーマ タスク キューに入れます。 このタスクが正常に完了すると、リモート テーブルがローカルの Stretch 対応テーブルに存在すると同じインデックスにあります。  
  
 呼び出すときにインデックスを調整する別のタスクがキューに存在する場合**sp_rda_reconcile_indexes**、重複するタスクがこのストアド プロシージャをキューに登録します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>引数  
 [@objname =] *'objname'*  
 インデックスを調整する、Stretch 対応テーブルの修飾名または非修飾名です。 修飾されたオブジェクトを指定する場合にのみ、引用符が必要です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または > 0 (失敗)  
  
## <a name="see-also"></a>関連項目  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
