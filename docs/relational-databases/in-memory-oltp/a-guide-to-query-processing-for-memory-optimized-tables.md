---
title: メモリ最適化テーブルのクエリ処理
ms.custom: seo-dt-2019
ms.date: 05/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 065296fe-6711-4837-965e-252ef6c13a0f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef5c610cb71a0f638c2dfba8aad1fbdb77308dfa
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412821"
---
# <a name="a-guide-to-query-processing-for-memory-optimized-tables"></a>メモリ最適化テーブルのクエリ処理のガイド
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、インメモリ OLTP によってメモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャが導入されています。 ここでは、メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャの両方に対するクエリ処理の概要について説明します。  
  
 ここでは、次の内容を含め、メモリ最適化テーブルに対するクエリがどのようにコンパイルおよび実行されるかについて説明します。  
  
-   ディスク ベース テーブルに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリ処理パイプライン。  
  
-   クエリ最適化。メモリ最適化テーブルの統計のロール、および不適切なクエリ プランのトラブルシューティングのためのガイドライン。  
  
-   解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用したメモリ最適化テーブルへのアクセス。  
  
-   メモリ最適化テーブルへのアクセスのためのクエリ最適化に関する注意点。  
  
-   ネイティブ コンパイル ストアド プロシージャのコンパイルと処理。  
  
-   オプティマイザーがコストの推定に使用する統計。  
  
-   不適切なクエリ プランを修正する方法。  
  
## <a name="example-query"></a>サンプル クエリ  
 次の例を使用して、この記事で説明するクエリ処理の概念を示します。  
  
 ここでは、Customer と Order という 2 個のテーブルについて検討します。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトには、2 個のテーブルおよび関連するインデックスの定義が (従来の) ディスク ベース形式で含まれています。  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY,  
  ContactName nvarchar (30) NOT NULL   
)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY,  
  CustomerID nchar (5) NOT NULL,  
  OrderDate date NOT NULL  
)  
GO  
CREATE INDEX IX_CustomerID ON dbo.[Order](CustomerID)  
GO  
CREATE INDEX IX_OrderDate ON dbo.[Order](OrderDate)  
GO  
```  
  
 ここでは、クエリ プランを構築できるように、2 個のテーブルに Northwind サンプル データベースのサンプル データが読み込まれています。このサンプル データベースは「 [SQL Server 2000 用の Northwind サンプル データベースと pubs サンプル データベース](https://www.microsoft.com/download/details.aspx?id=23654)」からダウンロードできます。  
  
 次のクエリについて考えてみます。このクエリでは、Customer テーブルと Order テーブルを結合し、注文の ID および関連付けられた顧客情報を返します。  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、次のような推定実行プランが表示されます。  
  
 ![ディスク ベース テーブルの結合のためのクエリ プラン。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-1.png "|::ref1::|")  
ディスク ベース テーブルの結合のためのクエリ プラン。  
  
 このクエリ プランについて  
  
-   Customer テーブルの行は、クラスター化インデックスから取得されます。これは、テーブル データ全体を含んでいるプライマリ データ構造になっています。  
  
-   Order テーブルのデータは、CustomerID 列の非クラスター化インデックスを使用して取得されます。 このインデックスには、結合に使用される CustomerID 列と、ユーザーに返す主キー列 OrderID の両方が含まれています。 Order テーブルから追加の列を返す場合は、Order テーブルのクラスター化インデックス内の参照が必要です。  
  
-   論理演算子 **Inner Join** は、物理演算子 **Merge Join**によって実装されます。 その他の物理結合の種類は、 **Nested Loops** と **Hash Join**です。 この **Merge Join** 演算子では、両方のインデックスが結合列 CustomerID を基準に並べ替えられていることを利用します。  
  
 これを少し変えたバリエーションとして、OrderID だけでなく、Order テーブルのすべての行を返すクエリを検討します。  
  
```sql  
SELECT o.*, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 このクエリの推定プランは、次のとおりです。  
  
 ![ディスク ベース テーブルのハッシュ結合のクエリ プラン。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-2.png "|::ref2::|")  
