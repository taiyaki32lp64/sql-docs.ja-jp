---
title: sp_syscollector_enable_collector (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_enable_collector
- sp_syscollector_enable_collector_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_enable_collector
- data collector [SQL Server], stored procedures
ms.assetid: 53ff2b0d-b7da-4e3d-8f3d-35e857bc3720
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab6087b68fba057e6acd91f43804b0e324992e1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000806"
---
# <a name="spsyscollectorenablecollector-transact-sql"></a>sp_syscollector_enable_collector (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データ コレクターを有効にします。 サーバーごとに 1 つだけのデータ コレクターがあるため、パラメーターは必要ありません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
dbo.sp_syscollector_enable_collector   
```  
  
## <a name="arguments"></a>引数  
 なし  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 既定値は、サーバー上のデータ コレクターです。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) **dc_admin** または **dc_operator** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、データ コレクターを有効にします。  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
