---
title: ハッシュ インデックスのトラブルシューティング - メモリ最適化テーブル
ms.custom: seo-dt-2019
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6216e8e008bff92ce502aa6dda8025c5ef63f0ba
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412661"
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>メモリ最適化テーブルのハッシュ インデックスのトラブルシューティング
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>前提条件  
  
この記事を理解するための重要なコンテキスト情報は、次の記事に収められています。  
  
- [メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>実際的な数値  
  
メモリ最適化テーブルのハッシュ インデックスを作成する場合、作成時にバケットの数を指定する必要があります。 ほとんどの場合、バケット数は、理想的にはインデックス キーの個別の値の数の 1 から 2 倍の範囲内にします。 

ただし、**BUCKET_COUNT** が推奨される範囲を多少逸脱している場合でも、ハッシュ インデックスのパフォーマンスは、許容できるか容認できる可能性があります。 少なくとも、ハッシュ インデックスの **BUCKET_COUNT** には、メモリ最適化テーブルが増大すると予測される行数とほぼ等しい値を指定することを検討してください。  
テーブルに 2,000,000 の行があるが、その数が 10 倍の 20,000, 000 行に増大すると予測していると仮定します。 テーブル内の行数の 10 倍のバケット数から始めます。 これにより、行数の増加に対応する余地ができます。  
  
- 理想的には、行数が最初のバケット数に達したときに、バケット数を増やすことになります。  
- 行数がバケット数の 5 倍に増大したとしても、多くの場合、パフォーマンスは良好です。  
  
ハッシュ インデックスに 10,000, 000 の個別のキー値があると仮定します。  
  
- バケット数 2,000,000 は、容認できるほぼ最低の値です。 パフォーマンスの低下の度合いは、許容できる可能性があります。  
  
## <a name="too-many-duplicate-values-in-the-index"></a>インデックス内の重複する値が多すぎる  
  
ハッシュ インデックス値の重複率が高いと、ハッシュ バケットのチェーンが長くなります。  
  
前の T-SQL 構文のコード ブロックと同じ SupportEvent テーブルがあると仮定します。 次の T-SQL コードは、 *すべての* 値の *一意の* 値に対する比率を検出して表示する方法を示しています。  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- 比率 10.0 以上は、インデックスの種類としてハッシュは適していないことを意味します。 代わりに非クラスター化インデックスを使用することを検討してください。   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>ハッシュ インデックスのバケット数のトラブルシューティング  
  
このセクションでは、ハッシュ インデックスのバケット数のトラブルシューティング方法について説明します。  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>チェーンと空のバケットの統計を監視する  
  
次の T-SQL SELECT を実行することで、ハッシュ インデックスの統計を監視できます。 この SELECT では、 **sys.dm_db_xtp_hash_index_stats**という名前のデータ管理ビュー (DMV) を使用します。  
  
```sql
SELECT  
  QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
  i.name                   as [index],   
  h.total_bucket_count,  
  h.empty_bucket_count,  
    
  FLOOR((  
    CAST(h.empty_bucket_count as float) /  
      h.total_bucket_count) * 100)  
                            as [empty_bucket_percent],  
  h.avg_chain_length,   
  h.max_chain_length  
FROM  
        sys.dm_db_xtp_hash_index_stats  as h   
  JOIN sys.indexes                     as i  
          ON h.object_id = i.object_id  
          AND h.index_id  = i.index_id  
JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
JOIN sys.tables t on h.object_id=t.object_id
WHERE ia.type=1
ORDER BY [table], [index];  
```
  
SELECT の結果を、次の統計ガイドラインと比較します。  
  
- 空のバケット:  
  - 33% は適切な目標値ですが、通常は、より大きなパーセント値 (ちょうど 90%) がふさわしい値となります。  
  - バケット数が個別のキー値の数と等しい場合は、バケットの約 33% が空です。  
  - 10% 未満の値は低すぎます。  
- バケット内のチェーン:  
  - 平均チェーン長は、重複するインデックス キーの値がない場合、1 が最適です。 通常、10 までのチェーン長を使用できます。  
  - 平均チェーン長が 10 より大きく、空のバケットの割合が 10% を超える場合、非常に多くのデータが重複しているため、ハッシュ インデックスは最も適切な種類ではない可能性があります。  
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>チェーンと空のバケットのデモンストレーション  
  
次の T-SQL コード ブロックを使用すると、 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`を簡単にテストできます。 このコード ブロックは 1 分で完了します。 次のコード ブロックのフェーズを以下に示します。  
  
1. いくつかのハッシュ インデックスがあるメモリ最適化テーブルを作成します。  
2. テーブルに数千行を設定します。  
    a. モジュロ演算子を使用して、StatusCode 列の重複する値の割合を構成します。  
    b. INSERT ループは、262,144 行を約 1 分間で挿入します。  
3. PRINT は、前述の SELECT を **sys.dm_db_xtp_hash_index_stats**から実行することを指示するメッセージを出力します。  

```sql
DROP TABLE IF EXISTS SalesOrder_Mem;  
go  
  
  
CREATE TABLE SalesOrder_Mem  
(  
  SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
  OrderSequence  int               NOT NULL,  
  OrderDate      datetime2(3)      NOT NULL,  
  StatusCode     tinyint           NOT NULL,  
  
  PRIMARY KEY NONCLUSTERED  
      HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
  
  INDEX ix_OrderSequence  
      HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
  
  INDEX ix_StatusCode  
      HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
  
  INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
)  
  WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
--------------------  
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
前述の `INSERT` ループは、次の操作を行います。  
  
- 主キー インデックスと *ix_OrderSequence* に一意の値を挿入します。  
- `StatusCode` の 8 つのみの個別の値を表す 20 ～ 30 万の行を挿入します。 したがって、*ix_StatusCode* インデックスの値は高い割合で重複しています。  
  
バケット数が最適でない場合のトラブルシューティングを行うために、 **sys.dm_db_xtp_hash_index_stats**からの SELECT の次の出力を確認します。 これらの結果を得るために、セクション D.1 からコピーした SELECT に `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` を追加しています。  
  
`SELECT` の結果をコードの後に示しています。見やすくするために、結果を幅の狭い 2 つの結果表に意図的に分割しています。  
  
- *バケット数*に関する結果は次のとおりです。  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
- *チェーン長*に関する結果を次に示します。  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
これらの結果表から、3 つのハッシュ インデックスを解釈してみましょう。  
  
*ix_StatusCode:*  
  
- バケットの 50% が空です。これは適切な値です。  
- ただし、平均チェーン長が非常に高くなっています (65,536)。  
  - これは、重複する値の割合が高いことを示しています。  
  - したがって、この場合は、ハッシュ インデックスの使用は適切ではありません。 代わりに、非クラスター化インデックスを使用する必要があります。  
  
*ix_OrderSequence:*  
  
- バケットの 0% が空です。この値は低すぎます。  
- このインデックスのすべての値が一意であっても、平均チェーン長は 8 になっています。  
  - したがって、バケット数を増やして、平均チェーン長が 2 または 3 に近づくまで減らす必要があります。  
- インデックス キーには 262,144 個の一意の値があるため、バケット数は最低でも 262,144 にする必要があります。  
  - 今後の増大が予測される場合、バケット数はさらに高くする必要があります。  
  
*Primary key index (PK_SalesOrd_...):*  
  
- バケットの 36% が空です。これは適切な値です。  
- 平均チェーン長は 1 であり、これも適切な値です。 変更は不要です。  
  
### <a name="balancing-the-trade-off"></a>トレードオフのバランスを考慮する  
  
OLTP ワークロードは、個々の行に注目します。 フル テーブル スキャンは、通常は OLTP ワークロードのパフォーマンスのクリティカル パスではありません。 したがって、**メモリ使用率の数量**と、**等値テストと挿入操作のパフォーマンス**とのトレードオフのバランスを考慮する必要があります。  
  
**メモリの使用量のほうが大きな問題である場合:**  
  
- インデックス キー レコードの数に近いバケット数を選択します。  
- バケット数は、インデックス キー値の数より大幅に小さくならないようにする必要があります。大幅に小さい場合、ほとんどの DML 操作や、サーバーの再起動後のデータベースの復旧に要する時間にも影響があります。  
  
**等値テストのパフォーマンスのほうが大きな問題である場合:**  
  
- 一意のインデックス値の数の 2 倍または 3 倍のバケット数が適しています。 高いバケット数は、次のことを意味します。  
  - 1 つの特定の値を検索する場合の高速での取得。  
  - メモリ使用率の上昇。  
  - ハッシュ インデックスのフル スキャンに必要な時間の増加。  
  

##  <a name="Additional_Reading"></a> その他の情報  
 [メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [メモリ最適化テーブルの非クラスター化インデックス](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  