ディスク ベース テーブルのハッシュ結合のクエリ プラン。  
  
 このクエリでは、Orders テーブルの行はクラスター化インデックスを使用して取得されます。 これで、 **Hash Match** 物理演算子は **Inner Join**に使用されます。 Order のクラスター化インデックスは CustomerID で並べ替えられません。したがって、 **Merge Join** はパフォーマンスに影響を与えるソート演算子を必要とします。 前の例の **Hash Match** 演算子のコスト (46%) と比較して、 **Merge Join** 演算子 (75%) の相対コストを確認してください。 オプティマイザーでは、前の例でも **Hash Match** 演算子を検討したうえで、 **Merge Join** 演算子の方がパフォーマンスがよいと判断されています。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-query-processing-for-disk-based-tables"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディスク ベース テーブルに対するクエリ処理  
 次の図は、アドホック クエリに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリ処理フローの概要を示しています。  
  
 ![SQL Server クエリ処理パイプライン。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-3.png "|::ref3::|")  
SQL Server クエリ処理パイプライン。  
  
 このシナリオでは:  
  
1.  ユーザーがクエリを実行します。  
  
2.  パーサーと algebrizer は、ユーザーから送信される [!INCLUDE[tsql](../../includes/tsql-md.md)] テキストに基づき、論理操作でクエリ ツリーを構築します。  
  
3.  オプティマイザーは物理操作 (たとえば、Nested Loops 結合) を含む最適化されたクエリ プランを作成します。 最適化後に、そのプランはプラン キャッシュに保存される場合もあります。 プラン キャッシュにこのクエリのプランが既に含まれている場合、この手順は省略されます。  
  
4.  クエリ実行エンジンは、クエリ プランの解釈を処理します。  
  
5.  各インデックスのシーク、インデックス スキャン、およびテーブル スキャン操作では、実行エンジンはそれぞれのインデックスおよびテーブルの構造からの行を Access Methods から要求します。  
  
6.  Access Methods は、バッファー プールのインデックスおよびデータ ページから行を取得し、必要に応じてバッファー プールにディスクからページを読み込みます。  

 クエリの最初の例の場合、実行エンジンは、Customer のクラスター化インデックスおよび Order の非クラスター化インデックスの行を Access Methods から要求します。 Access Methods は、要求された行を取得するために B ツリー インデックス構造をスキャンします。 この場合は、プランがフル インデックス スキャンを必要とするため、すべての行が取得されます。  
  
## <a name="interpreted-includetsqlincludestsql-mdmd-access-to-memory-optimized-tables"></a>解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] によるメモリ最適化テーブルへのアクセス  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] アドホック バッチおよびストアド プロシージャは、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]とも呼ばれます。 "解釈された" とは、クエリ プラン内の各演算子について、クエリ実行エンジンによってクエリ プランが解釈されることを意味します。 実行エンジンは、演算子とそのパラメーターを読み取り、操作を実行します。  
  
 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、メモリ最適化テーブルとディスク ベース テーブルの両方にアクセスできます。 次の図は、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] によるメモリ最適化テーブルへのアクセスのクエリ処理を示しています。  
  
 ![解釈された tsql のクエリ処理パイプライン。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-4.png "解釈された tsql のクエリ処理パイプライン。")  
解釈された Transact-SQL によるメモリ最適化テーブルへのアクセスのクエリ処理パイプライン。  
  
 図で示すように、ほとんどの場合、クエリ処理パイプラインは変更されません。  
  
-   パーサーと algebrizer はクエリ ツリーを構築します。  
  
-   オプティマイザーは実行プランを作成します。  
  
