---
title: sp_mergedummyupdate (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 209a41ff29f8063ec6c46fe1fb5e821be1419cd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019980"
---
# <a name="spmergedummyupdate-transact-sql"></a>sp_mergedummyupdate (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定した行でダミーを更新し、その更新が次のマージで再送されるようにします。 パブリッシャーのパブリケーション データベースまたはサブスクライバーのサブスクリプション データベースに対して、このストアド プロシージャを実行できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>引数  
`[ @source_object = ] 'source_object'` ソース オブジェクトの名前です。 *source_object*は**nvarchar (386)** 、既定値はありません。  
  
`[ @rowguid = ] 'rowguid'` 行識別子です。 *rowguid*は**uniqueidentifier**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_mergedummyupdate**はマージ レプリケーションで使用します。  
  
 **sp_mergedummyupdate**レプリケーション競合表示モジュール (Wzcnflct.exe) する代わりに、独自に記述する場合に便利です。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **db_owner**固定データベース ロールが実行できる**sp_mergedummyupdate**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
