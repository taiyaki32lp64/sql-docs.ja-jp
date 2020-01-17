---
title: sp_syscollector_stop_collection_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_stop_collection_set_TSQL
- sp_syscollector_stop_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_stop_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 4668cfb7-462f-40d0-948c-8f740a792a4d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3e09efe938dabb031e1c57020f051cd5ab03e55a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010570"
---
# <a name="spsyscollectorstopcollectionset-transact-sql"></a>sp_syscollector_stop_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクション セットを停止します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_stop_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @stop_collection_job = ] stop_collection_job ]  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_id = ] *collection_set_id*  
 コレクション セットの一意なローカル識別子を指定します。 *collection_set_id*は**int**既定値は NULL です。 *collection_set_id*場合、値が必要*名前*は NULL です。  
  
 [ @name = ] '*name*'  
 コレクション セットの名前を指定します。 *名前*は**sysname**既定値は NULL です。 *名前*場合、値が必要*collection_set_id*は NULL です。  
  
 [ @stop_collection_job = ] *stop_collection_job*  
 コレクション セットのコレクション ジョブが実行されている場合に、停止を指定します。 *stop_collection_job*は**ビット**既定値は 1 です。  
  
 *stop_collection_job*コレクション モードを設定してキャッシュにコレクション セットにのみ適用されます。 詳細については、次を参照してください。 [sp_syscollector_create_collection_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syscollector_create_collection_set は、msdb システム データベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_operator 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、識別子を使用してコレクション セットを停止します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクション](../../relational-databases/data-collection/data-collection.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
