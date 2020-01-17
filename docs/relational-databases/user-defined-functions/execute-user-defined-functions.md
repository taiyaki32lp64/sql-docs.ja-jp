---
title: ユーザー定義関数の実行 | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b028b6ab4da678444427682a635f679acce576ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123589"
---
# <a name="execute-user-defined-functions"></a>ユーザー定義関数の実行
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Transact-SQL を使用してユーザー定義関数を実行する
  

> **注:** ユーザー定義関数の詳細については、「[ユーザー定義関数](user-defined-functions.md)」および「[CREATE FUNCTION (Transact SQL)](../../t-sql/statements/create-function-transact-sql.md)」を参照してください。 
  
 
##  <a name="BeforeYouBegin"></a> はじめる前に  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 Transact-SQL では、 *値* を使用するか、@*parameter_name*=*値.* を使用し、パラメーターを指定できます。 パラメーターは、トランザクションの一部ではないです。そのため、トランザクションが後でロールバックの値にパラメーターが変更された場合、パラメーター戻すことはできません前の値にします。 呼び出し元に返される値は常に、モジュールから戻る時点での値になります。  
  
###  <a name="Security"></a> セキュリティ  
  
 [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) ステートメントの実行に権限は必要ありませんが、 EXECUTE 文字列内で参照されるセキュリティ保護可能なリソースに対しては権限が **必要です** 。 たとえば、この文字列に [INSERT](../../t-sql/statements/insert-transact-sql.md) ステートメントが含まれている場合、EXECUTE ステートメントの呼び出し元は対象のテーブルに対する INSERT 権限が必要です。 EXECUTE ステートメントは、モジュール内に含まれている場合でも、検出されるたびに権限が確認されます。 詳細については、「[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
### <a name="example"></a>例 
  
この例では、 `ufnGetSalesOrderStatusText` のほとんどのエディションで利用できる `AdventureWorks`スカラー値関数を使用しています。  この関数の目的は、所与の整数から売り上げ状況のテキスト値を返すことです。  **\@Status** パラメーターに 1 ～ 7 の整数を渡すことで例を変えられます。
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
