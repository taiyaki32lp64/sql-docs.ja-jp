---
title: sp_dropextendedproc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: stevestein
ms.author: sstein
ms.openlocfilehash: b12ebcfb662db9740efdf918f0857b94144e0ceb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054299"
---
# <a name="spdropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拡張ストアド プロシージャを削除します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CLR 統合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) を使用してください。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>引数  
`[ @functname = ] 'procedure'` 削除する拡張ストアド プロシージャの名前です。 *プロシージャ*は**nvarchar (517)** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 実行**sp_dropextendedproc**からユーザー定義の拡張ストアド プロシージャ名を削除、 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)カタログ ビューからエントリを削除して、 [sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)カタログ ビューです。 このストアド プロシージャでのみ実行できる、**マスター**データベース。  
  
**sp_dropextendedproc**システム拡張ストアド プロシージャを削除できません。 代わりに、システム管理者がする拡張ストアド プロシージャに対する EXECUTE 権限を拒否する必要があります、**パブリック**ロール。  
  
 **sp_dropextendedproc**トランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_dropextendedproc**します。  
  
## <a name="examples"></a>使用例  
 次の例では、削除、`xp_hello`拡張ストアド プロシージャ。  
  
> [!NOTE]  
>  既に存在する必要がありますこの拡張ストアド プロシージャまたは例では、エラー メッセージを返します。  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
