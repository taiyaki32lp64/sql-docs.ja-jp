---
title: メモリ最適化テーブルのインデックス | Microsoft Docs
ms.custom: ''
ms.date: 09/16/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6db09106a6ebd8128cc9a7c69b9094adbf732ad7
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929695"
---
# <a name="indexes-on-memory-optimized-tables"></a>メモリ最適化テーブルのインデックス

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

すべてのメモリ最適化テーブルには少なくとも 1 つのインデックスが必要です。このインデックスによって行が連結されるためです。 メモリ最適化テーブルでは、すべてのインデックスもメモリ最適化されます。 メモリ最適化テーブルは、ディスク ベース テーブルの従来のインデックスとはさまざまな点で違いがあります。  

- データ行はページに格納されないため、ページやエクステントのコレクションも、テーブルのすべてのページを取得するために参照できるパーティションやアロケーション ユニットもありません。 インデックスの使用可能ないずれかの型に対するインデックス ページの概念はありますが、これらの格納方法はディスクベースのテーブルのインデックスとは異なります。 それらはページ内で断片化の従来の種類を計上しないため、fillfactor を持ちません。
- データ操作中にメモリ最適化テーブルのインデックスに行われた変更がディスクに書き込まれることはありません。 データ行と、データへの変更のみが、トランザクション ログに書き込まれます。 
- メモリ最適化インデックスは、データベースがオンライに戻ったときに再構築されます。 

メモリ最適化テーブルのすべてのインデックスは、データベースの復旧中にインデックスの定義に基づいて作成されます。

インデックスは、次のいずれかにする必要があります。  
  
- ハッシュ インデックス  
- メモリ最適化済み非クラスター化インデックス (B ツリーの既定の内部構造を意味します) 
  
*ハッシュ* インデックスについては、「[メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)」で、詳しく説明します。  
*非クラスター化*インデックスについては、「[Nonclustered Index for Memory-Optimized Tables](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)」(メモリ最適化テーブルの非クラスター化インデックス) で、詳しく説明します。  
*列ストア* インデックスについては、 [別の記事](../../relational-databases/indexes/columnstore-indexes-overview.md)で説明します。  

## <a name="syntax-for-memory-optimized-indexes"></a>メモリ最適化インデックスの構文  
  
メモリ最適化テーブル用の各 CREATE TABLE ステートメントには、INDEX によって明示的に、または PRIMAY KEY もしくは UNIQUE 制約によって暗黙的にインデックスを含める必要があります。
  
既定の DURABILITY = SCHEMA\_AND_DATA で宣言するには、メモリ最適化テーブルが主キーを持つ必要があります。 次の CREATE TABLE ステートメントの PRIMARY KEY NONCLUSTERED 句は、2 つの要件を満たします。  
  
- CREATE TABLE ステートメントの 1 つのインデックスの最小要件を満たすためにインデックスを提供します。  
- SCHEMA\_AND_DATA 句に必要な主キーを提供します。  

    ```sql
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
    ```

> [!NOTE]  
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] には、メモリ最適化テーブルまたはテーブル型あたりインデックスは 8 個までという制限があります。 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、メモリ最適化テーブルおよびテーブル型に固有のインデックス数に制限がなくなりました。
  
### <a name="code-sample-for-syntax"></a>構文のコード例  
  
ここには、メモリ最適化テーブルのさまざまなインデックスを作成する構文を示す Transact-SQL コード ブロックが含まれています。 コードは、次の操作を示しています。  
  
1. メモリ最適化テーブルを作成します。  
2. ALTER TABLE ステートメントを使用して、2 つのインデックスを追加します。  
3. 数行のデータを挿入します。  
   
    ```sql
    DROP TABLE IF EXISTS SupportEvent;  
    go  

    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  

        StartDateTime        datetime2     not null,  
        CustomerName         nvarchar(16)  not null,  
        SupportEngineerName  nvarchar(16)      null,  
        Priority             int               null,  
        Description          nvarchar(64)      null  
    )  
        WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA\_AND_DATA);  
    go  
        
        --------------------  
        
    ALTER TABLE SupportEvent  
        ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  

    ALTER TABLE SupportEvent  
        ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
        
        --------------------  
        
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
        VALUES  
        ('2016-02-23 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-24 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-26 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go 
    ``` 
  
## <a name="duplicate-index-key-values"></a>重複するインデックス キー値

インデックス キーの値が重複していると、メモリ最適化テーブルのパフォーマンスが低下することがあります。 ほとんどのインデックス読み書き操作でエントリ チェーンが走査されるためシステム向けに重複が作られます。 重複するエントリのチェーンが 100 エントリを超えると、パフォーマンスの低下が無視できないほどになることがあります。

### <a name="duplicate-hash-values"></a>重複するハッシュ値

ハッシュ インデックスの場合、重複が目立って問題になります。 ハッシュ インデックスの場合に問題が大きくなるのは次の理由によります。

- ハッシュ インデックスの場合、操作あたりのコストが低い。
- 大きな重複チェーンがハッシュ競合チェーンを干渉する。

インデックス内の重複を減らすためには、次の調整をお試しください。

- クラスター化されていないインデックスを使用する。
- インデックス キーの末尾に列を追加し、重複の数を減らす。
  - たとえば、主キーにもある列を追加できます。

ハッシュ競合の詳細については、[メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)に関するページを参照してください。

### <a name="example-improvement"></a>改善例

インデックスで非効率なパフォーマンスを回避する方法の例を紹介します。

`CustomerId` に主キーが、列 `CustomerCategoryID`にインデックスがある `Customers` テーブルを考えてみてください。 一般的に、特定のカテゴリに多くの顧客がいます。 そのため、インデックスの特定のキー内には、CustomerCategoryID の重複値がたくさんできます。

