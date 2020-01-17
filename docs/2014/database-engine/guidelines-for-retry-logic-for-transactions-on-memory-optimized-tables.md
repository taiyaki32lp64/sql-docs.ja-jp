---
title: メモリ最適化テーブルでのトランザクションの再試行ロジックのガイドライン |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f719470419940b130967b7c1360c4ae0c281eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779216"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>メモリ最適化テーブルでのトランザクションの再試行ロジックのガイドライン
  メモリ最適化テーブルにアクセスするトランザクションに発生するエラー条件にはさまざまなものがあります。  
  
-   41302. 現在のトランザクションが、トランザクションが開始してから更新されたレコードを更新しようとしました。  
  
-   41305. 現在のトランザクションは、REPEATABLE READ の検証の失敗が原因でコミットされませんでした。  
  
-   41325. 現在のトランザクションは、SERIALIZABLE の検証の失敗が原因でコミットされませんでした。  
  
-   41301. 現在のトランザクションが依存している前のトランザクションが中止されたため、現在のトランザクションはコミットできません。  
  
 このようなエラーの原因としてよくあるのが、同時に実行されたトランザクションの間の競合です。 一般的な対処方法は、トランザクションを再試行するというものです。  
  
 これらのエラー条件の詳細については、競合の検出、検証、およびコミット依存関係の確認のセクションをご覧ください。[メモリ最適化テーブルでのトランザクション](../relational-databases/in-memory-oltp/memory-optimized-tables.md)です。  
  
 デッドロック (エラー コード 1205) は、メモリ最適化テーブルでは発生しません。 メモリ最適化テーブルではロックを使用しません。 ただし、アプリケーションに既にデッドロックに対する再試行ロジックが含まれている場合には、既存のロジックを拡張して新しいエラー コードを追加することもできます。  
  
## <a name="considerations-for-retrying"></a>再試行に関する注意点  
 アプリケーションでは通常、トランザクション間の競合が発生するため、その解決のために再試行ロジックを実装する必要があります。 発生する競合の数は、要因の数によって異なります。  
  
-   個々の行の競合。 競合の可能性は、同じ行の更新を試みるトランザクションの数が増えるにつれて増加します。  
  
-   REPEATABLE READ トランザクションによって読み取られる行の数。 読み取る行が増えるほど、その行のなかに同時実行トランザクションによって更新されるものがある可能性が高くなります。 このため、REPEATABLE READ 検証が失敗する原因になります。  
  
-   SERIALIZABLE トランザクションで使用されるスキャン範囲の大きさ。 スキャンの範囲が大きくなるほど、同時実行トランザクションによってファントム行が発生する可能性が高くなり、SERIALIZABLE 検証の失敗につながります。  
  
     アプリケーションでこのような競合が発生しないようにするのは難しいため、再試行ロジックが必要になります。  
  
> [!IMPORTANT]  
>  メモリ最適化テーブルにアクセスする読み取り/書き込みトランザクションでは、再試行ロジックが必要です。  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>読み取り専用トランザクションおよびネイティブ コンパイル ストアド プロシージャに関する注意点  
 ネイティブ コンパイル ストアド プロシージャを 1 回実行する読み取り専用トランザクションでは、REPEATABLE READ トランザクションおよび SERIALIZABLE トランザクションの検証は不要です。 トランザクションが読み取り専用であれば、書き込みの競合は発生しません。  
  
 ただし、依存関係のエラーは発生する可能性があります。 依存関係のエラーは、競合に起因するエラーよりも発生の可能性は低いです。 このため、ネイティブ コンパイル ストアド プロシージャを 1 回実行する読み取り専用トランザクションでは、多くの場合、特定の再試行ロジックは必要ありません。  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>読み取り専用トランザクションと複数コンテナーにまたがるトランザクションに関する注意点  
 読み取り専用で複数コンテナーにまたがるトランザクションは、ネイティブ コンパイル ストアド プロシージャのコンテキスト外で開始されるトランザクションであり、メモリ最適化テーブルがいずれも SNAPSHOT 分離下でアクセスされている場合には、検証を実行しません。 ただし、メモリ最適化テーブルが REPEATABLE READ または SERIALIZABLE 分離下でアクセスされている場合には、コミット時に検証が実行されます。 この場合、再試行ロジックが必要になることがあります。  
  
 詳細については、コンテナーにまたがるトランザクションでのセクションをご覧ください。[トランザクション分離レベル](../../2014/database-engine/transaction-isolation-levels.md)します。  
  
## <a name="implementing-retry-logic"></a>再試行ロジックの実装  
 メモリ最適化テーブルにアクセスするすべてのトランザクションと同様に、書き込みの競合 (エラー コード 41302) や依存関係の失敗 (エラー コード 41301) など、潜在的なエラーを処理するための再試行ロジックを検討する必要があります。 ほとんどのアプリケーションでは失敗率が低くなりますが、トランザクションの再試行によって問題に対処することが必要です。 再試行ロジックを実装する 2 つの方法をお勧めします。  
  
-   クライアント側の再試行。 クライアント側の再試行は、一般的な事例で再試行ロジックを実装する方法としてお勧めします。 クライアント アプリケーションは、トランザクションによってスローされたエラーをキャッチし、トランザクションを再試行します。 既存のクライアント アプリケーションにデッドロックを処理する再試行ロジックがある場合は、新しいエラー コードを処理するようにアプリケーションを拡張できます。  
  
-   ラッパー ストアド プロシージャの使用。 クライアントは、ネイティブ コンパイル ストアド プロシージャを呼び出すかトランザクションを実行する、解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] ストアド プロシージャを呼び出します。 その後、ラッパー プロシージャは、try/catch ロジックを使用し、エラーをキャッチして必要に応じてプロシージャ呼び出しを再試行します。 障害発生前に結果がクライアントに返され、クライアントがその結果を破棄する方法がわからない可能性があります。 したがって、念のため、クライアントに結果セットを返さないネイティブ コンパイル ストアド プロシージャのみでこのメソッドを使用することをお勧めします。  
  
 再試行ロジックは、[!INCLUDE[tsql](../includes/tsql-md.md)] と中間層のアプリケーション コードのいずれかに実装できます。  
  
 再試行ロジックを検討する理由には次の 2 つがあります。  
  
-   クライアント アプリケーションには他のエラー コード (1205 など) についての再試行ロジックがあり、拡張することができるため。  
  
-   競合が発生するのはまれであり、準備実行によってエンド ツー エンドの待機時間を減らすことが重要であるため。 ネイティブの実行の詳細については、ストアド プロシージャを直接コンパイルを参照してください。 [Natively Compiled Stored Procedures](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)します。  
  
 次のサンプルでは、ネイティブ コンパイル ストアド プロシージャまたは複数コンテナーにまたがるトランザクションへの呼び出しが含まれている [!INCLUDE[tsql](../includes/tsql-md.md)] の解釈されたストアド プロシージャの再試行ロジックを示します。  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルに対するトランザクションの概要](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [メモリ最適化テーブルでのトランザクション](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [メモリ最適化テーブルのトランザクション分離レベルに関するガイドライン](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
