---
title: DROP ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_ENDPOINT_TSQL
- DROP ENDPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- removing endpoints
- endpoints [SQL Server], removing
- deleting endpoints
- DROP ENDPOINT statement
- dropping endpoints
ms.assetid: 6aca7412-66a5-4fa4-86b2-061512ff2080
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b490b3aae8fce4ef7b4ae912275e8a338f44833
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898061"
---
# <a name="drop-endpoint-transact-sql"></a>DROP ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存のエンドポイントを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP ENDPOINT endPointName  
```  
  
## <a name="arguments"></a>引数  
 *endPointName*  
 削除するエンドポイント名です。  
  
## <a name="remarks"></a>Remarks  
 ENDPOINT DDL ステートメントは、ユーザー トランザクション内部では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール **sysadmin** のメンバーであるか、そのエンドポイントの所有者であるか、またはエンドポイントに対する CONTROL 権限が許可されている必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、以前に作成したエンドポイント `sql_endpoint` を削除します。  
  
```  
DROP ENDPOINT sql_endpoint;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
