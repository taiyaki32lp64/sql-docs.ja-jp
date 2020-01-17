---
title: CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6278faa80721ce500257650db70359dcc740ee8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132074"
---
# <a name="context_info--transact-sql"></a>CONTEXT_INFO  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、現在のセッションまたはバッチに設定された、または [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) ステートメントを使用して派生した **context_info** 値を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>戻り値
**context_info** 値。
  
**Context_info** は設定されませんでした: 場合
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は NULL を返します。  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] で  、一意のセッション固有 GUID.を返します。  
  
## <a name="remarks"></a>Remarks  
複数のアクティブな結果セット (MARS) 機能によって、アプリケーションは複数のバッチまたは要求を同じ接続上で同時に実行できます。 `CONTEXT_INFO` 関数が SET ステートメントと同じバッチで実行される場合、MARS 接続バッチの 1 つで SET CONTEXT_INFO を実行すると、`CONTEXT_INFO` 関数は新しいコンテキスト値を返します。 `CONTEXT_INFO` 関数が他の 1 つ以上の接続バッチで実行されている場合、SET ステートメントを実行したバッチの完了後にバッチが開始されない限り、`CONTEXT_FUNCTION` は新しい値を返しません。
  
## <a name="permissions"></a>アクセス許可  
特に必要な権限はありません。 次のシステム ビューはコンテキスト情報を格納しますが、これらのビューに直接クエリを実行するには SELECT および VIEW SERVER STATE アクセス許可が必要です。
- **sys.dm_exec_requests**
- **sys.dm_exec_sessions**
- **sys.sysprocesses**
  
## <a name="examples"></a>使用例  
この簡単な例では、**context_info** 値を `0x1256698456` に設定してから、`CONTEXT_INFO` 関数を使用して値を取得します。
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>参照
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
