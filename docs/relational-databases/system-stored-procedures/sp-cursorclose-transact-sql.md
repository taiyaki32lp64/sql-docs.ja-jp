---
title: sp_cursorclose (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 543e8c0b41000ec2afe9ab07aef08aa86967c2ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108565"
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  閉じると、カーソルの割り当てを解除だけでなく関連付けられているリソースをすべて解放つまり、KEYSET または STATIC のサポートに使用される一時テーブルを削除**カーソル**します。 sp_cursorclose は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットで 9 を = です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 カーソル*処理*によって生成される値[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]され、sp_cursoropen プロシージャから返されます。 *カーソル*が必要なパラメーターです、 **int**値を入力します。  
  
> [!NOTE]  
>  入力の値を-1 は、現在の接続ですべてのカーソルに適用されます。  
  
## <a name="remarks"></a>コメント  
 *カーソル*カーソルが閉じられた後、プロシージャが実行された場合、または無効なハンドルが指定されている場合、エラー メッセージが返されます。  
  
 RPC の状態は、全体的な成功または失敗を示します。  
  
 DONE の行数は常に 0 です。  
  
## <a name="see-also"></a>関連項目  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
