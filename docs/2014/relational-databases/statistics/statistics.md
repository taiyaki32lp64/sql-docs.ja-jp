---
title: 統計 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cc9657d8db84b67abe324aea9614dd27c2d9df83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033730"
---
# <a name="statistics"></a>統計
  クエリ オプティマイザーでは、クエリのパフォーマンスを向上させるクエリ プランを作成するために統計を使用します。 ほとんどのクエリでは、高品質のクエリ プランに必要な統計がクエリ オプティマイザーによって既に生成されていますが、最適な結果を得るために追加の統計情報を作成したりクエリのデザインを変更したりする必要がある場合もあります。 このトピックでは、クエリ最適化に関する統計の概念と、それを効果的に使用するためのガイドラインについて説明します。  
  
##  <a name="DefinitionQOStatistics"></a> コンポーネントおよび概念  
 統計  
 クエリ最適化に関する統計は、テーブルまたはインデックス付きビューの 1 つまたは複数の列の値の分布に関する統計情報を格納するオブジェクトです。 クエリ オプティマイザーでは、これらの統計を使用してクエリ結果の *カーディナリティ*、つまり行数を推定します。 これらの *カーディナリティの推定* に基づいて、クエリ オプティマイザーでは高品質なクエリ プランを作成できます。 たとえば、クエリ オプティマイザーでは、カーディナリティの推定に基づいて、リソースの消費が多い Index Scan 操作ではなく Index Seek 操作が使用される場合があります。この場合、クエリのパフォーマンスが向上します。  
  
 統計オブジェクトは 1 つ以上のテーブル列で構成されるリストごとに作成され、それぞれに最初の列の値の分布を示すヒストグラムが含まれます。 複数列の統計オブジェクトには、さらに、列間の値の相関関係に関する統計情報も格納されます。 これらの相関関係の統計情報 ( *密度*) は、個別の列値を持つ行の数から得られます。 統計オブジェクトの詳細については、「[DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)」を参照してください。  
  
 フィルター選択された統計情報  
 適切に定義されたデータのサブセットから選択するクエリでは、フィルター選択された統計情報を使用するとクエリのパフォーマンスを向上させることができます。 フィルター選択された統計情報では、統計情報に含まれるデータのサブセットを選択するためにフィルター述語を使用します。 統計情報を適切にフィルター選択すると、テーブル全体の統計情報を使用する場合と比べて、クエリ実行プランが向上します。 フィルター述語の詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)」を参照してください。 フィルター選択された統計情報を作成する場合の詳細については、このトピックの「 [統計を作成する場合](#UpdateStatistics) 」を参照してください。 ケース スタディについては、SQLCAT Web サイトのブログ「 [Using Filtered Statistics with Partitioned Tables](https://go.microsoft.com/fwlink/?LinkId=178505)」(英語) を参照してください。  
  
 統計オプション  
 統計の作成と更新のタイミングおよび方法を指定するための 3 つのオプションを設定できます。 これらのオプションは、データベース レベルでのみ設定されます。  
  
 AUTO_CREATE_STATISTICS オプション  
 統計の自動作成オプション AUTO_CREATE_STATISTICS がオンの場合、クエリ プランのカーディナリティの推定を向上させるために、クエリ オプティマイザーによってクエリ述語内の個々の列に関する統計が必要に応じて作成されます。 これらの 1 列ずつの統計は、既存の統計オブジェクトにまだヒストグラムがない列について作成されます。 AUTO_CREATE_STATISTICS オプションでは、インデックスに対する統計を作成するかどうかは判断されません。 また、フィルター選択された統計情報も生成されません。 このオプションは、テーブル全体の 1 列ずつの統計にのみ適用されます。  
  
 AUTO_CREATE_STATISTICS オプションを使用した結果としてクエリ オプティマイザーによって統計が作成された場合、その統計名は `_WA`で始まります。 次のクエリを使用すると、クエリ オプティマイザーでクエリ述語列の統計が作成されたかどうかを判断できます。  
  
```  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
 AUTO_UPDATE_STATISTICS オプション  
 統計の自動更新オプション AUTO_UPDATE_STATISTICS がオンの場合、古くなっている可能性がある統計がクエリ オプティマイザーによって判断され、それらがクエリで使用されると更新されます。 挿入、更新、削除、またはマージの各操作によってテーブルまたはインデックス付きビューのデータの分布が変わると、統計は古くなったと判断されます。 クエリ オプティマイザーでは、統計が前回更新されてから発生したデータ変更の数をカウントし、その変更の数をしきい値と比較することで、統計が古くなっている可能性がないかを判断します。 このしきい値は、テーブルまたはインデックス付きビューの行数に基づいて決められます。  
  
 クエリ オプティマイザーによる古い統計の確認は、クエリをコンパイルする前と、キャッシュされたクエリ プランを実行する前に行われます。 クエリをコンパイルする前は、クエリ オプティマイザーで、クエリ述語内の列、テーブル、およびインデックス付きビューを使用して古くなっている可能性がある統計が判断されます。 キャッシュされたクエリ プランを実行する前は、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] で、クエリ プランが最新の統計を参照しているかどうかが確認されます。  
  
 AUTO_UPDATE_STATISTICS オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) ステートメントを使用して作成された統計に適用されます。 また、フィルター選択された統計情報にも適用されます。  
  
 AUTO_UPDATE_STATISTICS_ASYNC  
 統計の非同期更新オプション AUTO_UPDATE_STATISTICS_ASYNC によって、クエリ オプティマイザーで統計の同期更新と非同期更新のどちらを使用するかが決まります。 既定では、統計の非同期更新オプションはオフであり、クエリ オプティマイザーによる統計の更新は同期更新になります。 AUTO_UPDATE_STATISTICS_ASYNC オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) ステートメントを使用して作成された統計に適用されます。  
  
 統計の更新には、同期更新 (既定) と非同期更新があります。 統計の同期更新では、クエリは常に最新の統計を使用してコンパイルおよび実行されます。統計が古い場合、クエリ オプティマイザーでは、統計が更新されるまでクエリのコンパイルおよび実行を待機します。 統計の非同期更新では、クエリは、既存の統計が古い場合でもその統計を使用してコンパイルされます。クエリのコンパイル時に古い統計が使用された場合、クエリ オプティマイザーで最適なクエリ プランが選択されない可能性があります。 非同期更新の完了後にコンパイルされるクエリには、更新された統計を使用できます。  
  
 テーブルの切り捨てや大部分の行の一括更新を行うなど、データの分布が変わる操作を実行する場合は、同期統計を使用することを検討してください。 操作が完了した後に統計を更新していない場合、同期統計を使用すれば、変更されたデータに対するクエリを実行する前に統計が最新になります。  
  
 次のような場合は、非同期統計を使用してクエリの応答時間を予測しやすくすることを検討してください。  
  
-   アプリケーションで同じクエリ、類似のクエリ、またはキャッシュされた類似のクエリ プランを頻繁に実行する場合。 クエリの応答時間は、統計の同期更新を使用するよりも非同期更新を使用した方が予測しやすくなります。非同期更新の場合、クエリ オプティマイザーでは、統計が最新になるまで待機せずに着信クエリを実行できるためです。 これにより、一部のクエリの遅延については回避することができます。  
  
-   アプリケーションで統計の更新を待機している 1 つ以上のクエリによって、クライアント要求がタイムアウトする場合。 場合によっては、同期統計を待機していることが原因で、厳しいタイムアウト時間が設定されたアプリケーションが失敗することがあります。  
  
 INCREMENTAL STATS  
 ON の場合、作成される統計はパーティションごとの統計です。 OFF の場合、統計ツリーが削除され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって統計が再計算されます。 既定値は OFF です。 この設定は、データベース レベルの INCREMENTAL プロパティをオーバーライドします。  
  
 大きなテーブルに新しいパーティションを追加した場合、新しいパーティションが含まれるように統計を更新する必要があります。 ただし、テーブル全体のスキャン (FULLSCAN または SAMPLE オプション) に要する時間は非常に長くなることがあります。 また、新しいパーティションに対する統計のみが必要となるため、テーブル全体をスキャンする必要はありません。 増分オプションでは、パーティションごとの統計が作成され格納されるため、更新時には、新しい統計を必要とするそれらのパーティションの統計のみを更新します。  
  
 パーティションごとの統計がサポートされていない場合、このオプションは無視され、警告が生成されます。 次の種類の統計では、増分統計がサポートされていません。  
  
-   ベース テーブルにパーティションで固定されていないインデックスを使用して作成された統計。  
  
-   AlwaysOn の読み取り可能なセカンダリ データベースに対して作成された統計。  
  
-   読み取り専用のデータベースに対して作成された統計。  
  
-   フィルター選択されたインデックスに対して作成された統計。  
  
-   ビューに対して作成された統計。  
  
-   内部テーブルに対して作成された統計。  
  
-   空間インデックスまたは XML インデックスを使用して作成された統計。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
##  <a name="CreateStatistics"></a> 統計を作成する場合  
 クエリ オプティマイザーによって、既に次のようにして統計が作成されています。  
  
1.  インデックスの作成時に、クエリ オプティマイザーによってテーブルまたはビューのインデックスに対する統計が作成されます。 これらの統計は、インデックスのキー列について作成されます。 インデックスがフィルター選択されたインデックスの場合は、フィルター選択されたインデックスに指定された行のサブセットと同じ行のサブセットについて、フィルター選択された統計が作成されます。 フィルター選択されたインデックスの詳細については、「[フィルター選択されたインデックスの作成](../indexes/create-filtered-indexes.md)」および 「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。  
  
2.  AUTO_CREATE_STATISTICS がオンの場合、クエリ オプティマイザーによってクエリ述語内の列に対して 1 列ずつ統計が作成されます。  
  
 ほとんどのクエリでは、これらの 2 つの方法で作成された統計を使用すれば、高品質のクエリ プランになります。ただし、 [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) ステートメントを使用して追加の統計を作成することで、クエリ プランが向上する場合もあります。 これらの追加の統計では、クエリ オプティマイザーでインデックスまたは 1 列ずつの統計を作成する場合には考慮されない統計的相関関係を取り込むことができます。 アプリケーションのテーブル データには、計算して統計オブジェクトに含めればクエリ オプティマイザーでクエリ プランを向上させることができる、他の統計的相関関係が含まれている場合があります。 たとえば、データ行のサブセットに関するフィルター選択された統計情報や、クエリ述語列の複数列統計を使用することで、クエリ プランが向上することがあります。  
  
 CREATE STATISTICS ステートメントを使用して統計を作成する場合、AUTO_CREATE_STATISTICS オプションをオンのままにし、クエリ述語列に対する 1 列ずつの統計がクエリ オプティマイザーによって通常どおり作成されるようにしておくことをお勧めします。 クエリ述語の詳細については、「[検索条件 &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql)」を参照してください。  
  
 次のいずれかに該当する場合は、CREATE STATISTICS ステートメントを使用して統計を作成することを検討してください。  
  
-   [!INCLUDE[ssDE](../../../includes/ssde-md.md)] チューニング アドバイザーで統計を作成するように提示される。  
  
-   相関関係にある複数の列がクエリ述語に含まれているが、それらがまだ同じインデックスに存在しない。  
  
-   データのサブセットから選択するクエリを使用する。  
  
-   クエリに統計がない。  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>相関関係にある複数の列がクエリ述語に含まれている  
 列間に相関関係や依存関係がある複数の列がクエリ述語に含まれている場合、複数列の統計を使用するとクエリ プランが向上することがあります。 複数列の統計には、 *密度*と呼ばれる列間の相関関係の統計が含まれます。これは、1 列ずつの統計では使用できません。 複数の列間のデータの相関関係によってクエリ結果が異なる場合、密度を使用するとカーディナリティの推定が向上します。  
  
 列が同じインデックスに既に存在する場合、複数列統計オブジェクトは既に存在するため、手動で作成する必要はありません。 列が同じインデックスにまだ存在しない場合は、列のインデックスを作成するか CREATE STATISTICS ステートメントを使用することによって、複数列統計を作成できます。 メンテナンスに必要なシステム リソースは、インデックスの方が統計オブジェクトよりも多くなります。 複数列のインデックスを必要としないアプリケーションの場合は、インデックスを作成せずに統計オブジェクトを作成すると、システム リソースを節約できます。  
  
 複数列統計を作成する場合、統計オブジェクト定義内の列の順序によって、カーディナリティの推定に密度を使用した場合の効果が変わります。 統計オブジェクトには、統計オブジェクト定義内のキー列の各プレフィックスの密度が格納されます。 密度については、「[DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)」を参照してください。  
  
 カーディナリティの推定に効果的な密度を作成するには、クエリ述語内の列が、統計オブジェクト定義内の列のいずれかのプレフィックスに一致する必要があります。 たとえば、次の例では、列 `LastName`、 `MiddleName`、および `FirstName`に対する複数列統計オブジェクトを作成しています。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 この例では、統計オブジェクト `LastFirst` に、列プレフィックス (`LastName`)、(`LastName, MiddleName`)、および (`LastName, MiddleName, FirstName`) の密度が格納されています。 (`LastName, FirstName`) の密度は使用できません。 `LastName` を使用せずに `FirstName` と `MiddleName` を使用したクエリの場合は、カーディナリティの推定に密度を使用することはできません。  
  
### <a name="query-selects-from-a-subset-of-data"></a>データのサブセットから選択するクエリを使用する  
 クエリ オプティマイザーでは、1 列ずつおよびインデックスに対して統計を作成する際、すべての行の値に対する統計を作成します。 行のサブセットから選択するクエリの場合、その行のサブセットのデータ分布が一意であれば、フィルター選択された統計情報を使用することでクエリ プランを向上させることができます。 フィルター選択された統計情報は、CREATE STATISTICS ステートメントを WHERE 句と共に使用してフィルター述語の式を定義することで作成できます。  
  
 たとえばを使用して[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]、Production.ProductCategory テーブルの 4 つのカテゴリのいずれかに属している、Production.Product テーブルに各製品。Bikes、Components、Clothing、Accessories。 各カテゴリでは、重量に関するデータ分布が異なります。自転車の重量は 13.77 ～ 30.0、部品の重量は 2.12 ～ 1050.00 (一部 NULL 値)、衣類の重量はすべて NULL、付属品の重量も NULL です。  
  
 たとえば Bikes の場合、自転車のすべての重量についてのフィルター選択された統計情報を使用すると、テーブル全体の統計情報を使用する場合や、Weight 列の統計情報が存在しない場合と比べて、より正確な統計情報がクエリ オプティマイザーに提供され、クエリ プランの品質が向上します。 自転車の重量の列は、フィルター選択された統計情報には適していますが、重量の参照が比較的少ない場合、フィルター選択されたインデックスには必ずしも適しているとは限りません。 フィルター選択されたインデックスを使用することで得られる参照のパフォーマンスの向上よりも、フィルター選択されたインデックスをデータベースに追加するためのメンテナンス コストとストレージ コストの増加の方が大きい場合があります。  
  
 次のステートメントでは、Bikes のすべてのサブカテゴリについてのフィルター選択された統計 `BikeWeights` を作成します。 フィルター選択された述語式で、比較 `Production.ProductSubcategoryID IN (1,2,3)`を使用して自転車のすべてのサブカテゴリを列挙することで、自転車を定義しています。 Bikes カテゴリは Production.ProductCategory テーブルに格納されているため、述語でそのカテゴリ名を使用することはできません。フィルター式に含まれるすべての列が、同じテーブル内に存在する必要があります。  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../snippets/tsql/SQL14/tsql/statisticsddl/transact-sql/filteredstats.sql#filteredstats2)]  
  
 クエリ オプティマイザーでは、 `BikeWeights` というフィルター選択された統計情報を使用して、重量が `25`を超えるすべての自転車を選択する次のクエリのクエリ プランを向上させることができます。  
  
```  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>統計がないことをクエリで識別する  
 クエリ オプティマイザーでは、エラーやその他のイベントによって統計を作成できない場合、統計を使用せずにクエリ プランを作成します。 クエリ オプティマイザーでは存在しない統計をマークし、次回のクエリの実行時に再生成しようとします。  
  
 統計が存在しない場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してクエリの実行プランをグラフィカルに表示すると、警告 (赤色のテーブル名) が表示されます。 また、 **を使用して** Missing Column Statistics [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] イベント クラスを監視すると、統計がない場合はそのことがわかります。 詳細については、「[Errors and Warnings イベント カテゴリ &#40;データベース エンジン&#41;](../event-classes/errors-and-warnings-event-category-database-engine.md)」を参照してください。  
  
 統計がない場合は、次の手順を実行します。  
  
-   AUTO_CREATE_STATISTICS と AUTO_UPDATE_STATISTICS がオンになっていることを確認します。  
  
-   データベースが読み取り専用ではないことを確認します。 データベースが読み取り専用の場合、クエリ オプティマイザーでは統計を保存できません。  
  
-   存在しない統計を CREATE STATISTICS ステートメントを使用して作成します。  
  
 読み取り専用データベースまたは読み取り専用スナップショットに関する統計が欠落しているか、古くなっている場合、[!INCLUDE[ssDE](../../../includes/ssde-md.md)]は、`tempdb` に一時的な統計を作成して維持します。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] で一時的な統計を作成する場合は、一時的な統計と永続的な統計とを区別するためのサフィックス _readonly_database_statistic が統計名に付加されます。 サフィックス _readonly_database_statistic は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によって生成される統計用に予約されています。 読み書き可能なデータベースでは、一時的な統計用のスクリプトを作成して再現できます。 スクリプトを作成する場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、統計名のサフィックスを _readonly_database_statistic から _readonly_database_statistic_scripted に変更します。  
  
 一時的な統計を作成して更新できるのは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のみです。 ただし、永続的な統計の場合と同じツールを使用すると、一時的な統計を削除して、統計のプロパティを監視できます。  
  
-   [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) ステートメントを使用して作成された統計に適用されます。  
  
-   **sys.stats** カタログ ビューと **sys.stats_columns** カタログ ビューを使用して統計を監視します。 **sys_stats** には、どの統計が一時的または永続的なものかを示すための **is_temporary** 列が含まれています。  
  
 一時的な統計は `tempdb` に格納されるので、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを再起動すると、一時的な統計がすべて表示されなくなります。  
  
##  <a name="UpdateStatistics"></a> 統計を更新する場合  
 クエリ オプティマイザーでは、古くなっている可能性がある統計を判断し、それらがクエリ プランに必要な場合は更新します。 場合によっては、AUTO_UPDATE_STATISTICS をオンにした場合より頻繁に統計を更新することで、クエリ プランが向上し、クエリのパフォーマンスが向上することがあります。 統計は、UPDATE STATISTICS ステートメントまたは sp_updatestats ストアド プロシージャを使用して更新できます。  
  
 統計を更新すると、クエリが最新の統計を使用してコンパイルされるようになります。 ただし、統計の更新によりクエリが再コンパイルされます。 パフォーマンスの向上を目的とする場合、クエリ プランの改善とクエリの再コンパイルに要する時間の間にはトレードオフの関係があるため、あまり頻繁に統計を更新しないようにすることをお勧めします。 実際のトレードオフはアプリケーションによって異なります。  
  
 UPDATE STATISTICS または sp_updatestats を使用して統計を更新する場合、AUTO_UPDATE_STATISTICS オプションを ON に設定したままにし、通常の更新がクエリ オプティマイザーによって引き続き行われるようにしておくことをお勧めします。 列、インデックス、テーブル、またはインデックス付きビューの統計を更新する方法については、「[UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)」を参照してください。 データベース内のすべてのユーザー定義および内部テーブルの統計を更新する方法については、ストアド プロシージャ [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) の説明を参照してください。  
  
 統計の最終更新日を調べるには、 [STATS_DATE](/sql/t-sql/functions/stats-date-transact-sql) 関数を使用します。  
  
 次のような場合は、統計を更新することを検討してください。  
  
-   クエリの実行に時間がかかる。  
  
-   昇順または降順のキー列に対して挿入操作を実行する。  
  
-   メンテナンス操作の実行後。  
  
### <a name="query-execution-times-are-slow"></a>クエリの実行に時間がかかる  
 クエリの応答時間が遅い場合や予測できない場合は、他のトラブルシューティング手順を実行する前に、クエリの統計が最新のものであることを確認してください。  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>昇順または降順のキー列に対して挿入操作を実行する  
 昇順または降順のキー列 (IDENTITY 列や実時間のタイムスタンプ列など) の統計では、クエリ オプティマイザーで実行されるよりも頻繁に統計の更新が必要になる場合があります。 挿入操作によって昇順または降順の列に新しい値が追加された場合に、 追加された行数が少なすぎると、統計の更新が実行されないことがあります。 統計が最新ではない場合に、追加された最新の行から選択するクエリを実行すると、現在の統計にそれらの新しい値のカーディナリティの推定が含まれません。 その結果、カーディナリティの推定が不正確になり、クエリのパフォーマンスが低下することがあります。  
  
 たとえば、最新の販売注文日から選択するクエリで、統計が最新の販売注文日のカーディナリティの推定を含むように更新されていないと、カーディナリティの推定が不正確になります。  
  
### <a name="after-maintenance-operations"></a>メンテナンス操作の実行後  
 テーブルの切り捨てや大部分の行の一括挿入を行うなど、データの分布が変わるメンテナンス操作を実行した後は、統計を更新することを検討してください。 これにより、統計の自動更新を待つことによってクエリ処理で発生する以降の遅延を回避することができます。  
  
 インデックスの再構築、デフラグ、再構成などの操作では、データの分布は変わりません。 そのため、ALTER INDEX REBUILD、DBCC REINDEX、DBCC INDEXDEFRAG、または ALTER INDEX REORGANIZE の各操作を実行した後に統計を更新する必要はありません。 ALTER INDEX REBUILD または DBCC DBREINDEX を使用してテーブルまたはビューのインデックスを再構築した場合、クエリ オプティマイザーによって統計が更新されますが、この統計の更新はインデックスを再作成する過程で実行されるものです。 DBCC INDEXDEFRAG 操作または ALTER INDEX REORGANIZE 操作の後は、クエリ オプティマイザーで統計は更新されません。  
  
##  <a name="DesignStatistics"></a> 統計を効果的に使用するクエリ  
 クエリ述語にローカル変数や複雑な式が含まれている場合など、特定のクエリ実装では、最適なクエリ プランにならないことがあります。 クエリのデザイン ガイドラインに従って統計を効果的に使用することで、この問題を回避できる場合があります。 クエリ述語の詳細については、「[検索条件 &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql)」を参照してください。  
  
 クエリのデザイン ガイドラインを適用して統計を効果的に使用することで、クエリ述語で使用される式、変数、および関数に対する *カーディナリティの推定* を向上させると、クエリ プランを向上させることができます。 クエリ オプティマイザーでは、式、変数、または関数の値が不明な場合、ヒストグラムで参照する値を特定できないため、ヒストグラムから最適なカーディナリティの推定を得ることができません。 その場合、クエリ オプティマイザーでは、ヒストグラム内のサンプリングされたすべての行の値ごとの平均行数に基づいてカーディナリティの推定を行います。 その結果、カーディナリティが適切に推定されず、クエリのパフォーマンスが低下することがあります。  
  
 以下のガイドラインでは、カーディナリティの推定を向上させることによってクエリ プランを改善するためのクエリの作成方法について説明します。  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>式に対するカーディナリティの推定を向上させる  
 式に対するカーディナリティの推定を向上させるには、次のガイドラインに従います。  
  
-   定数を含む式は可能な限り単純にします。 クエリ オプティマイザーでは、カーディナリティの推定を判断する前に、定数を含むすべての関数および式の評価は行われません。 たとえば、式 ABS(`-100) to 100`を簡略化します。  
  
-   式で複数の変数を使用している場合は、式の計算列を作成し、その計算列に対する統計またはインデックスを作成することを検討します。 たとえば、クエリ述語 `WHERE PRICE + Tax > 100` のカーディナリティの推定は、式 `Price + Tax` に対する計算列を作成すると向上する可能性があります。  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>変数および関数に対するカーディナリティの推定を向上させる  
 変数および関数に対するカーディナリティの推定を向上させるには、次のガイドラインに従います。  
  
-   クエリ述語でローカル変数を使用している場合は、ローカル変数の代わりにパラメーターを使用してクエリを書き換えることを検討します。 ローカル変数の値は、クエリ オプティマイザーでのクエリ実行プランの作成時には認識されません。 クエリでパラメーターを使用すると、クエリ オプティマイザーで、ストアド プロシージャに渡される最初の実際のパラメーター値に対するカーディナリティの推定が使用されます。  
  
-   複数ステートメントのテーブル値関数の結果を格納する場合は、標準のテーブルか一時テーブルを使用することを検討します。 クエリ オプティマイザーでは、複数ステートメントのテーブル値関数の統計は作成されません。 この方法を使用すると、クエリ オプティマイザーでテーブル列の統計を作成できるため、それを使用することでクエリ プランを向上させることができます。  
  
-   テーブル変数の代わりに標準のテーブルか一時テーブルを使用することを検討します。 クエリ オプティマイザーでは、テーブル変数の統計は作成されません。 この方法を使用すると、クエリ オプティマイザーでテーブル列の統計を作成できるため、それを使用することでクエリ プランを向上させることができます。 一時テーブルとテーブル変数のどちらを使用するかの判断には、トレードオフの関係があります。ストアド プロシージャでテーブル変数を使用すると、ストアド プロシージャの再コンパイルの回数が、一時テーブルを使用した場合よりも少なくなります。 アプリケーションによっては、テーブル変数の代わりに一時テーブルを使用しても、パフォーマンスが向上しない場合もあります。  
  
-   渡されたパラメーターを使用するクエリがストアド プロシージャに含まれている場合は、パラメーター値がクエリで使用される前にストアド プロシージャ内で変更されないようにします。 クエリに対するカーディナリティの推定は、更新された値ではなく渡されたパラメーターの値に基づいて行われます。 パラメーター値が変更されないようにするには、2 つのストアド プロシージャを使用するようにクエリを書き換えます。  
  
     たとえば、次のストアド プロシージャ `Sales.GetRecentSales` では、パラメーター `@date` の場合に `@date is NULL`の値を変更します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     ストアド プロシージャ `Sales.GetRecentSales` の最初の呼び出しで `@date` パラメーターに NULL が渡された場合、クエリ オプティマイザーでは、クエリ述語が `@date = NULL` で呼び出されていなくても、`@date = NULL` に対するカーディナリティの推定を使用してストアド プロシージャをコンパイルします。 このカーディナリティの推定は、実際のクエリ結果の行数と大きく異なる場合があります。 そのため、クエリ オプティマイザーにより、最適なクエリ プランが選択されないことがあります。 この問題を回避するには、ストアド プロシージャを次のように 2 つのプロシージャに書き換えます。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>クエリ ヒントを使用してカーディナリティの推定を向上させる  
 ローカル変数に対するカーディナリティの推定を向上させるために、RECOMPILE を指定して OPTIMIZE FOR または OPTIMIZE FOR UNKNOWN クエリ ヒントを使用することができます。 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)」を参照してください。  
  
 アプリケーションによっては、クエリを実行するたびに再コンパイルすると時間がかかりすぎる場合がありますが、 OPTIMIZER FOR クエリ ヒントは RECOMPILE オプションを使用しなくても役立つことがあります。 たとえば、ストアド プロシージャ Sales.GetRecentSales に OPTIMIZER FOR オプションを追加して、特定の日付を指定することができます。 Sales.GetRecentSales プロシージャに OPTIMIZE FOR を追加した例を次に示します。  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>プラン ガイドを使用してカーディナリティの推定を向上させる  
 アプリケーションによっては、クエリを変更できない場合や、RECOMPILE クエリ ヒントを使用すると再コンパイルが多くなりすぎる場合など、クエリのデザイン ガイドラインを適用できないことがあります。 プラン ガイドを使用すると、アプリケーション ベンダーによるアプリケーションの違いを確認しながら、その他のヒント (USE PLAN など) を指定してクエリの動作を制御することができます。 プラン ガイドの詳細については、「 [Plan Guides](../performance/plan-guides.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)   
 [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [フィルター選択されたインデックスの作成](../indexes/create-filtered-indexes.md)  