-   クエリ実行エンジンは、実行プランを解釈します。  
  
 従来のクエリ処理パイプライン (図 2) との主な相違点は、メモリ最適化テーブルの行が Access Methods を使用してバッファー プールから取得されないことです。 代わりに、インメモリ データ構造体からインメモリ OLTP エンジンを使用して行が取得されます。 データ構造が異なるために、次の例で示すように、オプティマイザーが異なるプランを引数として取得する場合があります。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトには、ハッシュ インデックスを使用する Order テーブルと Customer テーブルのメモリ最適化バージョンが含まれています。  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY NONCLUSTERED,  
  ContactName nvarchar (30) NOT NULL   
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY NONCLUSTERED,  
  CustomerID nchar (5) NOT NULL INDEX IX_CustomerID HASH(CustomerID) WITH (BUCKET_COUNT=100000),  
  OrderDate date NOT NULL INDEX IX_OrderDate HASH(OrderDate) WITH (BUCKET_COUNT=100000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 同じクエリをメモリ最適化テーブルで実行するとします。  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 推定プランは次のとおりです。  
  
 ![メモリ最適化テーブルの結合のためのクエリ プラン。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-5.png "メモリ最適化テーブルの結合のためのクエリ プラン。")  
メモリ最適化テーブルの結合のためのクエリ プラン。  
  
 ディスク ベース テーブルの同じクエリに対するプラン (図 1) で、次の相違点を確認します。  
  
-   このプランでは、Customer テーブルに対するクラスター化インデックス スキャンではなくテーブル スキャンが含まれています。  
  
    -   テーブルの定義には、クラスター化インデックスが含まれていません。  
  
    -   クラスター化インデックスは、メモリ最適化テーブルでサポートされていません。 代わりに、すべてのメモリ最適化テーブルには 1 つ以上の非クラスター化インデックスが必要です。メモリ最適化テーブルのすべてのインデックスは、そのテーブル内のすべての列に効率的にアクセスできます。列をインデックスに格納したり、クラスター化されたインデックスを参照したりする必要はありません。  
  
-   このプランには、 **Merge Join** ではなく **Hash Match**が含まれます。 Order テーブルと Customer テーブルの両方のインデックスはハッシュ インデックスになるため、順序付けされません。 **Merge Join** では並べ替え操作が必要であり、それによってパフォーマンスが低下していました。  
  
## <a name="natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャ  
 ネイティブ コンパイル ストアド プロシージャは、クエリ実行エンジンによって解釈されるのではなく、マシン語コードにコンパイルされる [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャです。 次のスクリプトは、(クエリの例のセクションの) クエリの例を実行する、ネイティブ コンパイル ストアド プロシージャを作成します。  
  
```sql  
CREATE PROCEDURE usp_SampleJoin  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = 'english')  
  
  SELECT o.OrderID, c.CustomerID, c.ContactName   
FROM dbo.[Order] o INNER JOIN dbo.[Customer] c   
  ON c.CustomerID = o.CustomerID  
  
END  
```  
  
 ネイティブ コンパイル ストアド プロシージャは作成時にコンパイルされ、解釈されたストアド プロシージャは最初の実行時にコンパイルされます (コンパイルの一部、特に解析と algebrizer の処理は作成時に実行されますが、 解釈されたストアド プロシージャの場合は、最初の実行時にクエリ プランの最適化が実行されます)。再コンパイルの論理と似ています。 サーバーを再起動した場合、ネイティブ コンパイル ストアド プロシージャは、プロシージャの最初の実行時に再コンパイルされます。 解釈されたストアド プロシージャは、そのプランがプラン キャッシュに存在しなくなった場合は再コンパイルされます。 次の表は、ネイティブ コンパイル ストアド プロシージャと解釈されたストアド プロシージャの両方について、コンパイルおよび再コンパイルのケースをまとめたものです。  
  
||ネイティブ コンパイル ストアド プロシージャ|解釈された|  
|-|-----------------------|-----------------|  
|最初のコンパイル|作成時。|最初の実行時。|  
|自動再コンパイル|データベースまたはサーバーの再起動後、プロシージャの最初の実行時。|サーバーの再起動時。 または、通常はスキーマや統計の変更またはメモリ不足に基づく、プラン キャッシュからの削除時。|  
|手動での再コンパイル|**sp_recompile**の使用。|**sp_recompile**の使用。 たとえば DBCC FREEPROCCACHE を使用して、キャッシュからプランを手動で削除できます。 また、WITH RECOMPILE ストアド プロシージャを作成することもできます。このストアド プロシージャは、実行のたびに再コンパイルされます。|  
  
### <a name="compilation-and-query-processing"></a>コンパイルとクエリ処理  
 次の図は、ネイティブ コンパイル ストアド プロシージャのコンパイル処理を示しています。  
  
 ![ストアド プロシージャのネイティブでのコンパイル](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-6.png "ストアド プロシージャのネイティブでのコンパイル")  
ストアド プロシージャのネイティブでのコンパイル  
  
 この処理は次のとおりです。  
  
1.  ユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対して **CREATE PROCEDURE** ステートメントを実行します。  
  
2.  パーサーと algebrizer は、プロシージャの処理フロー、およびストアド プロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリのクエリ ツリーを作成します。  
  
3.  オプティマイザーは、ストアド プロシージャ内のすべてのクエリに対して最適化されたクエリ実行プランを作成します。  
  
4.  インメモリ OLTP コンパイラは、埋め込みの最適化されたクエリ プランで処理フローを受け取り、ストアド プロシージャを実行するためのマシン語コードを含む DLL を生成します。  
  
5.  生成された DLL がメモリに読み込まれます。  
  
 ネイティブ コンパイル ストアド プロシージャの呼び出しは、DLL 内の関数の呼び出しに変換されます。  
  
 ![ネイティブ コンパイル ストアド プロシージャの実行。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-7.png "|::ref7::|")  
ネイティブ コンパイル ストアド プロシージャの実行。  
  
 ネイティブ コンパイル ストアド プロシージャの呼び出しは、次のとおりです。  
  
1.  ユーザーは、 **EXEC**_usp_myproc_ ステートメントを実行します。  
  
2.  パーサーは、名前とストアド プロシージャのパラメーターを抽出します。  
  
     たとえば **sp_prep_exec**を使用して、ステートメントが準備されている場合、パーサーは実行時にプロシージャ名とパラメーターを抽出する必要はありません。  
  
3.  インメモリ OLTP ランタイムがストアド プロシージャに対する DLL エントリ ポイントを特定します。  
  
4.  DLL のマシン語コードが実行され、その結果がクライアントに返されます。  
  
 **パラメーターを見つけ出す**  
  
 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャは最初の実行時にコンパイルされますが、ネイティブ コンパイル ストアド プロシージャは作成時にコンパイルされます。 解釈されたストアド プロシージャが呼び出し時にコンパイルされる場合、この呼び出しに指定されたパラメーターの値が、実行プランの生成時にオプティマイザーによって使用されます。 コンパイル時にパラメーターをこのように使用することを、"パラメーターを見つけ出す" と表現します。  
  
 パラメーターを見つけ出すことは、ネイティブ コンパイル ストアド プロシージャのコンパイルには使用されません。 ストアド プロシージャに対するすべてのパラメーターは、UNKNOWN 値があると見なされます。 解釈されたストアド プロシージャと同様に、ネイティブ コンパイル ストアド プロシージャでも、 **OPTIMIZE FOR** ヒントがサポートされます。 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。  
  
### <a name="retrieving-a-query-execution-plan-for-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャ用のクエリ実行プランの取得  
 ネイティブ コンパイル ストアド プロシージャ用のクエリ実行プランは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **推定実行プラン** または [!INCLUDE[tsql](../../includes/tsql-md.md)]の SHOWPLAN_XML オプションを使用して取得できます。 次に例を示します。  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC dbo.usp_myproc  
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 クエリ オプティマイザーによって生成される実行プランは、ノード上のクエリ演算子を含むツリーおよびツリーのリーフで構成されます。 ツリーの構造により、演算子間の対話 (演算子間での行のフロー) が決定されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のグラフィカルなビューでは、フローは右から左に流れます。 たとえば、図 1 のクエリ プランは、2 個のインデックス スキャン操作を含み、マージ結合操作に行を渡しています。 マージ結合操作が選択操作に行を渡します。 選択操作は、最終的にはクライアントに行を返します。  
  
### <a name="query-operators-in-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャのクエリ演算子  
 次の表は、ネイティブ コンパイル ストアド プロシージャの内部でサポートされるクエリ演算子をまとめたものです。  
  
|演算子|サンプル クエリ|メモ|  
|--------------|------------------|-----------|  
|SELECT|`SELECT OrderID FROM dbo.[Order]`||  
|INSERT|`INSERT dbo.Customer VALUES ('abc', 'def')`||  
|UPDATE|`UPDATE dbo.Customer SET ContactName='ghi' WHERE CustomerID='abc'`||  
|DELETE|`DELETE dbo.Customer WHERE CustomerID='abc'`||  
|Compute Scalar|`SELECT OrderID+1 FROM dbo.[Order]`|この操作は、組み込み関数と型変換の両方で使用されます。 一部の関数と型変換は、ネイティブ コンパイル ストアド プロシージャの内部でサポートされません。|  
|Nested Loops 結合|`SELECT o.OrderID, c.CustomerID FROM dbo.[Order] o INNER JOIN dbo.[Customer] c`|Nested Loops は、ネイティブ コンパイル ストアド プロシージャでサポートされている唯一の結合操作です。 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] として実行される同じクエリのプランにハッシュ結合またはマージ結合が含まれている場合でも、結合を含むすべてのプランは Nested Loops 操作を使用します。|  
|並べ替え|`SELECT ContactName FROM dbo.Customer ORDER BY ContactName`||  
|TOP|`SELECT TOP 10 ContactName FROM dbo.Customer`||  
|Top-sort|`SELECT TOP 10 ContactName FROM dbo.Customer  ORDER BY ContactName`|**TOP** 式 (返される行数) が 8,000 行を超えることはできません。 クエリに結合演算子および集計演算子がある場合、処理できる行数はこれより少なくなります。 一般的に結合と集計を行うと、並べ替える行数は、ベース テーブルの行数より少なくなります。|  
|Stream Aggregate|`SELECT count(CustomerID) FROM dbo.Customer`|Hash Match 操作が集計をサポートしていないことに注意してください。 したがって、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] 内の同じクエリに対するプランが Hash Match 操作を使用しても、ネイティブ コンパイル ストアド プロシージャ内のすべての集計は Stream Aggregate 操作を使用します|  
  
