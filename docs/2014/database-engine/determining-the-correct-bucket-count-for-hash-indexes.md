---
title: ハッシュ インデックスの適切なバケット数を決定する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b79c0908f8639df869d01a8ff862afc5be77cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754244"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>ハッシュ インデックスの適切なバケット数の決定
  メモリ最適化テーブルを作成するときに `BUCKET_COUNT` パラメーターの値を指定する必要があります。 このトピックでは、`BUCKET_COUNT` パラメーターの適切な値を判断する際の推奨事項を示します。 適切なバケット数を決定できない場合は、代わりに非クラスター化インデックスを使用してください。  `BUCKET_COUNT` の値が不適切な場合 (特に小さすぎる場合)、ワークロードのパフォーマンス、およびデータベースの復旧時間に大きな影響を与えることがあります。 バケット数は大きめに設定することをお勧めします。  
  
 重複したインデックス キーは、複数のキーが同じバケットにハッシュされることが原因でバケットのチェーンの増加を引き起こし、ハッシュ インデックスのパフォーマンス低下につながる可能性があります。  
  
 非クラスター化ハッシュ インデックスの詳細については、「 [Hash Indexes](hash-indexes.md) 」と「 [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)」を参照してください。  
  
 メモリ最適化テーブルの各ハッシュ インデックスに対して 1 個のハッシュ テーブルが割り当てられます。 インデックスがで指定された割り当てられるハッシュ テーブルのサイズ、`BUCKET_COUNT`パラメーター [CREATE TABLE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql)または[CREATE TYPE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql). バケット数は内部的に、最も近い 2 のべき乗に切り上げられます。 たとえば、バケット数に 300,000 を指定すると、実際のバケット数は 524,288 になります。  
  
 バケット数に関する記事とビデオへのリンクについては、「 [ハッシュ インデックス (インメモリ OLTP) に正しいバケット数を指定する方法](https://www.mssqltips.com/sqlservertip/3104/determine-bucketcount-for-hash-indexes-for-sql-server-memory-optimized-tables/)」を参照してください。  
  
## <a name="recommendations"></a>推奨事項  
 ほとんどの場合、バケット数はインデックス キーにおける別個の値の数の 1 倍から 2 倍の範囲に設定する必要があります。 インデックス キーに重複する値が多数含まれている場合 (平均して各インデックス キー値に対して 10 を超える行がある場合) は、代わりに非クラスター化インデックスを使用します。  
  
 特定のインデックス キーに値がどれぐらいあるかは、予測できないこともあります。 `BUCKET_COUNT` 値が実際のキー値の数の 5 倍以内である場合、パフォーマンスは許容できます。  
  
 既存のデータの一意なインデックス キーの数を判断するには、次の例のようなクエリを使用します。  
  
### <a name="primary-key-and-unique-indexes"></a>主キーと一意インデックス  
 主キー インデックスは一意であるため、そのキーでの別個の値の数はテーブル内の行の数に相当します。 AdventureWorks データベースの Sales.SalesOrderDetail テーブル内の (SalesOrderID, SalesOrderDetailID) の主キーの例の場合は、次のクエリを発行して、テーブル内の行数に相当する別個の主キーの値の数を計算します。  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 このクエリは行数 121,317 を示します。 行数が大幅に変化しない場合は、240,000 というバケット数を使用します。 テーブル内にある販売注文の数が 4 倍になると予想されている場合は、480,000 というバケット数を使用します。  
  
### <a name="non-unique-indexes"></a>一意ではないインデックス  
 (SpecialOfferID, ProductID) の複数列のインデックスなど、その他のインデックスの場合は、次のクエリを発行して一意なインデックス キーの値の数を決定します。  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 このクエリは (SpecialOfferID, ProductID) に対応するインデックス キー数として 484 を返し、非クラスター化ハッシュ インデックスの代わりに、非クラスター化インデックスを使用する必要があることを示します。  
  
### <a name="determining-the-number-of-duplicates"></a>重複数の決定  
 インデックス キー値の重複する値の平均数を決定するには、合計行数を一意のインデックス キーの数で割ります。  
  
 (SpecialOfferID, ProductID) のインデックスの例の場合は、121317 / 484 = 251 になります。 この結果から、インデックス キーの値が平均して 251 あるため、非クラスター化インデックスを使用する必要があることがわかります。  
  
## <a name="troubleshooting-the-bucket-count"></a>バケット数のトラブルシューティング  
 メモリ最適化テーブルのバケット数の問題をトラブルシューティングするには、 [sys.dm_db_xtp_hash_index_stats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql)空のバケットと行チェーンの長さに関する統計情報を取得します。 次のクエリを使用して、現在のデータベースのすべてのハッシュ インデックスに関する統計情報を取得できます。 データベースに大きなテーブルがある場合、このクエリの実行には数分かかることがあります。  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 ハッシュ インデックスの状態を示す主要インジケーターとして、次の 2 つがあります。  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* は、ハッシュ インデックス内の空のバケットの数を示します。  
  
 *empty_bucket_percent* が 10 未満の場合は、バケット数が少なすぎると考えられます。 *empty_bucket_percent* は 33% 以上であるのが理想的です。 バケット数がインデックス キー値の数と一致する場合、ハッシュ分散のためにバケットの約 1/3 が空です。  
  
 *avg_chain_length*  
 *avg_chain_length* は、ハッシュ バケット内の行チェーンの平均の長さを示します。  
  
 *avg_chain_length* が 10 より大きくて、 *empty_bucket_percent* が 10% より大きい場合は、重複するインデックス キー値が多いと考えられるため、非クラスター化インデックスの方が適切です。 平均チェーン長さが 1 であれば理想的です。  
  
 チェーン長さに影響を与える要素には、次の 2 つがあります。  
  
1.  重複: すべての重複行は、ハッシュ インデックスの同じチェーンに含まれます。  
  
2.  複数のキー値が同じバケットにマップされます。 バケット数が少ない場合は、複数の値のマップ先となるバケットが多くなります。  
  
 例として、次のテーブルとテーブルのサンプル行を挿入するスクリプトを考えます。  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 スクリプトは、テーブルに 262,144 個の行を挿入します。 これは、主キー インデックスと IX_OrderSequence に一意な値を挿入し、 重複する値をインデックス IX_Status に挿入します。別個の値は 8 つだけ生成されます。  
  
 BUCKET_COUNT トラブルシューティング クエリの出力は次のとおりです。  
  
|インデックス名|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 このテーブルの 3 つのハッシュ インデックスについて考えます。  
  
-   IX_Status:バケットの 50% が空で、適切です。 しかし、平均チェーン長さは非常に高くなっています (65,536)。 これは、重複する値が多いことを示しています。 したがって、この場合は非クラスター化ハッシュ インデックスの使用は適切ではありません。 代わりに、非クラスター化インデックスを使用する必要があります。  
  
-   IX_OrderSequence:バケットの 0% は、空が低すぎます。 また、平均チェーン長さは 8 です。 このインデックスの値は一意であるため、これは平均 8 個の値が各バケットにマップされていることを意味します。 バケット数を増やす必要があります。 インデックス キーには 262,144 個の一意な値があるため、バケット数は少なくとも 262,144 個必要です。 今後さらに大きくなることが予測される場合、さらに数を多くする必要があります。  
  
-   主キー インデックス (pk _ _salesorder...):バケットの 36% が空で、適切です。 また、平均チェーン長さも 1 で、適切です。 変更は不要です。  
  
 メモリ最適化ハッシュ インデックスの問題のトラブルシューティングの詳細については、「 [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md)」を参照してください。  
  
## <a name="detailed-considerations-for-further-optimization"></a>さらに最適化するための詳細な検討  
 このセクションでは、バケット数を最適化するための考慮事項について概説します。  
  
 ハッシュ インデックスで最高のパフォーマンスを発揮するには、ハッシュ テーブルに割り当てるメモリの量と主キーでの別個の値の数とのバランスを取ります。 ポイント参照とテーブル スキャンの間のバランスもあります。  
  
-   バケット数が大きくなると、インデックス内の空のバケットの数が増えることになります。 このことは、各バケットをテーブル スキャンの一部としてスキャンするときに、メモリ使用量 (バケットごとに 8 バイト) とテーブル スキャンのパフォーマンスに影響を与えます。  
  
-   バケット数が小さくなると、単一のバケットにより多くの値が割り当てられます。 この場合、検索述語で指定された値を検索するには [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が単一のバケットで複数の値をスキャンすることが必要になる可能性があるため、ポイント参照や挿入のパフォーマンスが低下します。  
  
 バケット数が一意のインデックス キーの数を大幅に下回る場合、多くの値が各バケットにマップされます。 これによって、ポイント参照 (個々のインデックス キーの参照) や挿入操作などほとんどの DML 操作でパフォーマンスが低下します。 たとえば、WHERE 句でインデックス キー列を照合するための等値述語が含まれた SELECT クエリ、UPDATE 操作、および DELETE 操作で、パフォーマンスが低下する可能性があります。 データベースの起動時にインデックスが再作成されるため、バケット数が少ないと、データベースの復旧時間にも影響があります。  
  
### <a name="duplicate-index-key-values"></a>重複するインデックス キー値  
 重複する値によって、ハッシュの競合のパフォーマンスに与える影響が大きくなることがあります。 各インデックス キーの重複数が少ない場合、これは通常は問題ではありません。 ただし、一意のインデックス キーの数とテーブル内の行の数の差が非常に大きくなると、問題になる可能性があります。  
  
 インデックス キーの値が同じである行はすべて同じ重複チェーンに入ります。 ハッシュの競合により複数のインデックス キーが同じバケットにある場合、インデックスのスキャナーは常に、2 つ目の値に対応する最初の行の検索前に最初の値の完全な重複チェーンをスキャンする必要があります。 重複するキーによって、ガベージ コレクションで行を探すことが困難にもなります。 たとえば、任意のキーの重複が 1,000 個あり、その行の 1 つが削除された場合、ガベージ コレクターは、一連の 1,000 個の重複をスキャンし、インデックスから行のリンクを解除する必要があります。 これは、削除対象を検索したクエリでより効率的なインデックス (主キー インデックス) を使用して行を指定する場合にも当てはまります。ガベージ コレクターは各インデックスからリンクを解除する必要があるためです。  
  
 ハッシュ インデックスの場合、インデックス キー値の重複が原因で生じる作業量を減らす方法は 2 とおりあります。  
  
-   代わりに、非クラスター化インデックスを使用します。 インデックス キーに列を追加して、重複数を減らすことができます。その際、アプリケーションを変更する必要はありません。  
  
-   インデックスに非常に多いバケット数を指定します。 たとえば、一意のインデックス キーの数の 20 ～ 100 倍を指定します。 これで、ハッシュの競合が減少します。  
  
### <a name="small-tables"></a>小さいテーブル  
 小さいテーブルの場合は、データベース全体のサイズと比較してインデックスのサイズが小さいため、メモリ使用量は通常は問題になりません。  
  
 ここでは、必要なパフォーマンスの種類に基づいて選択する必要があります。  
  
-   インデックスに関するパフォーマンス クリティカルな操作が主にポイント参照や挿入操作の場合は、バケット数を大きくするとハッシュ競合の可能性が少なくなります。 行の数の 3 倍以上に設定するのが最適です。  
  
-   パフォーマンス クリティカルな操作がフル インデックス スキャンである場合は、実際のインデックス キー値の数に近いバケット数を使用します。  
  
### <a name="big-tables"></a>大きいテーブル  
 大きいテーブルの場合は、メモリ使用量が問題になることがあります。 たとえば、10億の場合のバケット数はそれぞれ、4 つのハッシュ インデックスのある 2億5千万行のテーブルと、ハッシュ テーブルのオーバーヘッドは、4 つのインデックス * 10億バケット\*8 バイト = 32 ギガバイトのメモリ使用率。 インデックスごとのバケット数に 2 億 5 千万個を選択すると、ハッシュ テーブルの合計オーバーヘッドは 8 GB です。 各インデックスはメモリ使用量の 8 バイトだけでなく、これは、このシナリオでは 8 ギガバイトである個々 の行を追加します (4 つのインデックス\*8 バイト\*2億5千万行の行)。  
  
 OLTP ワークロードのパフォーマンス クリティカル パスでは、フル テーブル スキャンは一般的ではありません。 そのため、メモリ使用量とポイント参照および挿入操作のパフォーマンスの間での選択になります。  
  
-   メモリ使用量を重視する場合は、インデックス キー値の数に近いバケット数を選択します。 バケット数は、インデックス キー値の数より大幅に小さくならないようにする必要があります。大幅に小さい場合、ほとんどの DML 操作や、サーバーの再起動後のデータベースの復旧に要する時間にも影響があります。  
  
-   ポイント参照のパフォーマンスを最適化する際は、一意のインデックス値の数の 2 ～ 3 倍のバケット数が適しています。 バケット数を大きくすると、メモリ使用量が増え、フル インデックス スキャンに必要な時間が増えます。  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルのインデックス](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
