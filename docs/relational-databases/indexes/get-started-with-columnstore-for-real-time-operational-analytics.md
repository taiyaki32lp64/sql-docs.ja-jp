---
title: 列ストアを使用したリアルタイム運用分析の概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: quickstart
ms.assetid: e1328615-6b59-4473-8a8d-4f360f73187d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2a242b02d14536036b53ee265413e28f5aeab231
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908025"
---
# <a name="get-started-with-columnstore-for-real-time-operational-analytics"></a>列ストアを使用したリアルタイム運用分析の概要
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  SQL Server 2016 にはリアルタイム運用分析が導入されており、同じデータベース テーブル上で分析ワークロードと OLTP ワークロードの両方を同時に実行できます。 分析をリアルタイムで実行するだけでなく、ETL やデータ ウェアハウスも不要になります。  
  
## <a name="real-time-operational-analytics-explained"></a>説明されているリアルタイム運用分析  
 従来、企業は運用 (OLTP) ワークロードと分析ワークロード用に別個のシステムを保有していました。 このようなシステムでは、抽出、変換、読み込み (ETL) ジョブにより、データを運用ストアから分析ストアに定期的に移動します。 分析データは通常、分析クエリを専門的に実行するデータ ウェアハウスやデータ マートに格納されています。 今まではこのソリューションが標準でしたが、主に 3 つの課題を抱えています。  
  
-   **複雑さ。** ETL の実装には、修正された行を読み込むだけでも大量のコーディングを必要とする場合があります。 変更された行を識別するのが困難なこともあります。  
  
-   **コスト。** ETL の実装には、追加のハードウェアやソフトウェアのライセンスを購入するためのコストが必要です。  
  
-   **データ待機時間。** ETL の実装により、分析の実行に時間遅延が発生します。 たとえば、ETL ジョブを各営業日の最後に実行する場合、分析クエリは少なくとも 1 日前のデータに対して実行されます。 多くの企業にとって、ビジネスの基盤はリアルタイムでデータを分析することにあるため、この遅延は許容されません。 たとえば、不正行為の検出には運用データに対するリアルタイムの分析が必要です。  
  
 ![リアルタイム運用分析の概要](../../relational-databases/indexes/media/real-time-operational-analytics-overview.png "リアルタイム運用分析の概要")  
  
 リアルタイム運用分析は、これらの課題を解決します。   
        分析ワークロードと OLTP ワークロードの実行の基になるテーブルが同じであるため、時間遅延は発生しません。   リアルタイム分析を使用できるシナリオでは、ETL が不要になり、別個のデータ ウェアハウスを購入して維持する必要がなくなるため、コストと複雑さが大幅に軽減されます。  
  
> [!NOTE]  
>  リアルタイム運用分析は、運用ワークロードと分析ワークロードの両方を実行できる、エンタープライズ リソース プランニング (ERP) アプリケーションなどの単一データソースのシナリオをターゲットにしています。 分析ワークロードを実行する前に複数のソースからのデータを統合する必要がある、またはキューブなどの事前集計データを使用して高度な分析パフォーマンスを必要とするときは、別個のデータ ウェアハウスが必要になることもあります。  
  
 リアルタイム分析は、行ストア テーブル上の更新可能な列ストア インデックスを使用します。  列ストア インデックスは、OLTP ワークロードと分析ワークロードが同じデータの別のコピーに対して実行されるように、データのコピーを管理します。 これにより、両方のワークロードを同時に実行してもパフォーマンス上の影響を最小限に抑えます。  SQL Server はインデックスの変更を自動的に管理するため、OLTP の変更が分析のために常に最新の状態に保たれます。 この設計により、最新のデータに対するリアルタイム分析を実現しています。 これは、ディスク ベース テーブルとメモリ最適化テーブルの両方で機能します。  
  
## <a name="get-started-example"></a>作業開始の例  
 リアルタイム分析を開始するには、次の手順に従います。  
  
1.  分析に必要なデータを含む、運用スキーマ内のテーブルを識別します。  
  
