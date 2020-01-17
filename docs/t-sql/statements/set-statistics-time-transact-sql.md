---
title: SET STATISTICS TIME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 90eb59652bf64e6e3be4edaa3cce2f0bf3c02df7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897997"
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  各ステートメントの解析、コンパイル、および実行に必要な時間をミリ秒単位で表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET STATISTICS TIME が ON の場合、ステートメントの処理時間の統計が表示されます。 OFF の場合、時間の統計は表示されません。  
  
 SET STATISTICS TIME は、解析時ではなく実行時に設定されます。  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、**簡易プーリング**構成オプションを有効にしたときに起動されるファイバー モードでは正確な統計情報を提供できません。  
  
 **sysprocesses** テーブル内の **cpu** 列が更新されるのは、SET STATISTICS TIME が ON の状態でクエリが実行されたときだけです。 SET STATISTICS TIME が OFF の場合は、**0** が返されます。  
  
 この設定が ON であるか OFF であるかによって、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [現在の利用状況] の [プロセス情報] ビューにある CPU 列にも影響します。  
  
## <a name="permissions"></a>アクセス許可  
 SET STATISTICS TIME を使用するには、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限が必要です。 SHOWPLAN 権限は必要ありません。  
  
## <a name="examples"></a>使用例  
 この例では、サーバーの実行、解析、コンパイルの時間を表示します。  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
