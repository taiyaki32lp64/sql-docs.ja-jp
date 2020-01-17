---
title: SAVE TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SAVE
- SAVE_TSQL
- SAVE_TRANSACTION_TSQL
- SAVE TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- rolling back transactions, SAVE TRANSACTION
- SAVE TRANSACTION statement
- transactions [SQL Server], rolling back
- marking transactions [SQL Server]
- savepoints [SQL Server]
- marked transactions [SQL Server], SAVE TRANSACTION statement
- duplicate savepoints
ms.assetid: b953c3f1-f96d-42f1-95a2-30e314292b35
author: rothja
ms.author: jroth
ms.openlocfilehash: 46a6f7c08b540b6180326350a6e0aadb933a7ef5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121813"
---
# <a name="save-transaction-transact-sql"></a>SAVE TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  トランザクション内でセーブポイントを設定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

 ## <a name="syntax"></a>構文  
  
```  
  
SAVE { TRAN | TRANSACTION } { savepoint_name | @savepoint_variable }  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *savepoint_name*  
 セーブポイントに割り当てる名前を指定します。 セーブポイント名は識別子の規則に従う必要があります。文字数は半角 32 文字に制限されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで大文字と小文字が区別されない場合であっても、*savepoint_name* では常に大文字と小文字が区別されます。  
  
 @*savepoint_variable*  
 有効なセーブポイント名を含むユーザー定義の変数名を指定します。 変数は、**char**、**varchar**、**nchar**、または **nvarchar** データ型を使用して宣言する必要があります。 この変数には 32 文字を超える文字列も渡されますが、使用されるのは最初の 32 文字だけです。  
  
## <a name="remarks"></a>Remarks  
 ユーザーは、トランザクション内にセーブポイントというマーカーを設定できます。 セーブポイントでは、トランザクションの一部が条件付きで取り消された場合に、トランザクションが戻ることのできる位置を定義します。 トランザクションがセーブポイントまでロールバックされた場合は、必要であれば追加の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと、COMMIT TRANSACTION ステートメントを使用して、トランザクションを最後まで実行します。最後まで実行しない場合は、開始位置までロールバックしてトランザクション全体を取り消す必要があります。 トランザクション全体を取り消す場合は、ROLLBACK TRANSACTION *transaction_name* を使用します。 この場合、そのトランザクションのすべてのステートメントまたはプロシージャが取り消されます。  
  
 1 つのトランザクションでは同じセーブポイント名を重複して指定できますが、ROLLBACK TRANSACTION ステートメントでそのセーブポイント名を指定した場合は、そのセーブポイント名を使用している最新の SAVE TRANSACTION のみにロールバックできます。  
  
 BEGIN DISTRIBUTED TRANSACTION で明示的に起動された分散トランザクション、またはローカル トランザクションから拡大された分散トランザクションでは、SAVE TRANSACTION はサポートされません。  
  
> [!IMPORTANT]  
>  ROLLBACK TRANSACTION ステートメントで savepoint_name を指定している場合、そのセーブポイントより後の時点で取得されたロックは解放されます。ただし、エスカレーションおよび変換が行われた場合、 これらのロックは解放されず、前のロック モードに戻ることはありません。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ストアド プロシージャの実行前にアクティブなトランザクションが開始された場合に、トランザクション セーブポイントを使用して、ストアド プロシージャによる変更だけをロールバックする方法を示します。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
           WHERE name = N'SaveTranExample')  
    DROP PROCEDURE SaveTranExample;  
GO  
CREATE PROCEDURE SaveTranExample  
    @InputCandidateID INT  
AS  
    -- Detect whether the procedure was called  
    -- from an active transaction and save  
    -- that for later use.  
    -- In the procedure, @TranCounter = 0  
    -- means there was no active transaction  
    -- and the procedure started one.  
    -- @TranCounter > 0 means an active  
    -- transaction was started before the   
    -- procedure was called.  
    DECLARE @TranCounter INT;  
    SET @TranCounter = @@TRANCOUNT;  
    IF @TranCounter > 0  
        -- Procedure called when there is  
        -- an active transaction.  
        -- Create a savepoint to be able  
        -- to roll back only the work done  
        -- in the procedure if there is an  
        -- error.  
        SAVE TRANSACTION ProcedureSave;  
    ELSE  
        -- Procedure must start its own  
        -- transaction.  
        BEGIN TRANSACTION;  
    -- Modify database.  
    BEGIN TRY  
        DELETE HumanResources.JobCandidate  
            WHERE JobCandidateID = @InputCandidateID;  
        -- Get here if no errors; must commit  
        -- any transaction started in the  
        -- procedure, but not commit a transaction  
        -- started before the transaction was called.  
        IF @TranCounter = 0  
            -- @TranCounter = 0 means no transaction was  
            -- started before the procedure was called.  
            -- The procedure must commit the transaction  
            -- it started.  
            COMMIT TRANSACTION;  
    END TRY  
    BEGIN CATCH  
        -- An error occurred; must determine  
        -- which type of rollback will roll  
        -- back only the work done in the  
        -- procedure.  
        IF @TranCounter = 0  
            -- Transaction started in procedure.  
            -- Roll back complete transaction.  
            ROLLBACK TRANSACTION;  
        ELSE  
            -- Transaction started before procedure  
            -- called, do not roll back modifications  
            -- made before the procedure was called.  
            IF XACT_STATE() <> -1  
                -- If the transaction is still valid, just  
                -- roll back to the savepoint set at the  
                -- start of the stored procedure.  
                ROLLBACK TRANSACTION ProcedureSave;  
                -- If the transaction is uncommitable, a  
                -- rollback to the savepoint is not allowed  
                -- because the savepoint rollback writes to  
                -- the log. Just return to the caller, which  
                -- should roll back the outer transaction.  
  
        -- After the appropriate rollback, echo error  
        -- information to the caller.  
        DECLARE @ErrorMessage NVARCHAR(4000);  
        DECLARE @ErrorSeverity INT;  
        DECLARE @ErrorState INT;  
  
        SELECT @ErrorMessage = ERROR_MESSAGE();  
        SELECT @ErrorSeverity = ERROR_SEVERITY();  
        SELECT @ErrorState = ERROR_STATE();  
  
        RAISERROR (@ErrorMessage, -- Message text.  
                   @ErrorSeverity, -- Severity.  
                   @ErrorState -- State.  
                   );  
    END CATCH  
GO  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)  
  
  