2.  各テーブルに、主に OLTP ワークロードでの既存の分析を高速化するために設計された BTree インデックスをすべてドロップします。 それらを単一の列ストア インデックスに置き換えます。  これにより、管理するインデックスの数が少なくなるため、OLTP ワークロードの全体的なパフォーマンスが向上します。  
  
    ```  
    --This example creates a nonclustered columnstore index on an existing OLTP table.  
    --Create the table  
    CREATE TABLE t_account (  
        accountkey int PRIMARY KEY,  
        accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int  
    );  
  
    --Create the columnstore index with a filtered condition  
    CREATE NONCLUSTERED COLUMNSTORE INDEX account_NCCI   
    ON t_account (accountkey, accountdescription, unitsold)   
    ;  
  
    ```  
  
     インメモリ テーブル上の列ストア インデックスは、インメモリ OLTP テクノロジとインメモリ列ストア テクノロジを統合することによって運用分析を実現し、OLTP ワークロードと分析ワークロードのパフォーマンスを高めます。 インメモリ テーブル上の列ストア インデックスには、すべての列が含まれている必要があります。  
  
    ```  
    -- This example creates a memory-optimized table with a columnstore index.  
    CREATE TABLE t_account (  
        accountkey int NOT NULL PRIMARY KEY NONCLUSTERED,  
        Accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int,  
        INDEX t_account_cci CLUSTERED COLUMNSTORE  
        )  
        WITH (MEMORY_OPTIMIZED = ON );  
    GO  
  
    ```  
  
3.  必要な操作はこれだけです。  

 アプリケーションに変更を加えることがなく、リアルタイム運用分析を実行する準備が整いました。  分析クエリは列ストア インデックスに対して実行され、OLTP 操作は OLTP BTree インデックスに対して継続的に実行されます。 OLTP ワークロードは引き続き実行されますが、列ストア インデックスの管理に追加のオーバーヘッドが発生します。 次のセクションでパフォーマンスの最適化について説明します。  
  
## <a name="blog-posts"></a>ブログ記事  
 リアルタイム運用分析については、Sunil Agarwal のブログ記事をご覧ください。  パフォーマンス ヒントのセクションが理解しやすくなるように、まずこちらのブログ記事を読むことをお勧めします。  
  
-   [リアルタイム運用分析のビジネス ケース](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)  
  
-   [非クラスター化列ストア インデックスを使用したリアルタイム運用分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)  
  
-   [非クラスター化列ストア インデックスの使用方法に関する簡単な例](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)  
  
-   [トランザクション ワークロードで SQL Server が非クラスター化列ストア インデックスを管理する方法](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)  
  
-   [フィルター処理されたインデックスを使用して非クラスター化列ストア インデックスのメンテナンスの影響を最小限に抑える](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)  
  
-   [圧縮遅延を使用して非クラスター化列ストア インデックスのメンテナンスの影響を最小限に抑える](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)  
  
-   [圧縮遅延を使用して非クラスター化列ストア インデックスのメンテナンスの影響を最小限に抑える - パフォーマンス番号](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)  
  
-   [メモリ最適化テーブルによるリアルタイム運用分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)  
  
