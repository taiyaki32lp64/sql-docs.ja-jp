---
title: トランザクション (SQL データ ウェアハウス) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 21e6d25305bd6abf4a3dc4555f2148a2fe385187
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121587"
---
# <a name="transactions-sql-data-warehouse"></a>トランザクション (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  トランザクションは、完全にコミットされた、または完全にロールバックされた 1 つ以上のデータベース ステートメントのグループです。 各トランザクションには、原子性、一貫性、分離性、持続性 (ACID) があります。 トランザクションが成功すると、その中のすべてのステートメントがコミットされます。 トランザクションが失敗した場合、つまりグループ内の少なくとも 1 つのステートメントが失敗した場合は、グループ全体がロールバックされます。  
  
 トランザクションの開始と終了は、AUTOCOMMIT 設定と BEGIN TRANSACTION、COMMIT、および ROLLBACK ステートメントによって変わります。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] では、次の種類のトランザクションがサポートされています。  
  
-   BEGIN TRANSACTION ステートメントで始まり、COMMIT または ROLLBACK ステートメントで終了する、*明示的なトランザクション*。  
  
-   セッション内で自動的に開始して、BEGIN TRANSACTION ステートメントでは開始されない、*自動コミット トランザクション*。 AUTOCOMMIT 設定が ON の場合、各ステートメントはトランザクション内で実行され、明示的な COMMIT または ROLLBACK は必要ありません。 AUTOCOMMIT 設定が OFF の場合は、トランザクションの結果を決定するために COMMIT または ROLLBACK ステートメントが必要です。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] では、自動コミット トランザクションは、COMMIT または ROLLBACK ステートメントのすぐ後、または SET OFF ステートメントの後に開始します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>引数  
 BEGIN TRANSACTION  
 明示的トランザクションの開始点をマークします。  
  
 COMMIT [ WORK ]  
 明示的なトランザクションまたはオートコミット トランザクションの終了をマークします。 このステートメントによって、トランザクション内の変更がデータベースに完全にコミットされます。 ステートメント COMMIT は、COMMIT WORK、COMMIT TRAN、および COMMIT TRANSACTION と同じです。  
  
 ROLLBACK [ WORK ]  
 トランザクションをトランザクションの先頭にロールバックします。 トランザクションに対する変更はデータベースにコミットされません。 ステートメント ROLLBACK は、ROLLBACK WORK、ROLLBACK TRAN、および ROLLBACK TRANSACTION と同じです。  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 トランザクションの開始方法と終了方法を決定します。  
  
 ON  
 各ステートメントは独自のトランザクションで実行され、明示的な COMMIT ステートメントまたは ROLLBACK ステートメントは必要ありません。 AUTOCOMMIT が ON の場合、明示的なトランザクションが許可されます。  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] は、トランザクションがまだ開始されていない場合、自動的にトランザクションを開始します。 後続のステートメントはトランザクションの一部として実行され、トランザクションの結果を決定するには COMMIT または ROLLBACK が必要です。 この操作モードでトランザクションがコミットまたはロールバックするとすぐに、モードは OFF のまま、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] によって新しいトランザクションを開始されます。 AUTOCOMMIT が OFF の場合、明示的なトランザクションは許可されません。  
  
 アクティブなトランザクション内で AUTOCOMMIT 設定を変更した場合、その設定は現在のトランザクションに影響し、トランザクションが完了するまで有効になりません。  
  
 AUTOCOMMIT が ON の場合、SET AUTOCOMMIT ON ステートメントをもう 1 回実行しても効果はありません。 同様に、AUTOCOMMIT が OFF の場合、SET AUTOCOMMIT OFF をもう 1 回実行しても効果はありません。  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 これで、SET AUTOCOMMIT と同じモードが切り替わります。 ON の場合、SET IMPLICIT_TRANSACTIONS によって接続は暗黙のトランザクション モードに設定されます。 OFF の場合、接続はオートコミット モードに戻ります。  詳細については、「[SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 トランザクション関連のステートメントを実行するために特別なアクセス許可は必要ありません。 トランザクション内でステートメントを実行するにはアクセス許可が必要です。  
  
## <a name="error-handling"></a>エラー処理  
 COMMIT または ROLLBACK が実行され、アクティブなトランザクションがない場合は、エラーが発生します。  
  
 トランザクションが既に進行中のときに BEGIN TRANSACTION が実行されると、エラーが発生します。 これが発生する可能性があるのは、BEGIN TRANSACTION ステートメントが正常に実行された後、または SET AUTOCOMMIT OFF の状態で実行されているセッションの場合です。  
  
 ステートメントの実行時エラー以外のエラーによりトランザクションを正常に完了できない場合、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] によってトランザクションが自動的にロールバックされ、そのトランザクションで保持されていたすべてのリソースが解放されます。 たとえば、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] のインスタンスへのクライアントのネットワーク接続が切断された場合、またはクライアントがアプリケーションからログオフした場合、ネットワークからインスタンスにこの切断が通知されると、その接続に対する未処理のトランザクションがすべてロールバックされます。  
  
 バッチでステートメントの実行時エラーが発生した場合、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] は **ON** に設定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT** と一致する動作をし、トランザクション全体がロールバックされます。 **XACT_ABORT** 設定の詳細については、「[SET XACT_ABORT (Transact-SQL)](https://msdn.microsoft.com/library/ms188792.aspx)」を参照してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 セッションで実行できるトランザクション数は一度に 1 つのみです。セーブ ポイントと入れ子になったトランザクションはサポートされません。  
  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] のプログラマは、トランザクションで参照されるすべてのデータが論理的に正しいことを確認したうえで COMMIT を実行する必要があります。  
  
 トランザクションが完了する前にセッションが終了すると、トランザクションはロールバックされます。  
  
 トランザクション モードはセッション レベルで管理されます。 たとえば、あるセッションで明示的なトランザクションが開始された場合、または AUTOCOMMIT が OFF に設定された場合、または IMPLICIT_TRANSACTIONS が ON に設定された場合、他のセッションのトランザクション モードには影響しません。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 COMMIT ステートメントを発行した後は、データの変更がデータベースの永続的な部分になるので、トランザクションをロールバックできなくなります。  
  
 [CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) コマンドと [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) コマンドは、明示的なトランザクション内で使用することはできません。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] にはトランザクションの共有メカニズムはありません。 これは、ある時点で、システム内のどのトランザクションでも、作業を実行できるのは 1 つのセッションのみであることを示します。  
  
