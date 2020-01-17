---
title: DROP ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ROUTE
- DROP_ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping routes
- DROP ROUTE statement
- deleting routes
- routes [Service Broker], removing
- removing routes
ms.assetid: d8fab0bc-d54a-46ca-9437-552db7477d40
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b11908f182037a1368b9d1fda34ebda3f1422918
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022588"
---
# <a name="drop-route-transact-sql"></a>DROP ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ルートを削除し、その情報を現在のデータベースのルーティング テーブルから削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP ROUTE route_name  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *route_name*  
 削除するルートの名前を指定します。 サーバー名、データベース名、スキーマ名は指定できません。  
  
## <a name="remarks"></a>Remarks  
 ルートを格納するルーティング テーブルは、カタログ ビュー **sys.routes** を介して読み取ることができるメタデータ テーブルです。 このルーティング テーブルは、CREATE ROUTE、ALTER ROUTE、DROP ROUTE ステートメントでのみ更新できます。  
  
 メッセージ交換でルートが使用されているかどうかに関係なく、ルートを削除することができますが、 しかし、リモート サービスへのルートが他に存在しない場合は、リモート サービスへのルートが作成されるか、メッセージ交換がタイムアウトになるまで、メッセージ交換のメッセージは転送キューに残ります。  
  
## <a name="permissions"></a>アクセス許可  
 ルートを削除する権限は、既定ではルートの所有者、db_ddladmin 固定データベース ロールまたは db_owner 固定データベース ロールのメンバー、および sysadmin 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
 次の例では、`ExpenseRoute` ルートを削除します。  
  
```  
DROP ROUTE ExpenseRoute ;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.routes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)  
  
  