このシナリオでは、`(CustomerCategoryID, CustomerId)` で非クラスター化インデックスを使用することを推奨します。 このインデックスは、`CustomerCategoryID` を伴う述語を使用するクエリに使用できます。それでも、インデックス キーには重複が含まれません。 そのため、重複する CustomerCategoryID 値やインデックスの追加列によりインデックスの保守管理が非効率になることはありません。

次のクエリでは、 `CustomerCategoryID` WideWorldImporters `Sales.Customers`サンプル データベースの [テーブルに含まれる](../../sample/world-wide-importers/wide-world-importers-documentation.md)上のインデックスについて、インデックス キー値の平均重複数がわかります。

```sql
SELECT AVG(row_count) FROM
    (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

ご使用のテーブルとインデックスについてインデックス キーの平均重複数を調べるには、 `Sales.Customers` をテーブル名、 `CustomerCategoryID` をインデックス キー列のリストで置き換えてください。

## <a name="comparing-when-to-use-each-index-type"></a>各種のインデックスを使用する状況の比較  
  
どの種類のインデックスが最善の選択であるかは、特定のクエリの性質によって決まります。  

既存のアプリケーションでメモリ最適化テーブルを実装するときは、非クラスター化インデックスから開始することが一般的に推奨されます。その機能が、ディスクベースのテーブルにおける、従来のクラスター化インデックスおよび非クラスター化インデックスの機能により近くなるためです。 
  
### <a name="recommendations-for-nonclustered-index-use"></a>非クラスター化インデックスの使用に関する推奨事項  
  
非クラスター化インデックスは、次に該当する場合にハッシュ インデックスよりも適しています。  
  
- クエリに、インデックス付き列に対する `ORDER BY` 句がある。  
- 複数列インデックスの最初の列のみをテストするクエリ。  
- クエリで、次の `WHERE` 句を使用してインデックス付き列をテストする。  
  - 非等値: `WHERE StatusCode != 'Done'`  
  - 値の範囲のスキャン: `WHERE Quantity >= 100`  
  
次のすべての SELECT では、ハッシュ インデックスよりも非クラスター化インデックスのほうが適しています。  

```sql
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE StartDateTime > DateAdd(day, -7, GetUtcDate());  

SELECT StartDateTime, CustomerName  
FROM SupportEvent  
ORDER BY StartDateTime DESC; -- ASC would cause a scan.

SELECT CustomerName  
FROM SupportEvent  
WHERE StartDateTime = '2016-02-26';  
```
  
### <a name="recommendations-for-hash-index-use"></a>ハッシュ インデックスの使用に関する推奨事項   
  
[ハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)は、範囲スキャンではなく、ポイント参照で主に使用されます。

非クラスター化インデックスでのハッシュ インデックスの使用は、クエリで等値述語を使用し、次の例のように `WHERE` 句がすべてのインデックス キー列にマップされる場合に適しています。  
  
```sql
SELECT CustomerName 
FROM SupportEvent  
WHERE SupportEngineerName = 'Liz';
```  

### <a name="multi-column-index"></a>複数列のインデックス  
  
複数列のインデックスは、非クラスター化インデックスにすることも、ハッシュ インデックスにすることもできます。 インデックスの列が col1 と col2 であるとします。 次の `SELECT` ステートメントの場合、クエリ オプティマイザーにとって役立つのは、非クラスター化インデックスのみになります。  
  
```sql
SELECT col1, col3  
FROM MyTable_memop  
WHERE col1 = 'dn';  
```

ハッシュ インデックスを使用するには、キーの列それぞれについて、`WHERE` 句が等値テストを指定する必要があります。 そうしないと、クエリ オプティマイザーにとってハッシュ インデックスは役に立ちません。  
  
インデックス キーの 2 番目の列のみ `WHERE` 句が指定した場合は、どちらの種類のインデックスも役に立ちません。  

## <a name="summary-table-to-compare-index-use-scenarios"></a>インデックス使用のシナリオを比較する概要表  
  
次の表は、異なるインデックスの種類でサポートされるすべての操作を示しています。 *はい*はインデックスが要求に十分に対応できることを意味し、*いいえ*はインデックスが要求に十分に対応できないことを意味します。 
  
| 演算 | メモリ最適化、 <br/> ハッシュ | メモリ最適化、 <br/> 非クラスター化 | ディスク ベース、 <br/> (非) クラスター化 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| インデックス スキャン、すべてのテーブルの行を取得する。 | はい | はい | はい |  
| 等値述語 (=) でのインデックス シーク。 | はい <br/> (フル キーが必要です。) | はい  | はい |  
| 非等値述語と範囲述語でのインデックス シーク <br/> (>, <, <=, >=, `BETWEEN`) | いいえ <br/> (インデックス スキャンが実行される) | はい <sup>1</sup> | はい |  
| インデックス定義と一致する行を並べ替え順序で取得する。 | いいえ | はい | はい |  
| インデックス定義の反対と一致する行を並べ替え順序で取得する。 | いいえ | いいえ | はい |  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> メモリ最適化された非クラスター化インデックスの場合、インデックス シークの実行にフル キーは必要ありません。  

## <a name="automatic-index-and-statistics-management"></a>インデックスと統計の自動管理

[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) のようなソリューションを活用し、1 つまたは複数のデータベースに対するインデックスの最適化と統計更新を自動管理します。 このプロシージャでは、断片化レベルやその他のパラメーターに基づいてインデックスを再構築または再構成するか、線形しきい値で統計を更新するかが自動的に選択されます。

## <a name="Additional_Reading"></a> 参照   
 [SQL Server インデックス デザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)   
 [メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [メモリ最適化テーブルの非クラスター化インデックス](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)    
 [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)  
