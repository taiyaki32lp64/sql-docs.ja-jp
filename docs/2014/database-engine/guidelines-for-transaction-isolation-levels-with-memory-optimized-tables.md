---
title: メモリ最適化テーブルでのトランザクション分離レベルのガイドライン |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26f0193d40a01858bc3fe651a23b389a4ffcb6ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779157"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>メモリ最適化テーブルのトランザクション分離レベルに関するガイドライン
  多くのシナリオでは、トランザクション分離レベルを指定する必要があります。 メモリ最適化テーブルのトランザクション分離は、ディスク ベース テーブルとは異なります。  
  
 トランザクション分離レベルを指定するために必要な条件は次のとおりです。  
  
-   トランザクション分離レベルは、ネイティブ コンパイル ストアド プロシージャの中身を構成する ATOMIC ブロックに必要なオプションです。  
  
-   複数のコンテナーにまたがるトランザクションで分離レベルを使用することには制約があるため、解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] でメモリ最適化テーブルを使用する場合には、そのテーブルへのアクセスに使用する分離レベルを指定するテーブル ヒントを併用するのが一般的です。 分離レベル ヒントとコンテナーにまたがるトランザクションの詳細については、次を参照してください。[トランザクション分離レベル](../../2014/database-engine/transaction-isolation-levels.md)します。  
  
-   必要なトランザクション分離レベルは、明示的に宣言する必要があります。 ロック ヒント (XLOCK など) を使用してトランザクションの特定の行またはテーブルの分離を保証することはできません。  
  
-   データベースにアクセスするアプリケーションでは、決定的なトランザクションの失敗を引き起こす競合、検証の失敗、およびコミット依存関係の失敗に起因するエラーを処理するための再試行ロジックを実装する必要があります。 コミット依存関係の失敗は、読み取り専用トランザクションでも発生する可能性があります。  
  
-   実行時間の長いトランザクションは、メモリ最適化テーブルでは避ける必要があります。 このようなトランザクションによって、競合とその後のトランザクション終了の可能性が高まります。 実行時間が長いトランザクションは、ガベージ コレクションが遅延する原因にもなります。 トランザクションの実行時間が長くなるほど、最近削除された行のバージョンがインメモリ OLTP で保持される時間も長くなります。これにより、新しいトランザクションの参照パフォーマンスが低下する場合があります。  
  
 ディスク ベース テーブルでは通常、トランザクションの分離にロックおよびブロックを使用しています。 メモリ最適化テーブルでは、複数バージョン管理および競合検出を使用して分離を確実なものにしています。 詳細についてには、競合の検出、検証、およびコミット依存関係の確認に関するセクションを参照[メモリ最適化テーブルでのトランザクション](../relational-databases/in-memory-oltp/memory-optimized-tables.md)です。  
  
 ディスク ベース テーブルでは、SNAPSHOT および READ_COMMITTED_SNAPSHOT の 2 つの分離レベルによる複数バージョン管理が可能です。 メモリ最適化テーブルでは、REPEATABLE READ と SERIALIZABLE も含め、すべての分離レベルが複数バージョン ベースになっています。  
  
## <a name="types-of-transactions"></a>トランザクションの種類  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリはいずれも、トランザクションのコンテキストで実行されます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のトランザクションの種類は、3 つに分けることができます。  
  
-   自動コミット トランザクション。 アクティブなトランザクション コンテキストがなく、暗黙のトランザクションがセッションで ON に設定されていない場合には、各クエリに独自のトランザクション コンテキストがあります。 トランザクションは、ステートメントの実行が開始されると開始となり、ステートメントが終了すると終了します。  
  
-   明示的なトランザクション。 ユーザーは、明示的に BEGIN TRAN または BEGIN ATOMIC を使用してトランザクションを開始します。 トランザクションは、対応する COMMIT および ROLLBACK、または (ATOMIC ブロックの場合には) END によって完了します。  
  
-   暗黙のトランザクション。 IMPLICIT_TRANSACTIONS オプションが ON に設定されていると、ユーザーがステートメントを実行し、アクティブなトランザクション コンテキストが存在しない場合にはいつでも、暗黙的にトランザクションが開始されます。 この種のトランザクションは、明示的に COMMIT および ROLLBACK を使用することによって完了します。  
  
