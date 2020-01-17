---
title: トランザクション (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c8e70e80cf7e2ddedce7a56c7d7bc92ed3b161b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072163"
---
# <a name="transactions-transact-sql"></a>トランザクション (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  トランザクションは、1 つの作業を表す単位です。 トランザクションが成功すると、トランザクションの実行中に行われたすべてのデータ変更がコミットされ、データベースの変更が確定します。 エラーが発生したため、トランザクションを取り消すか、またはロールバックする必要がある場合、すべてのデータ変更は消去されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次のトランザクション モードで動作します。  
  
 自動コミット トランザクション  
 各ステートメントは 1 つのトランザクションです。  
  
 明示的なトランザクション  
 各トランザクションは、BEGIN TRANSACTION ステートメントで明示的に開始し、COMMIT または ROLLBACK ステートメントで明示的に終了します。  
  
 暗黙のトランザクション  
 新しいトランザクションは、前のトランザクションが終了すると暗黙的に開始しますが、各トランザクションは COMMIT または ROLLBACK ステートメントで明示的に終了します。  
  
 バッチスコープのトランザクション  
 複数のアクティブな結果セット (MARS) にのみ該当します。MARS セッションで開始された [!INCLUDE[tsql](../../includes/tsql-md.md)] の明示的または暗黙的なトランザクションは、バッチスコープのトランザクションになります。 バッチの完了時にコミットまたはロールバックされていないバッチスコープのトランザクションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により自動的にロールバックされます。  

> [!NOTE] 
> データ ウェアハウスに関連する特別な考慮事項については、「[トランザクション (SQL データ ウェアハウス)](transactions-sql-data-warehouse.md)」を参照してください。   

## <a name="in-this-section"></a>このセクションの内容  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、次のトランザクション ステートメントが用意されています。  
  
|||  
|-|-|  
|[BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[COMMIT TRANSACTION](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[SAVE TRANSACTION](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[COMMIT WORK](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>参照  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
