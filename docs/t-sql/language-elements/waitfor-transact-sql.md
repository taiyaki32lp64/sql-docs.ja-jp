---
title: WAITFOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WAITFOR
- WAITFOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TIME option
- delaying executions [SQL Server]
- batches [SQL Server], execution times
- stored procedures [SQL Server], executing
- DELAY
- time [SQL Server], execution delays
- blocking executions
- transactions [SQL Server], execution times
- WAITFOR statement
- timing executions
ms.assetid: 8e896e73-af27-4cae-a725-7a156733f3bd
author: rothja
ms.author: jroth
ms.openlocfilehash: ea7697294cd25412d4ac78c92f3b1bf689f1ff34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086111"
---
# <a name="waitfor-transact-sql"></a>WAITFOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定された時間または期間が経過するか、指定されたステートメントによって少なくとも 1 つの行が変更または返されるまで、バッチ、ストアド プロシージャ、またはトランザクションの実行をブロックします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
WAITFOR   
{  
    DELAY 'time_to_pass'   
  | TIME 'time_to_execute'   
  | [ ( receive_statement ) | ( get_conversation_group_statement ) ]   
    [ , TIMEOUT timeout ]  
}  
```  
  
## <a name="arguments"></a>引数  
 DELAY  
 バッチ、ストアド プロシージャ、またはトランザクションを実行する前に経過する必要のある、最大 24 時間までの指定された時間です。  
  
 '*time_to_pass*'  
 待機する時間の長さです。 *time_to_pass* は、**datetime** データ形式で、またはローカル変数として、指定できます。 日付を指定することはできないため、**datetime** 値の日付の部分は許可されません。 *time_to_pass* は、hh:mm[[:ss].mss] として書式設定されます。
  
 TIME  
 バッチ、ストアド プロシージャ、またはトランザクションを実行するように指定された時間です。  
  
 '*time_to_execute*'  
 WAITFOR ステートメントが終了する時間です。 *time_to_execute* は、**datetime** データ形式で、またはローカル変数として指定できます。 日付を指定することはできないため、**datetime** 値の日付の部分は許可されません。 *time_to_execute* は hh:mm[[:ss].mss] で書式設定され、必要に応じて、1900-01-01 の日付を含めることができます。
  
 *receive_statement*  
 有効な RECEIVE ステートメントです。  
  
> [!IMPORTANT]  
>  *receive_statement* が指定された WAITFOR は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージに対してのみ適用できます。 詳細については、「[RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)」を参照してください。  
  
 *get_conversation_group_statement*  
 有効な GET CONVERSATION GROUP ステートメントです。  
  
> [!IMPORTANT]  
>  *get_conversation_group_statement* が指定された WAITFOR は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージに対してのみ適用できます。 詳細については、「[GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)」を参照してください。  
  
 TIMEOUT *timeout*  
 キューでメッセージの到着を待機する時間を、ミリ秒単位で指定します。  
  
> [!IMPORTANT]  
>  TIMEOUT が指定された WAITFOR は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージに対してのみ適用できます。 詳細については、「[RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)」と「[GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 WAITFOR ステートメントを実行している間は、トランザクションが実行され、その他のリクエストは同じトランザクションの下で実行することはできません。  
  
 実際の遅延時間は *time_to_pass*、*time_to_execute* または *timeout* で指定される時間によって異なり、サーバーの利用状況レベルにも依存します。 時間のカウンターは、WAITFOR ステートメント スレッドがスケジュールされた時点から開始します。 サーバーがビジーの場合、スレッドはすぐにスケジュールされない場合があるので、遅延時間は指定した時間よりも長くなることがあります。  
  
 WAITFOR はクエリのセマンティクスを変更しません。 クエリが行を返すことができない場合、WAITFOR は待機状態のままか、TIMEOUT が指定されている場合は TIMEOUT に達するまで待機します。  
  
 WAITFOR ステートメントでは、カーソルをオープンすることはできません。  
  
 WAITFOR ステートメントでは、ビューを定義することはできません。  
  
 クエリが query wait オプションの値を超えると、WAITFOR ステートメントの引数を実行せずに完了できます。 構成オプションの詳細については、「[query wait サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)」を参照してください。 アクティブな待機中の処理を表示するには、[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) を使用します。  
  
 各 WAITFOR ステートメントには、それに関連付けられたスレッドがあります。 同じサーバーに多くの WAITFOR ステートメントが指定されている場合、これらのステートメントの実行を待機することを中止できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、WAITFOR ステートメント スレッドの数が監視され、サーバーでスレッドが不足し始めると、これらのスレッドの一部がランダムに選択されて終了されます。  
  
 WAITFOR ステートメントによってアクセスされている行セットの変更を禁止するロックも保持しているトランザクション内で、WAITFOR を含むクエリを実行すると、デッドロックが発生する可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、これらのシナリオを識別し、このようなデッドロックの機会が存在する場合は、空の結果セットを返します。  
  
> [!CAUTION]  
>  WAITFOR を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスの完了が遅くなり、その結果、アプリケーションでタイムアウト メッセージが表示される可能性があります。 必要に応じて、アプリケーション レベルで接続のタイムアウト設定を調整してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-waitfor-time"></a>A. WAITFOR TIME を使用する  
 次の例では、午後 10 時 20 分に msdb データベースでストアド プロシージャ `sp_update_job` を実行します。 (`22:20`)。  
  
```  
EXECUTE sp_add_job @job_name = 'TestJob';  
BEGIN  
    WAITFOR TIME '22:20';  
    EXECUTE sp_update_job @job_name = 'TestJob',  
        @new_name = 'UpdatedJob';  