## <a name="baseline-read-committed-isolation"></a>ベースラインとしての READ COMMITTED 分離  
 READ COMMITTED は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定の分離レベルです。  
  
 分離レベル READ COMMITTED は、トランザクションが、現在のトランザクションの外部で実行された変更に起因する、コミットされていないデータを認識しないことを保証します。 つまり、トランザクションは、データベースにコミットされたデータ、または現在のトランザクションによって変更されたデータだけを読み取ります。  
  
 メモリ最適化テーブルでサポートされる分離レベルは、すべて READ COMMITTED が保証されています。 このため、トランザクションによってさらに厳密な保証が求められるのでなければ、メモリ最適化テーブルでサポートされる分離レベルのどれを使用してもかまいません。 SNAPSHOT では、使用するシステム リソースが分離レベルのうち最も少なくなっています。  
  
 SNAPSHOT 分離レベル (メモリ最適化テーブルでサポートされる分離レベルのうち、最も低いレベル) による保証には、READ COMMITTED の保証が含まれています。 トランザクションの各ステートメントでは、同一で一貫性のあるバージョンのデータベースを読み取ります。 トランザクションによって読み取られる行がいずれもデータベースにコミットされるだけでなく、すべての読み取り操作で同じトランザクションによって変更が実行されます。  
  
 **ガイドライン**:READ COMMITTED 分離の保証が必要な場合にのみ使用してスナップショット分離では、ネイティブ コンパイル ストアド プロシージャとによって、メモリ最適化テーブルにアクセスするための解釈[!INCLUDE[tsql](../includes/tsql-md.md)]します。  
  
 自動コミット トランザクションでは、分離レベル READ COMMITTED が暗黙的にメモリ最適化テーブルの SNAPSHOT にマッピングされています。 このため、TRANSACTION ISOLATION LEVEL セッションの設定が READ COMMITTED に設定されている場合には、メモリ最適化テーブルにアクセスするときにテーブル ヒントを使用して分離レベルを指定する必要はありません。  
  
 以下の自動コミット トランザクションの例では、アドホック バッチの一環としてメモリ最適化テーブル Customers と通常のテーブル [Order History] の間の結合を表示しています。  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 以下の明示的トランザクションまたは暗黙的トランザクションの例でも同じ結合を示していますが、今回は明示的なユーザー トランザクションを使用しています。 テーブル ヒント WITH (SNAPSHOT) で示すように、メモリ最適化テーブル Customers が SNAPSHOT 分離レベルでアクセスされています。これに対して、通常のテーブル [Order History] は、READ COMMITTED 分離レベルでアクセスされています。  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>動作の違い  
 ディスク ベース テーブルを使用するアプリケーションが使用している主な実装は、READ COMMITTED 保証のほかに 2 つあります。 READ COMMITTED 分離を使用してアクセスするディスク ベース テーブルを SNAPSHOT 分離を使用してアクセスするメモリ最適化テーブルに変換するときには、以下の 2 点に注意が必要です。  
  
-   ディスク ベース テーブルに READ COMMITTED 分離レベルを実装した場合 (READ_COMMITTED_SNAPSHOT はオフと想定) には、読み取りと書き込みの間の競合を防ぐためにロックを使用します。 書き込み側が行の更新を開始するときに、ロックを取得します。トランザクションがコミットされるまで、このロックは解放されません。 読み取り操作はすべてブロックされ、書き込みトランザクションがコミットされるまで待機することになります。  
  
     一部のアプリケーションでは、書き込み側がコミットするまでの間、読み取り側が常に待機することが想定されています。特に、アプリケーション層で 2 つのトランザクションを同期させる場合です。  
  
     **ガイドライン:** アプリケーションは、ブロックの動作に依存できません。 アプリケーションでは、同時実行トランザクション間の同期を必要とする場合このようなロジックまたは実装できますアプリケーション層で、データベース層を介して[sp_getapplock &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql)します。  
  
-   READ COMMITTED 分離を使用するトランザクションでは、各ステートメントでデータベースの行の最新のバージョンが使用されます。 このため、以降のステートメントでは、データベースの状態が変化することになります。  
  
     新しい行が見つかるまで WHILE ループを使用してテーブルをポーリングする方法は、この前提を使用するアプリケーション パターンの一例です。 ループの各反復処理で、クエリにデータベースの最新の更新が適用されます。  
  
     **ガイドライン:** をアプリケーションがテーブルに書き込まれた最新の行を取得するメモリ最適化テーブルをポーリングする必要がある場合は、トランザクションのスコープ外ポーリング ループを移動します。  
  
     以下は、この前提を使用するアプリケーション パターンの一例です。 WHILE ループを使用して、新しい行が見つかるまでテーブルをポーリングしています。 ループの各反復処理で、クエリがデータベースの最新の更新にアクセスします。  
  
 次の例のスクリプトでは、行を取得するまでテーブル t1 をポーリングしています。 その後で、テーブルから行を 1 つ削除してさらに処理を実行します。  
  
 ポーリングのロジックはテーブル t1 にアクセスするうえで SNAPSHOT 分離を使用しているため、トランザクションの範囲外に置く必要があることに注意してください。 トランザクションの範囲内でポーリング ロジックを使用すると、トランザクションの実行時間が長くなり、好ましくありません。  
  
```sql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>ロックに関するテーブル ヒント  
 ロック ヒント ([テーブル ヒント&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)) など、HOLDLOCK および XLOCK で使えるディスク ベース テーブルが[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]分離レベルを指定するために必要な多くのロックを取得します。  
  
 メモリ最適化テーブルではロックは使用しません。 REPEATABLE READ や SERIALIZABLE など、高度な分離レベルを使用して必要な保証を宣言できます。  
  
 ロック ヒントはサポートされていません。 代わりに、トランザクション分離レベルを使用して必要な保証を宣言します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではメモリ最適化テーブルにロックを使用しないため、NOLOCK がサポートされます。 ディスク ベース テーブルとは異なり、NOLOCK は、メモリ最適化テーブルに対する READ UNCOMMITTED 動作を示すわけではないことに注意してください。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルに対するトランザクションの概要](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [メモリ最適化テーブルでのトランザクションの再試行ロジックをするためのガイドライン](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [トランザクション分離レベル](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
