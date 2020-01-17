---
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5baec7bb0328f6765bc4d4e1a04993074ad62999
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843523"
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  最後のステートメントの影響を受けた行数を返します。 行の数が 20億を超える場合は、次のようを使用して [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、次の方法で @@ROWCOUNT に値を設定できます。  
  
-   @@ROWCOUNT に、影響を受ける行または読み取られる行の数を設定します。 行はクライアントに送信される場合と、送信されない場合があります。  
  
-   前にステートメントを実行したときの @@ROWCOUNT を保存します。  
  
-   @@ROWCOUNT を 0 にリセットしますが、クライアントにはその値を返しません。  
  
 単純な割り当てを行うステートメントの場合、@@ROWCOUNT の値は常に 1 に設定されます。 行はクライアントに送信されません。 ステートメントの例は次のとおりです。SET @*local_variable*、RETURN、READTEXT、および SELECT GETDATE() または SELECT **'***一般的なテキスト***'** などのクエリのない SELECT ステートメント。  
  
 クエリ内で代入操作をするステートメントまたはクエリ内で RETURN を使用するステートメントは、クエリの影響を受ける行またはクエリに読み取られる行の数を @@ROWCOUNT 値に設定します (例: SELECT @*local_variable* = c1 FROM t1)。  
  
 データ操作言語 (DML) ステートメントは、@@ROWCOUNT 値に、クエリに影響を受ける行の数を設定し、この値をクライアントに返します。 DML ステートメントは、クライアントに行を送信しない場合もあります。  
  
 DECLARE CURSOR および FETCH は、@@ROWCOUNT 値に 1 を設定します。  
  
 EXECUTE ステートメントは、前の @@ROWCOUNT を保存します。  
  
 USE、SET \<option>、DEALLOCATE CURSOR、CLOSE CURSOR、PRINT、RAISERROR、BEGIN TRANSACTION、COMMIT TRANSACTION などのステートメントは、ROWCOUNT 値を 0 にリセットします。  
  
 ネイティブ コンパイル ストアド プロシージャでは、直前の @@ROWCOUNT が維持されます。 ネイティブ コンパイル ストアド プロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、@@ROWCOUNT は設定しないでください。 詳細については、次を参照してください。 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)です。  
  
## <a name="examples"></a>使用例  
 次の例では、`UPDATE` ステートメントを実行し、`@@ROWCOUNT` を使用して、変更された行があるかどうかを調べます。  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  
