---
title: sp_invalidate_textptr (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_invalidate_textptr_TSQL
- sp_invalidate_textptr
dev_langs:
- TSQL
helpviewer_keywords:
- sp_invalidate_textptr
ms.assetid: dd9920e1-7064-4c05-93d8-9303103fa1d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81df88f6e451d71dc5778e49162db97def7ed27d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113192"
---
# <a name="spinvalidatetextptr-transact-sql"></a>sp_invalidate_textptr (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定した行内テキスト ポインター、またはトランザクション内のすべての行内テキスト ポインターを無効にします。 **sp_invalidate_textptr**行内テキスト ポインターに対してのみ使用できます。 これらのポインターがあるテーブルからは、**行内テキスト**オプションを有効にします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>引数  
`[ @TextPtrValue = ] textptr_value` 行内テキスト ポインターは無効にします。 *textptr_value*は**varbinary (** 16 **)** 、既定値は NULL です。 NULL の場合、 **sp_invalidate_textptr**トランザクション内のすべての行内テキスト ポインターが無効になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、各データベースの各トランザクションに、アクティブで有効な行内テキスト ポインターを 1,024 個まで使用できます。ただし、複数のデータベースにまたがるトランザクションの場合は、各データベースに行内テキスト ポインターを 1,024 個まで使用できます。 **sp_invalidate_textptr**行内テキスト ポインターを無効にし、そのため、他の行内テキスト ポインター用に領域を解放するために使用できます。  
  
 Text in row オプションの詳細については、次を参照してください。 [sp_tableoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
