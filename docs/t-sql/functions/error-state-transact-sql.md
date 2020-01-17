---
title: ERROR_STATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_STATE_TSQL
- ERROR_STATE
dev_langs:
- TSQL
helpviewer_keywords:
- messages [SQL Server], state
- ERROR_STATE function
- errors [SQL Server], state
- TRY...CATCH [SQL Server]
- CATCH block
- states [SQL Server], error numbers
ms.assetid: 6059af00-83fe-409f-ab7c-daad111bc671
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 694017e60682d191bd1d02cdc231b7185c3b8c87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094609"
---
# <a name="errorstate-transact-sql"></a>ERROR_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  TRY...CATCH 構造の CATCH ブロックが実行された原因となるエラーの状態番号を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ERROR_STATE ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
 CATCH ブロックの中で呼び出された場合は、CATCH ブロックが実行された原因となるエラー メッセージの状態番号を返します。  
  
 CATCH ブロックの範囲外で呼び出された場合は NULL を返します。  
  
## <a name="remarks"></a>Remarks  
 エラー メッセージが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] のコード内の複数の場所で生成される場合があります。 たとえば、異なる複数の条件で "1105" エラーが生成されることがあります。 エラーを生成するそれぞれの条件によって、一意の状態コードが割り当てられます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報などの既知の問題のデータベースを参照する際には、この状態番号を使用して、データベースに登録されている問題が、実際に発生したエラーと同じものかどうかを確認できます。 たとえば、技術情報の資料で取り上げられている 1105 エラー メッセージの状態番号が 2 で、実際の 1105 エラー メッセージの状態番号が 3 だった場合、そのエラーは、その資料で報告されているものとは別の原因で発生したと考えられます。  
  
 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサポート エンジニアは状態コードを使用して、エラーが発生したソース コード内の場所を探し、問題を診断することができます。  
  
 ERROR_STATE は、CATCH ブロックのスコープ内の任意の場所で呼び出すことができます。  
  
 ERROR_STATE は、実行された回数や実行される CATCH ブロックのスコープ内の場所に関係なく、エラー状態を返します。 これは、@@ERROR などの関数とは対照的です。これらの関数がエラー番号を返すのは、エラーが発生したステートメントの直後のステートメントか、CATCH ブロックの最初のステートメントだけです。  
  
 入れ子になった CATCH ブロックでは、ERROR_STATE は、参照されている CATCH ブロックのスコープに固有のエラー状態を返します。 たとえば、外側の TRY...CATCH 構造の CATCH ブロックには、TRY...CATCH 構造が入れ子にされている場合があります。 この場合、入れ子になった CATCH ブロック内では、ERROR_STATE は、入れ子になった CATCH ブロックを呼び出したエラーの状態を返します。 ERROR_STATE が外部の CATCH ブロックで実行された場合は、その CATCH ブロックを呼び出したエラーの状態が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-errorstate-in-a-catch-block"></a>A. CATCH ブロックで ERROR_STATE を使用する  
 次の例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 エラーの状態が返されます。  
  
```sql  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>B. CATCH ブロックで ERROR_STATE を他のエラー処理ツールと一緒に使用する  
 次の例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 エラーの状態と共にエラーに関する情報が返されます。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>C. CATCH ブロックで ERROR_STATE を他のエラー処理ツールと一緒に使用する  
 次の例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 エラーの状態と共にエラーに関する情報が返されます。  
  
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
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)    
 [エラーとイベントのリファレンス &#40;データベース エンジン&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
    

