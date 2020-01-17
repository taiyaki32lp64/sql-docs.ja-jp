---
title: SET ROWCOUNT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_ROWCOUNT_TSQL
- ROWCOUNT_TSQL
- SET ROWCOUNT
- ROWCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- row return limitations [SQL Server]
- SET ROWCOUNT statement
- number of rows affected by statement
- ROWCOUNT option
- counting rows
- stopping queries
- limiting rows returned
- queries [SQL Server], stopping
ms.assetid: c6966fb7-6421-47ef-98f3-82351f2f6bdc
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f79e7931e0e1fd04a699620f65c1dc2566347202
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140230"
---
# <a name="set-rowcount-transact-sql"></a>SET ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定の行数が返された後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリの処理を停止します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SET ROWCOUNT { number | @number_var }   
```  
  
## <a name="arguments"></a>引数  
 *number* | @*number_var*  
 特定のクエリを停止するまでに処理される行数を整数で指定します。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  SQL Server の将来のリリースでは、SET ROWCOUNT を使用しても、DELETE、INSERT、および UPDATE ステートメントが影響を受けることはありません。 新しい開発作業では DELETE、INSERT、および UPDATE ステートメントでの SET ROWCOUNT の使用を避け、現在 SET ROWCOUNT を使用しているアプリケーションは変更を検討してください。 同様の処理を行う場合は、TOP 構文を使用します。 詳細については、「[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)」を参照してください。  
  
 このオプションをオフにして、すべての行が返されるようにするには、SET ROWCOUNT 0 を指定します。  
  
 SET ROWCOUNT オプションを設定すると、大部分の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、指定した行数の処理が終わったところで処理が停止します。 これにはトリガーも含まれます。 ROWCOUNT オプションは動的カーソルには影響しませんが、このオプションによってキーセット カーソルと非反映型カーソルの行セットは制限されます。 このオプションの使用には注意が必要です。  
  
 SET ROWCOUNT で指定された行数が SELECT ステートメントの TOP キーワードの値より少ない場合は、SET ROWCOUNT の値がオーバーライドされます。  
  
 SET ROWCOUNT は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 SET ROWCOUNT を指定した場合、指定した行数が返されると処理は停止します。 次の例では、500 行を超える行数は、`Quantity` が `300` より少ないという条件を満たしていますが、 SET ROWCOUNT の適用後、すべての行が返されたわけではないことがわかります。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT count(*) AS Count  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Count 
 ----------- 
 537 
 
 (1 row(s) affected)
 ```  
  
 ここで `ROWCOUNT` を `4` に設定し、すべての行のうち、4 行だけが返されることを確認します。  
  
```  
SET ROWCOUNT 4;  
SELECT *  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
  
(4 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 SET ROWCOUNT を指定した場合、指定した行数が返されると処理は停止します。 次の例では、20 より多くの行が `AccountType = 'Assets'` の条件を満たしていることに注意してください。 SET ROWCOUNT の適用後、すべての行が返されたわけではないことがわかります。  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 5;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
 すべての行を返すには、ROWCOUNT を 0 に設定します。  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 0;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

