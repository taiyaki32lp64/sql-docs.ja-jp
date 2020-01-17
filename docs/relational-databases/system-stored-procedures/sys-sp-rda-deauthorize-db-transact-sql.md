---
title: sys.sp_rda_deauthorize_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6aeb27d4fb452a4ed5b7f45086f601eacb4f0339
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905113"
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>sys.sp_rda_deauthorize_db (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  ローカルの Stretch 対応データベースとリモート Azure データベース間の認証された接続を削除します。 実行**sp_rda_deauthorize_db**とリモートのデータベースが到達不可または不整合な状態で、データベース内のすべての Stretch 対応テーブルに対するクエリ動作を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または > 0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 Db_owner アクセス許可が必要です。  
  
## <a name="remarks"></a>コメント  
 実行した後**sp_rda_deauthorize_db** 、Stretch 対応データベースとテーブルに対するすべてのクエリは失敗します。 つまり、クエリ モードは無効に設定します。 このモードを終了するには、次のいずれかの操作を行います。  
  
-   実行[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)リモート Azure データベースに再接続します。 この操作に自動的にリセット クエリ モード LOCAL_AND_REMOTE、Stretch Database の既定の動作はします。 つまり、クエリは、ローカルとリモートの両方のデータから結果を返します。  
  
-   実行[sys.sp_rda_set_query_mode &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)をクエリがローカルのデータのみに対して引き続き実行できるように、LOCAL_ONLY 引数。  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_rda_set_query_mode &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
