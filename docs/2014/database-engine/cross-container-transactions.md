---
title: コンテナーにまたがるトランザクション |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290aff0bfcb01e098ae87b48cf582cdf999314c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807426"
---
# <a name="cross-container-transactions"></a>複数コンテナーにまたがるトランザクション
  複数コンテナーにまたがるトランザクションは、ネイティブ コンパイル ストアド プロシージャの呼び出しまたはメモリ最適化テーブルでの操作を含む、暗黙的または明示的なユーザー トランザクションです。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、ストアド プロシージャの呼び出しでトランザクションが開始されることはありません。 ネイティブ コンパイル プロシージャの (ユーザー トランザクションのコンテキストではなく) 自動コミット モードでの実行は、複数コンテナーにまたがるトランザクションとは見なされません。  
  
 メモリ最適化テーブルを参照する解釈されたクエリは、明示的または暗黙的なトランザクションから実行された場合も、自動コミット モードで実行された場合も、複数コンテナーにまたがるトランザクションの一部と見なされます。  
  
##  <a name="isolation"></a> 個々 の操作の分離  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各トランザクションには分離レベルがあります。 既定の分離レベルは READ COMMITTED です。 別の分離レベルを使用する分離レベルを使用して、設定できます[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)します。  
  
 多くの場合、ディスク ベース テーブルでの操作とは異なる分離レベルで、メモリ最適化テーブルでの操作を実行することが必要になります。 トランザクションでは、ステートメントのコレクションまたは個別の読み取り操作に対して別の分離レベルを設定することができます。  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>個別の操作の分離レベルの指定  
 トランザクションの一連のステートメントに対して別の分離レベルを設定するには、`SET TRANSACTION ISOLATION LEVEL` を使用します。 トランザクションの次の例では既定で SERIALIZABLE 分離レベルを使用します。 t3、t2、および t1 に対する挿入操作や選択操作は、REPEATABLE READ 分離レベルで実行されます。  
  
