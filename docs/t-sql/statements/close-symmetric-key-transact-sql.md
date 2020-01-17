---
title: CLOSE SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLOSE SYMMETRIC KEY
- CLOSE_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- closing symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], closing
- CLOSE SYMMETRIC KEY statement
- cryptography [SQL Server], symmetric keys
ms.assetid: 3b083cbb-3c6a-4f59-8d34-601db1efcc83
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8d0f9c50b5d89926f370f9059a1cbce6c246e216
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141164"
---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定した対称キー、または現在のセッションで開いているすべての対称キーを閉じます。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
## <a name="arguments"></a>引数  
 *Key_name*  
 閉じる対称キーの名前を指定します。  
  
## <a name="remarks"></a>Remarks  
 開いている対称キーは、セキュリティ コンテキストではなくセッションにバインドされており、 明示的に閉じられるか、セッションが終了するまで引き続き使用できます。 CLOSE ALL SYMMETRIC KEYS では、[OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) ステートメントによって現在のセッションで開いていた任意のデータベースのマスター キーが閉じられます。  開いているキーに関する情報は、[sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) カタログ ビューで確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 対称キーを閉じるために、明示的な権限は必要ありません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-closing-a-symmetric-key"></a>A. 対称キーを閉じる  
 次の例では、対称キー `ShippingSymKey04` を閉じます。  
  
```  
CLOSE SYMMETRIC KEY ShippingSymKey04;  
GO  
```  
  
### <a name="b-closing-all-symmetric-keys"></a>B. すべての対称キーを閉じる  
 次の例では、現在のセッションで開いているすべての対称キーと、明示的に開かれたデータベースのマスター キーを閉じます。  
  
```  
CLOSE ALL SYMMETRIC KEYS;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  
