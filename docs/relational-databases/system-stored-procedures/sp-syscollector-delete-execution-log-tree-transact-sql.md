---
title: sp_syscollector_delete_execution_log_tree (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_execution_log_tree_TSQL
- sp_syscollector_delete_execution_log_tree
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_execution_log_tree
- data collector [SQL Server], stored procedures
ms.assetid: 0a9a7c5b-c3cc-40ca-b524-e948a8cce4e4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9aa59c95b211591ce89b3207b2bac181bb413222
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000834"
---
# <a name="spsyscollectordeleteexecutionlogtree-transact-sql"></a>sp_syscollector_delete_execution_log_tree (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つのコレクション セットの実行のすべてのログ エントリを削除します。 ログ エントリの削除も、[!INCLUDE[ssIS](../../includes/ssis-md.md)]を実行するためのテーブル。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_delete_execution_log_tree[ @log_id = ] log_id  
          , [ @from_collection_set = ] from_collection_set  
```  
  
## <a name="arguments"></a>引数  
`[ @log_id = ] log_id` コレクションの一意の識別子は、ログを設定します。 *log_id*は**int**します。  
  
`[ @from_collection_set = ] from_collection_set` コレクション セットの識別子です。 *from_collection_set*は**ビット 1 =** します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **dc_operator** (EXECUTE 権限) を持つ固定データベース ロールにこのプロシージャを実行します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