## <a name="locking-behavior"></a>ロック動作  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] では、複数のユーザーが同時にアクセスしたときにトランザクションの整合性を保証し、データベースの一貫性を保つため、ロックを使用します。 ロックは、暗黙的および明示的なトランザクションで使用されます。 各トランザクションでは、トランザクションが依存するテーブルやデータベースなど、リソースに対してさまざまな種類のロックが要求されます。 すべての [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ロックはテーブル レベル以上です。 ロックをかけると、ロックを要求したトランザクションにとって問題になるようなリソースの変更が行われないように、他のトランザクションがブロックされます。 各トランザクションでは、ロックされたリソースに依存関係がなくなると、ロックが解除されます。明示的なトランザクションでは、コミット時またはロールバック時にトランザクションが完了するまでロックが保持されます。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. 明示的なトランザクションを使用します。  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. トランザクションのロールバック  
 次の例では、トランザクションのロールバックの効果を示します。  この例で ROLLBACK ステートメントがロールバックされます、INSERT ステートメントでは、作成されたテーブルはそのまま残ります。  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. AUTOCOMMIT の設定  
 次の例では、自動コミット設定を `ON` に設定します。  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 次の例では、自動コミット設定を `OFF` に設定します。  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. 複数ステートメントの暗黙のトランザクションの使用  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>参照  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
