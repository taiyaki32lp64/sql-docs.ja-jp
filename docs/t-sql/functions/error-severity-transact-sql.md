---
title: ERROR_SEVERITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_SEVERITY_TSQL
- ERROR_SEVERITY
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], severity
- messages [SQL Server], severity
- TRY...CATCH [SQL Server]
- CATCH block
- ERROR_SEVERITY function
ms.assetid: 50228f2f-6949-4d2e-8e43-fad11bf973ab
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a5df90640dc9ebdd2d59593c4b2a82a0f7daa00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094651"
---
# <a name="errorseverity-transact-sql"></a>ERROR_SEVERITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

エラーが発生し、そのエラーによって TRY…CATCH 構文の CATCH ブロックが実行された場合、この関数によってエラーの重大度が返されます。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ERROR_SEVERITY ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
エラーが発生した CATCH ブロックの中で呼び出されると、`ERROR_SEVERITY` は `CATCH` ブロックの実行を引き起こしたエラーの重大度を返します。  

`ERROR_SEVERITY` は、CATCH ブロックの範囲外で呼び出された場合に NULL を返します。  
  
## <a name="remarks"></a>Remarks  
`ERROR_SEVERITY` は、CATCH ブロックのスコープ内の任意の場所で呼び出すことができます。  
  
`ERROR_SEVERITY` は、実行回数に関係なく、あるいは `CATCH` ブロックのスコープ内の実行場所に関係なく、エラーのエラー重大度を返します。 エラーが発生したステートメントの直後のステートメントのエラー番号のみを返す、@@ERROR などの関数とは対照的となります。  
  
通常、`ERROR_SEVERITY` は入れ子になった `CATCH` ブロック内で動作します。 `ERROR_SEVERITY` は、`CATCH` ブロックを参照した `CATCH` ブロックのスコープに固有のエラー重大度を返します。 たとえば、外側の TRY...CATCH 構造の `CATCH` ブロックの中に `TRY...CATCH` 構造が含まれることがあります。 その内側の `CATCH` ブロック内では、`ERROR_SEVERITY` は内側の `CATCH` ブロックを呼び出したエラーの重大度を返します。 `ERROR_SEVERITY` が外側の `CATCH` ブロック内で実行される場合、外側の `CATCH` ブロックを呼び出したエラーの重大度を返します。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-errorseverity-in-a-catch-block"></a>A. CATCH ブロックで ERROR_SEVERITY を使用する  
この例では、0 除算エラーを生成したストアド プロシージャを示します。 `ERROR_SEVERITY` はそのエラーの重大度を返します。  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorSeverity
-------------
16

(1 row(s) affected)

```  
  
### <a name="b-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>B. CATCH ブロックで ERROR_SEVERITY を他のエラー処理ツールと一緒に使用する  
この例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 ストアド プロシージャは、エラーに関する情報を返します。  

```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine   ErrorMessage
----------- ------------- ----------- --------------- ----------- ----------------------------------
8134        16            1           NULL            4           Divide by zero error encountered.

(1 row(s) affected)

```  
  
## <a name="see-also"></a>参照  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
 [エラーとイベントのリファレンス &#40;データベース エンジン&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
    