## <a name="column-statistics-and-joins"></a>列統計と結合  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックス スキャンやインデックス シークなど特定の操作のコストを推定できるように、インデックス キー列に値の統計を保持します。 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、非インデックス キー列に対しても、明示的に作成された場合またはクエリ オプティマイザーによってクエリの述語に応じて作成された場合、統計が作成されます)。コストの推定の主要な基準は、1 個の操作によって処理される行数です。 ディスク ベース テーブルの場合、コストの推定では、特定の操作でアクセスされるページ数が重要です。 ただし、メモリ最適化テーブルではページ数は重要ではないため (常にゼロ)、ここでは行数を中心に説明します。 推定は、プラン内のインデックス シークおよびスキャン操作で開始され、続いて、結合操作などの他の操作へと進みます。 結合操作によって処理される行数の推定値は、基になるインデックス、シーク、およびスキャン操作の推定値に基づきます。 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] によるメモリ最適化テーブルへのアクセスの場合は、実際の実行プランを調べて、プラン内の操作の推定行数と実際の行数の違いを確認することができます。  
  
 図 1 の例の場合は、次のようになります。  
  
-   Customer でのクラスター化インデックス スキャンは、推定値が 91、実際の値が 91。  
  
-   CustomerID での非クラスター化インデックス スキャンは、推定値が 830、実際の値が 830。  
  
-   マージ結合操作は、推定値が 815、実際の値が 830。  
  
 インデックス スキャンの推定値は正確です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディスク ベース テーブルの行数を保持します。 テーブル全体の推定およびインデックス スキャンは常に正確です。 結合の推定も非常に正確です。  
  
 これらの推定が変わると、さまざまなプランの選択肢に対するコストの注意点も変わります。 たとえば、1 個の結合操作の推定値が 1 または少ない行数である場合、Nested Loops 結合を使用する方が低コストです。  
  
 次に、クエリのプランを示します。  
  
```  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 Customer テーブルで 1 行だけを残してすべての行を削除した後  
  
 ![列統計と結合。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-9.png "|::ref8::|")  
  
 このクエリ プランについて  
  
-   Hash Match は、Nested Loops 物理結合操作で置き換えられました。  
  
-   IX_CustomerID でのフル インデックス スキャンは、インデックス シークで置き換えられました。 これにより、スキャンの対象は 5 行となり、フル インデックス スキャンに必要な 830 行ではなくなります。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