-   [列ストア インデックスと行グループのマージ ポリシー](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
## <a name="performance-tip-1-use-filtered-indexes-to-improve-query-performance"></a>パフォーマンス ヒント 1:フィルター処理されたインデックスを使用したクエリ パフォーマンスの改善  
 リアルタイム分析の運用を実行すると、OLTP ワークロードのパフォーマンスに影響を及ぼすことがあります。  この影響は最小限に抑える必要があります。 次の例では、分析をリアルタイムで実行しつつ、フィルター処理されたインデックスを使用してトランザクション ワークロード上の非クラスター化列ストア インデックスの影響を最小限に抑える方法を示します。  
  
 運用ワークロード上で非クラスター化列ストア インデックスを管理するために必要なオーバーヘッドを最小限に抑えるには、フィルター処理条件を使用して *ウォーム* データ (緩やかに変化するデータ) 対してのみ非クラスター化列ストア インデックスを作成します。 たとえば、注文管理アプリケーションの場合、既に出荷されている注文に対して非クラスター化列ストア インデックスを作成できます。 注文が出荷された後はほとんど変化しないため、ウォーム データと捉えることができます。 フィルター処理されたインデックスを使用すると、非クラスター化列ストア インデックスのデータに必要な更新プログラムの数が少なくなるため、トランザクション ワークロードへの影響が少なくなります。  
  
 分析クエリは、ウォーム データおよび必要に応じてホット データに透過的にアクセスすることでリアルタイム分析を提供します。 運用ワークロードの大部分が「ホット」データと接触している場合、それらの操作に対して列ストア インデックスの追加メンテナンスは不要です。 ベスト プラクティスは、列の行ストア クラスター化インデックスをフィルター処理されたインデックス定義に使用することです。   SQL Server は、クラスター化インデックスを使用してフィルター処理条件を満たしていない行を迅速にスキャンします。 このクラスター化インデックスがない場合、これらの行を探すには行ストア テーブルのフル テーブル スキャンが必要になり、分析クエリのパフォーマンスに多大な悪影響を及ぼすことがあります。 クラスター化インデックスが存在しない場合は、補足的にフィルター処理された非クラスター化 BTree インデックスを作成してそのような行を特定できますが、非クラスター化 BTree インデックスを通じた広範囲の行に対するアクセスは高コストであるため、お勧めしません。  
  
> [!NOTE]  
>  フィルター処理された非クラスター化列ストア インデックスは、ディスク ベースのテーブルに対してのみサポートされます。 メモリ最適化テーブルではサポートされていません。  
  
### <a name="example-a-access-hot-data-from-btree-index-warm-data-from-columnstore-index"></a>例 A:BTree インデックスからホット データ、列ストア インデックスからウォーム データにアクセスする  
 この例では、フィルター処理条件 (accountkey > 0) を使用して、列ストア インデックスに含まれる行を確立します。 目標は、フィルター処理条件と後続のクエリを設計し、頻繁に変化する BTree インデックスからの "ホット" データにアクセスする、およびより安定した列ストア インデックスからの "ウォーム" データにアクセスすることです。  
  
 ![ウォーム データとホット データの結合インデックス](../../relational-databases/indexes/media/de-columnstore-warmhotdata.png "ウォーム データとホット データの結合インデックス")  
  
> [!NOTE]  
>  クエリ オプティマイザーはクエリ プランの列ストア インデックスを考慮しますが、常に選択するわけではありません。 クエリ オプティマイザーがフィルター処理された列ストア インデックスを選択すると、列ストア インデックスからの行とフィルター処理条件を満たしていない行を透過的に結合され、リアルタイム分析を実現します。 これは、通常のフィルター処理された非クラスター インデックスとは異なり、インデックスに存在する行に限定されたクエリでのみ使用できます。  
  
```  
--Use a filtered condition to separate hot data in a rowstore table  
-- from "warm" data in a columnstore index.  
  
-- create the table  
CREATE TABLE  orders (  
         AccountKey         int not null,  
         Customername       nvarchar (50),  
        OrderNumber         bigint,  
        PurchasePrice       decimal (9,2),  
        OrderStatus         smallint not null,  
        OrderStatusDesc     nvarchar (50))  
  
-- OrderStatusDesc  
-- 0 => 'Order Started'  
-- 1 => 'Order Closed'  
-- 2 => 'Order Paid'  
-- 3 => 'Order Fullfillment Wait'  
-- 4 => 'Order Shipped'  
-- 5 => 'Order Received'  
  
CREATE CLUSTERED INDEX  orders_ci ON orders(OrderStatus)  
  
--Create the columnstore index with a filtered condition  
CREATE NONCLUSTERED COLUMNSTORE INDEX orders_ncci ON orders  (accountkey, customername, purchaseprice, orderstatus)  
where orderstatus = 5  
;  
  
-- The following query returns the total purchase done by customers for items > $100 .00  
-- This query will pick  rows both from NCCI and from 'hot' rows that are not part of NCCI  
SELECT top 5 customername, sum (PurchasePrice)  
FROM orders  
WHERE purchaseprice > 100.0   
Group By customername  
```  
  
 分析クエリは、次のクエリ プランで実行されます。 フィルター処理条件を満たしていない行には、クラスター化 BTree インデックスを通じてアクセスされます。  
  
 ![クエリ プラン](../../relational-databases/indexes/media/query-plan-columnstore.png "クエリ プラン")  
  
 [フィルター処理された非クラスター化列ストア インデックス](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)の詳細については、ブログを参照してください。  
  
## <a name="performance-tip-2-offload-analytics-to-always-on-readable-secondary"></a>パフォーマンス ヒント 2:AlwaysOn 読み取り可能セカンダリに対する分析の負荷を軽減する  
 列ストア インデックスのメンテナンスはフィルター処理された列ストア インデックスを使用して最小限に抑えることはできますが、それでも分析クエリには多大なコンピューティング リソース (CPU、IO、メモリ) が必要であり、運用ワークロードのパフォーマンスに影響します。 ほとんどのミッション クリティカルなワークロードについては、AlwaysOn 構成を使用することをお勧めします。 この構成では、負荷を読み取り可能セカンダリにオフロードすることで、実行中の分析の影響を除去できます。  
  
## <a name="performance-tip-3-reducing-index-fragmentation-by-keeping-hot-data-in-delta-rowgroups"></a>パフォーマンス ヒント 3:ホット データを DELTA 行グループに保持することでインデックスの断片化を削減する  
 圧縮された行がワークロードによって更新/削除された場合、列ストア インデックスのあるテーブルは (削除された行によって) 大幅に断片化されることがあります。 断片化された列ストア インデックスは、メモリと記憶域の非効率的な使用につながります。 リソースの非効率的な使用だけでなく、余分な IO と結果セットから削除された行をフィルター処理する必要があるため、分析クエリのパフォーマンスにも悪影響を及ぼします。  
  
 削除された行は、REORGANIZE コマンドを使用してインデックスのデフラグを実行するか、テーブル全体または影響を受けているパーティションの列ストア インデックスを再構築するまで、物理的には削除されません。 REORGANIZE とインデックスの REBUILD は高コストな操作であり、ワークロードに使用されるリソースを取り除きます。 さらに、行の圧縮が早すぎる場合は、更新により何度も再圧縮する必要性が出てくるため、無駄な圧縮によるオーバーヘッドにつながる可能性があります。  
インデックスの断片化は、COMPRESSION_DELAY オプションを使用して最小限に抑えることができます。  
  
```  
  
-- Create a sample table  
create table t_colstor (  
               accountkey                      int not null,  
               accountdescription              nvarchar (50) not null,  
               accounttype                     nvarchar(50),  
               accountCodeAlternatekey         int)  
  
-- Creating nonclustered columnstore index with COMPRESSION_DELAY. The columnstore index will keep the rows in closed delta rowgroup for 100 minutes   
-- after it has been marked closed  
CREATE NONCLUSTERED COLUMNSTORE index t_colstor_cci on t_colstor (accountkey, accountdescription, accounttype)   
                       WITH (DATA_COMPRESSION= COLUMNSTORE, COMPRESSION_DELAY = 100);  
  
;  
```  
  
 [圧縮遅延](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)の詳細については、ブログを参照してください。  
  
 推奨されているベスト プラクティスを次に示します。  
  
-   **挿入/クエリ ワークロード:** ワークロードで主にデータを挿入してクエリを実行する場合、COMPRESSION_DELAY オプションは既定の 0 のままにすることをお勧めします。 単一の DELTA 行グループに 100 万行が挿入されると、新しく挿入された行が圧縮されます。  
    このようなワークロードの例としては、(a) 従来の DW ワークロード (b) クリック ストリーム分析 (Web アプリケーションのクリック パターンの分析) が挙げられます。  
  
-   **OLTP ワークロード:** ワークロードに大量の DML (更新、削除、挿入が混在) がある場合、DMV の sys. dm_db_column_store_row_group_physical_stats を分析することで列ストア インデックスの断片化が見られることがあります。 10% を上回る行が最近圧縮された行グループで削除済みとマークされている場合、行を圧縮できるタイミングで COMPRESSION_DELAY オプションを使用して時間遅延を追加できます。 たとえば、ワークロードで新しく挿入された行が 60 分間 "ホット" な状態にある (複数回更新される) 場合は、COMPRESSION_DELAY を 60 にすることをお勧めします。  
  
 ほとんどのお客様は何もする必要がないことを想定しています。 COMPRESSION_DELAY オプションの既定値で問題なく動作するはずです。  
上級ユーザーの場合は、以下のクエリを実行して過去 7 日間で削除された行の割合を収集することをお勧めします。  
  
```  
SELECT row_group_id,cast(deleted_rows as float)/cast(total_rows as float)*100 as [% fragmented], created_time  
FROM sys. dm_db_column_store_row_group_physical_stats  
WHERE object_id = object_id('FactOnlineSales2')   
             AND  state_desc='COMPRESSED'   
             AND deleted_rows>0   
             AND created_time > GETDATE() - 7  
ORDER BY created_time DESC  
```  
  
 圧縮された行グループで削除された行の数が 20% を超える場合、それより前の行グループを 5% 以下のバリエーション (コールド グループと呼ばれます) で平坦化することで、COMPRESSION_DELAY = (youngest_rowgroup_created_time -  current_time) に設定します。 このアプローチは、安定性が高く比較的同種のワークロードに最適です。  
  
## <a name="see-also"></a>参照  
 [列ストア インデックス ガイド](../../relational-databases/indexes/columnstore-indexes-overview.md)   
 [列ストア インデックス データの読み込み](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [列ストア インデックスのクエリ パフォーマンス](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [データ ウェアハウスの列ストア インデックス](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)
  
