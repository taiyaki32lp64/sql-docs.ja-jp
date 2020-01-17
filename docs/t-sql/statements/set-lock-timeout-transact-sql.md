---
title: SET LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97bdfbe485c129e7040235db7fffe296bb16897a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928906"
---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  ロックが解除されるまでのステートメントの待ち時間をミリ秒単位で指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>引数  
 *timeout_period*  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がロック エラーを返すまでの経過時間をミリ秒単位で指定します。 値が -1 (既定値) の場合は、タイムアウトはなく、無期限に待機します。  
  
 ロックの待ち時間がタイムアウト値を超えると、エラーが返されます。 値が 0 の場合は、待ち時間はなく、ロックがかかるとすぐにメッセージが返されます。  
  
## <a name="remarks"></a>Remarks  
 この設定では、接続の開始時に -1 が割り当てられます。 この値が変更されると、その接続の残りの期間については、新しい設定が適用されます。  
  
 SET LOCK_TIMEOUT は、解析時ではなく実行時に設定されます。  
  
 SET オプションの代わりに READPAST ロック ヒントを使用できます。  
  
 CREATE DATABASE、ALTER DATABASE、および DROP DATABASE ステートメントでは、SET LOCK_TIMEOUT の設定は無視されます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>A:ロック タイムアウトを 1,800 ミリ秒に設定する  
 次の例では、ロック タイムアウトの待ち時間を `1800` ミリ秒に設定します。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. ロックが解放されるまで無限に待機するようにロック タイムアウトを設定する。  
 次の例では、ロック タイムアウトを無期限に待機して期限切れにならないように設定します。 これは、各接続の開始時に既に設定されている既定の動作です。  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 次の例では、ロック タイムアウトの待ち時間を `1800` ミリ秒に設定します。 このリリースの [!INCLUDE[ssDW](../../includes/ssdw-md.md)] は、ステートメントを正常に解析しますが、1800 という値は無視して既定の動作を使い続けます。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>参照  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

