---
title: BEGIN...END (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BEGIN
- BEGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e278e41fa2f27684b1ce249bb45b1dc78356753
ms.sourcegitcommit: a92fa97e7d3132ea201e4d86c76ac39cd564cd3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2019
ms.locfileid: "75325564"
---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのグループを実行できるように、一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを囲みます。 BEGIN と END はフロー制御言語のキーワードです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>引数  
 { *sql_statement* | *statement_block* }  
 有効な 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、またはステートメント ブロックで定義したステートメントのグループを指定します。  
  
## <a name="remarks"></a>解説  
 BEGIN...END ブロックは入れ子にできます。  
  
 BEGIN...END ブロック内ではすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが有効ですが、同じバッチまたはステートメント ブロック内で一緒にグループ化できない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントもあります。  
  
## <a name="examples"></a>例  
 次の例では、`BEGIN` と `END` を使用して、まとめて実行する一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを定義します。 `BEGIN...END` ブロックが指定されていない場合、両方の `ROLLBACK TRANSACTION` ステートメントが実行され、両方の `PRINT` メッセージが返されます。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、`BEGIN` と `END` を使用して、まとめて実行する一連の [!INCLUDE[DWsql](../../includes/dwsql-md.md)] ステートメントを定義します。 `BEGIN...END` ブロックが含まれていない場合、次の例は連続するループになります。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
    SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [フロー制御言語 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  