END;  
GO  
```  
  
### <a name="b-using-waitfor-delay"></a>B. WAITFOR DELAY を使用する  
 次の例では、ストアド プロシージャを 2 時間遅延して実行します。  
  
```  
BEGIN  
    WAITFOR DELAY '02:00';  
    EXECUTE sp_helpdb;  
END;  
GO  
```  
  
### <a name="c-using-waitfor-delay-with-a-local-variable"></a>C. ローカル変数と共に WAITFOR DELAY を使用する  
 次の例では、`WAITFOR DELAY` オプションでローカル変数を使用する方法を示します。 このストアド プロシージャは、可変の時間だけ待機してから、経過した時間数、分数、秒数に関する情報をユーザーに返します。  
  
```  
IF OBJECT_ID('dbo.TimeDelay_hh_mm_ss','P') IS NOT NULL  
    DROP PROCEDURE dbo.TimeDelay_hh_mm_ss;  
GO  
CREATE PROCEDURE dbo.TimeDelay_hh_mm_ss   
    (  
    @DelayLength char(8)= '00:00:00'  
    )  
AS  
DECLARE @ReturnInfo varchar(255)  
IF ISDATE('2000-01-01 ' + @DelayLength + '.000') = 0  
    BEGIN  
        SELECT @ReturnInfo = 'Invalid time ' + @DelayLength   
        + ',hh:mm:ss, submitted.';  
        -- This PRINT statement is for testing, not use in production.  
        PRINT @ReturnInfo   
        RETURN(1)  
    END  
BEGIN  
    WAITFOR DELAY @DelayLength  
    SELECT @ReturnInfo = 'A total time of ' + @DelayLength + ',   
        hh:mm:ss, has elapsed! Your time is up.'  
    -- This PRINT statement is for testing, not use in production.  
    PRINT @ReturnInfo;  
END;  
GO  
/* This statement executes the dbo.TimeDelay_hh_mm_ss procedure. */  
EXEC TimeDelay_hh_mm_ss '00:00:10';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `A total time of 00:00:10, in hh:mm:ss, has elapsed. Your time is up.`  
  
## <a name="see-also"></a>参照  
 [フロー制御言語 &#40;TRANSACT-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
