---
title: sp_droptype (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droptype_TSQL
- sp_droptype
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droptype
ms.assetid: e78464ac-2370-4c4e-9cc0-06aebc07cec5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 13ef625d778fe20aa5d33b2958c90aa8cd5a2a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088470"
---
# <a name="spdroptype-transact-sql"></a>sp_droptype (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  別名データ型からの削除**systypes**します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>引数  
`[ @typename = ] 'type'` 所有している別名データ型の名前です。 *型*は**sysname**、既定値はありません。  
  
## <a name="return-code-type"></a>リターン コードの種類  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **型**エイリアス テーブルやその他のデータベース オブジェクトが参照している場合のデータ型を削除することはできません。  
  
> [!NOTE]  
>  別名データ型は、テーブル定義内で使用されている場合、またはをルールまたはデフォルトがバインドされている場合、別名データ型を削除できません。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **db_owner**固定データベース ロール、または**db_ddladmin**固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、別名データ型を削除する`birthday`します。  
  
> [!NOTE]  
>  この別名データ型は存在している必要があります。存在しない場合、この例ではエラー メッセージが返されます。  
  
```  
USE master;  
GO  
EXEC sp_droptype 'birthday';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addtype &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