```sql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 トランザクションの既定値と異なる個別の読み取り操作の分離レベルを設定するには、テーブル ヒント (SERIALIZABLE など) を使用します。 行の更新や削除を可能にするには、その行を読み取っておくことが常に必要であるため、すべての選択は読み取り操作に相当し、すべての更新やすべての削除は読み取りに相当します。 書き込みは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では常に分離されるため、挿入操作には分離レベルはありません。 次の例では、トランザクションの既定の分離レベルは READ COMMITTED ですが、テーブル t1 には SERIALIZABLE 分離で、テーブル t2 には SNAPSHOT 分離でアクセスします。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>個別の操作の分離セマンティクス  
 シリアル化可能なトランザクション T は完全に分離して実行されます。 他のすべてのトランザクションは、T の開始前にコミット済みであるか、T のコミット後に開始されるかのように見えます。 トランザクション内の別の操作に別の分離レベルがある場合は、さらに複雑になります。  
  
 トランザクション分離レベルでの一般的なセマンティクス[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、ロックの影響、と共にについては[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)します。  
  
 異なる操作に異なる分離レベルがある複数コンテナーにまたがるトランザクションの場合は、個別の読み取り操作の分離のセマンティクスを理解しておく必要があります。 書き込み操作は常に分離されます。 それぞれ異なるトランザクションでの書き込みが互いに影響し合うことはできません。  
  
 データの読み取り操作では、フィルター条件を満たす行の数が返されます。  
  
 読み取り操作のトランザクション t です。 分離レベルの一部は、以下の観点認識できるように読み取りは実行されます。  
  
 コミットの状態  
 コミットの状態では、読み取られたデータのコミットが保証されるかどうかを参照します。  
  
 (トランザクションの) 一貫性  
 一連の読み取りに関するトランザクションの一貫性では、読み取られた行バージョンがすべて正確な同じ一連のトランザクションからの更新を含んでいることが保証されるかどうかを参照します。  
  
 安定性では、読み取られたデータについてシステムからトランザクション T への提供が保証されます。  
 安定性は、トランザクションの読み取りが反復可能かどうかを参照します。 したがって、読み取りが反復された場合、同じ行や行バージョンが返されるかということになります。  
  
 特定の保証では、トランザクションの論理的な終了時刻を参照します。 一般に、論理的な終了時刻は、トランザクションがデータベースにコミットされる時間です。 メモリ最適化テーブルにトランザクションからアクセスする場合、論理的な終了時刻は、理論的には検証フェーズの開始時です (詳細については、トランザクション有効期間の説明を参照してください。[メモリ最適化テーブルでのトランザクション](../relational-databases/in-memory-oltp/memory-optimized-tables.md)です。  
  
 分離レベルに関係なく、トランザクション (T) は常に自己の更新を確認します。  
  
 READ UNCOMMITTED  
 読み取られるデータが、コミット済み、一貫した状態、または安定状態のいずれでもありません。 ただし、これには T によって実行された前の書き込み操作が含まれます。  
  
 READ COMMITTED  
 読み取られるデータはコミットされます。  
  
 SNAPSHOT  
 SNAPSHOT 分離で T によって実行されたすべての読み取り操作には、同じ論理的読み取り時刻があります。それは、トランザクションの開始時です。 読み取られるデータは、コミットされること、および論理的読み取りの時点で一貫性があることが保証されます。 元の読み取りの時点で読み取りを繰り返しても、同じ結果を返すことが保証されます。  
  
 REPEATABLE READ  
 読み取られるデータは、コミットされること、およびトランザクションの論理的終了時刻まで安定状態であることが保証されます。  
  
 SERIALIZABLE  
 REPEATABLE READ とファントムの回避と T. ファントムの回避の意味、スキャン操作が、T によって書き込まれた追加の行を返すことができますのみで実行されるすべてのシリアル化可能な読み取り操作に関して、トランザクションの一貫性の保証がすべてがありません他のトランザクションによって書き込まれた行。  
  
 次のようなトランザクションがあるとします。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 このトランザクションでは、READ COMMITTED 分離で t3 からすべての行を削除し、SERIALIZABLE 分離で t1 からすべての行を t3 にコピーして、t1 と t3 を比較します。 テーブルが空にされたので、一部の行 [t1 の行以外] が t3 に追加されている可能性があります。 コピーは SERIALIZABLE であったので、t1 には行は追加されていません。  
  
 トランザクションの終了時の t1 からの読み取りは構文的に READ COMMITTED で行われますが、同じ読み取りが SERIALIZABLE のトランザクションで前に実行されているので、この読み取りは効果的にシリアル化可能です。シリアル化可能性により、トランザクションの後続のどの時点で読み取りを実行しても、同じ行を返すことが保証されます。  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>複数コンテナーにまたがるトランザクションと分離レベル  
 コンテナーにまたがるトランザクションは 2 つの辺を持つものとして見なすことができます。 (ディスク ベース テーブルに対する操作) のディスク ベース側と、メモリ最適化側 (メモリ最適化テーブルでの操作) にします。 これら 2 つの側で分離レベルが異なる場合があります。 実際に、それぞれの側での個々の読み取り操作で分離レベルが異なることがあります。  
  
 特定のトランザクション T のディスク ベース側は、次の条件のいずれかに一致する場合、特定の分離レベル X に達します。  
  
-   X で開始します。つまり、セッションの既定値が X、いずれかを実行するため`SET TRANSACTION ISOLATION LEVEL`、または、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]既定。  
  
-   トランザクションの実行中に、`SET TRANSACTION ISOLATION LEVEL` を使用して、既定の分離レベルが X に変更されます。  
  
-   ディスク ベース テーブルに対する読み取り操作が、構文 `WITH (X)` を使用して、分離レベル X で実行されます。  
  
 T の実行中に、メモリ最適化テーブルに対する任意の読み取り操作、または任意のネイティブ コンパイル ストアド プロシージャが分離レベル Y で実行された場合、T のメモリ最適化側は分離レベル Y に達します。  
  
 次のトランザクションを例として考えてみましょう。 ここで、t1 と t2 はディスク ベース テーブル、t3 と t4 はメモリ最適化テーブルです。  
  
 トランザクションのディスク ベース側は READ COMMITTED 分離レベルに達します。これは、開始時のレベルが READ COMMITTED であるためです。 また、ディスク ベース側は REPEATABLE READ にも達します。これは、最初の読み取り操作が REPEATABLE READ で実行されるためです。 トランザクションの終了時の削除は READ COMMITTED 分離レベルで実行され、新しい分離レベルの導入はありません。  
  
 トランザクションのメモリ最適化側で、2 つのレベルのいずれかに達することができます: condition1 が true の場合は serializable に達し、false の場合、メモリ最適化側到達だけでスナップショット分離中にします。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>複数コンテナーにまたがるトランザクションでサポートされる分離レベル  
 複数コンテナーにまたがるトランザクションでは、メモリ最適化テーブルでの操作に使用される分離レベルに制限があります。  
  
 メモリ最適化テーブルは、SNAPSHOT、REPEATABLE READ、および SERIALIZABLE の各分離レベルをサポートします。 自動コミット トランザクションの場合、メモリ最適化テーブルは READ COMMITTED 分離レベルをサポートします。  
  
 次のシナリオがサポートされます。  
  
-   READ UNCOMMITTED、READ COMMITTED、および READ_COMMITTED_SNAPSHOT の複数コンテナーにまたがるトランザクションは、SNAPSHOT、REPEATABLE READ、および SERIALIZABLE の各分離でメモリ最適化テーブルにアクセスできます。 READ COMMITTED の保証はトランザクションに対して保持されます。トランザクションで読み取られたすべての行がデータベースにコミットされています。  
  
-   REPEATABLE READ および SERIALIZABLE のトランザクションは、SNAPSHOT 分離でメモリ最適化テーブルにアクセスできます。  
  
## <a name="read-only-cross-container-transactions"></a>読み取り専用の複数コンテナーにまたがるトランザクション  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のほとんどの読み取り専用トランザクションは、コミット時にロールバックされます。 データベースにコミットされる変更がないため、システムはトランザクションによって使用されるリソースを単純に解放します。 読み取り専用のディスク ベース トランザクションの場合、トランザクションによって使用されるロックはこの時点ですべて解放されます。 ネイティブ コンパイル プロシージャの 1 回の実行全体での読み取り専用のメモリ最適化トランザクションの場合、検証は実行されません。  
  
 自動コミット モードの複数コンテナーにまたがる読み取り専用トランザクションは、トランザクションの終了時に単純にロールバックされます。 検証は実行されません。  
  
 明示的または暗黙的な複数コンテナーにまたがる読み取り専用トランザクションでは、REPEATABLE READ 分離または SERIALIZABLE 分離でメモリ最適化テーブルにアクセスする場合、コミット時に検証を実行します。 検証に関する詳細については、競合の検出、検証、に関するセクションを参照し、コミットの依存関係の確認[メモリ最適化テーブルでのトランザクション](../relational-databases/in-memory-oltp/memory-optimized-tables.md)です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルに対するトランザクションの概要](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [メモリ最適化テーブルでのトランザクション分離レベルに関するガイドライン](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [メモリ最適化テーブルでのトランザクションの再試行ロジックのガイドライン](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
