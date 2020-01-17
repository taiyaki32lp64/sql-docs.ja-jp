---
title: 移行後の検証および最適化ガイド | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: pelopes
ms.author: harinid
ms.openlocfilehash: 915dde0b6b2083c45b5bfe4196e7578537a91379
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909155"
---
# <a name="post-migration-validation-and-optimization-guide"></a>移行後の検証および最適化ガイド

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の移行後手順は、データの精度と完全性の調整、およびワークロードのパフォーマンスの問題の発見に、非常に重要です。

## <a name="common-performance-scenarios"></a>パフォーマンスの一般的なシナリオ

次に示すのは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プラットフォームへの移行後に発生する一般的なパフォーマンスのシナリオと、その解決方法です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行 (古いバージョンから新しいバージョン) に固有のシナリオや、外部のプラットフォーム (Oracle、DB2、MySQL、Sybase など) から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行に固有のシナリオが含まれています。

## <a name="CEUpgrade"></a> CE バージョンでの変更によるクエリ パフォーマンス低下

**適用対象:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行。

古いバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 以降に移行する場合、および[データベース互換性レベル](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)を最新のレベルにアップグレードする場合、ワークロードのパフォーマンスが低下するリスクにさらされる可能性があります。

これは、[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 以降、すべてのクエリ オプティマイザーの変更が最新の[データベース互換性レベル](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)と連携しているため、プランの変更は、アップグレードの時点ではなく、ユーザーが `COMPATIBILITY_LEVEL` のデータベース オプションを最新のものに変更した時点で発生するためです。 この機能とクエリ ストアの組み合わせによって、アップグレード プロセス中のクエリのパフォーマンスを高いレベルで制御できます。 

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] で導入されたクエリ オプティマイザーの変更の詳細については、「[Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx)」(SQL Server 2014 のカーディナリティ推定を使用したクエリ プランの最適化) を参照してください。

### <a name="steps-to-resolve"></a>解決手順

[データベース互換性レベル](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)をソース バージョンに変更して、次の図に示すように推奨されるアップグレードのワークフローに従います。

![query-store-usage-5](../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  

このトピックの詳細については、「[SQL Server 2016 へのアップグレード中にパフォーマンスの安定性を維持する](../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)」を参照してください。

## <a name="ParameterSniffing"></a> パラメーター スニッフィングに対する感度

**適用対象:** 外部プラットフォーム (Oracle、DB2、MySQL、Sybase など) から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行で、移行元の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にこの問題が存在していた場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の新しいバージョンにそのまま移行したのでは、このシナリオには対処できません。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、最初のコンパイルで入力パラメーターのスニッフィングを使って、その入力データの分布に最適化された、パラメーター化された再利用可能なプランを生成することで、ストアド プロシージャのクエリ プランをコンパイルします。 ストアド プロシージャではない場合でも、単純なプランを生成するほとんどのステートメントがパラメーター化されます。 プランが最初にキャッシュされた後、それ以降の実行は前にキャッシュされたプランにマップします。
その最初のコンパイルで通常のワークロードに対する最も一般的なパラメーターのセットが使われないことがある場合、問題が発生する可能性があります。 異なるパラメーターに対して実行プランが同じでは非効率的になります。 このトピックの詳細については、「[パラメーター スニッフィング](../relational-databases/query-processing-architecture-guide.md#ParamSniffing)」を参照してください。

### <a name="steps-to-resolve"></a>解決手順

1.  `RECOMPILE` ヒントを使います。 プランは、各パラメーター値に適応されるたびに計算されます。
2.  `(OPTIMIZE FOR(<input parameter> = <value>))` オプションを使うように、ストアド プロシージャを書き直します。 関連するワークロードのほとんどに適した値を決定し、パラメーター化された値に対して効率的になる 1 つのプランを作成して保守します。
3.  プロシージャ内でローカル変数を使うように、ストアド プロシージャを書き直します。 これで、オプティマイザーは予測に密度ベクトルを使うようになり、パラメーター値に関係なく同じプランになります。
4.  `(OPTIMIZE FOR UNKNOWN)` オプションを使うように、ストアド プロシージャを書き直します。 ローカル変数の手法を使う場合と同じ効果があります。
5.  `DISABLE_PARAMETER_SNIFFING` ヒントを使うようにクエリを書き直します。 `OPTION(RECOMPILE)`、`WITH RECOMPILE`、または `OPTIMIZE FOR <value>` が使われていない場合はパラメーター スニッフィングを完全に無効にすることで、ローカル変数の手法を使う場合と同じ効果があります。

> [!TIP] 
> これが問題かどうかをすばやく識別するには、[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] のプラン分析機能を利用します。 詳細については、[こちら](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/)をご覧ください。

## <a name="MissingIndexes"></a> 欠落したインデックス

**適用対象:** 外部プラットフォーム (Oracle、DB2、MySQL、Sybase など) および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行。

正しくないインデックスまたは不足しているインデックスにより、余分な I/O が発生し、結果としてメモリや CPU が浪費されます。 原因は、ワークロード プロファイルが変更されて、異なる述語が使われるようになり、既存のインデックス設計が無効になったためである可能性があります。 不適切なインデックス戦略またはワークロード プロファイルの変更の証拠としては、次のようなものがあります。
-   重複したインデックス、冗長なインデックス、ほとんど使われていないインデックス、およびまったく使われていないインデックスを探します。
-   更新では使われていないインデックスに特に注意します。

### <a name="steps-to-resolve"></a>解決手順

1.  存在しないインデックス参照にはグラフィカル実行プランを利用します。
2.  [データベース エンジン チューニング アドバイザー](../tools/dta/tutorial-database-engine-tuning-advisor.md)によって生成されたインデックスの提案。
3.  [不足インデックス DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) または [SQL Server パフォーマンス ダッシュ ボード](https://www.microsoft.com/download/details.aspx?id=29063)を利用します。
4.  欠落、重複、冗長、低使用頻度、完全不使用のインデックスに関するインサイト、およびインデックス参照がデータベースの既存のプロシージャにヒント/ハードコーディングされているかどうかに関するインサイトを提供する既存の DMV を使用できる既存のスクリプトを活用します。 

> [!TIP] 
> 既存のスクリプトの例としては、[Index Creation](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) や [Index Information](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information) などがあります。 

## <a name="InabilityPredicates"></a> 述語を使ってデータをフィルターできない

**適用対象:** 外部プラットフォーム (Oracle、DB2、MySQL、Sybase など) および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行で、移行元の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にこの問題が存在していた場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の新しいバージョンにそのまま移行したのでは、このシナリオには対処できません。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、コンパイル時に認識されている情報のみを考慮することができます。 ワークロードが実行時にのみ認識できる述語に依存する場合は、不適切なプランの選択が増える可能性があります。 高品質のプランでは、述語は **SARGable** (**S**earch **Arg**ument**able**: 検索引数化可能 ) である必要があります。

SARGable ではない述語の例を次に示します。
-   VARCHAR から NVARCHAR、INT から VARCHAR のような暗黙的なデータ変換。 実際の実行プランで実行時の CONVERT_IMPLICIT 警告を探します。 型を変換すると、精度が失われるをこともあります。
-   `WHERE UnitPrice + 1 < 3.975` などの複雑な不定式。`WHERE UnitPrice < 320 * 200 * 32` は違います。
-   `WHERE ABS(ProductID) = 771` や `WHERE UPPER(LastName) = 'Smith'` などの関数を使う式
-   `WHERE LastName LIKE '%Smith'` のような先頭にワイルドカード文字がある文字列。`WHERE LastName LIKE 'Smith%'` は違います。

### <a name="steps-to-resolve"></a>解決手順

1. 常に目的のターゲット[データ型](../t-sql/data-types/data-types-transact-sql.md)として変数/パラメーターを宣言します。 
  -   これには、データベースに格納されるユーザー定義のコード構造 (ストアド プロシージャ、ユーザー定義関数、ビューなど) と、基になるテーブルで使われるデータ型についての情報を保持するシステム テーブル ([sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md) など) の比較が含まれる場合があります。
2. 前のポイントまですべてのコードをスキャンできない場合は、同じ目的で、変数/パラメーターの宣言と一致するように、テーブルのデータ型を変更します。
3. 次の構造の有用性を熟考します。

  -   述語として使われている関数
  -   ワイルドカード検索
  -   列データに基づく複雑な式 – インデックスを作成できる永続計算列を代わりに作成する必要性を評価します。

> [!NOTE] 
> 上記のすべてをプログラムで実行することができます。

## <a name="TableValuedFunctions"></a> テーブル値関数の使用 (複数ステートメントとインライン)

**適用対象:** 外部プラットフォーム (Oracle、DB2、MySQL、Sybase など) および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への移行で、移行元の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にこの問題が存在していた場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の新しいバージョンにそのまま移行したのでは、このシナリオには対処できません。

テーブル値関数は、ビューの代わりになるテーブル データ型を返します。 ビューは 1 つの `SELECT` ステートメントに制限されますが、ユーザー定義関数はビューより多くのロジックを許される追加ステートメントを含むことができます。

> [!IMPORTANT] 
> MSTVF (複数ステートメントのテーブル値関数) の出力テーブルはコンパイル時に作成されないので、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは実際の統計ではなくヒューリスティックに依存して、行の推定を決定します。 基底テーブルにインデックスを追加しても、役には立ちません。 MSTVF の場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、MSTVF によって返されるものと予想される行数に固定値 1 を使います ([!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 以降、固定の推定値は 100 行です)。

### <a name="steps-to-resolve"></a>解決手順

1.  複数ステートメントの TVF が 1 ステートメントのみである場合は、インライン TVF に変換します。

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```

    インライン形式の例を次に示します。

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.  さらに複雑な場合は、メモリ最適化テーブルまたは一時テーブルに格納される中間結果を使うことを検討します。

##  <a name="Additional_Reading"></a> その他の情報

 [クエリ ストアを使用する際の推奨事項](../relational-databases/performance/best-practice-with-the-query-store.md)  
[メモリ最適化テーブル](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[ユーザー定義関数](../relational-databases/user-defined-functions/user-defined-functions.md)  
[テーブル変数と行の推定 - パート 1](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[テーブル変数と行の推定 - パート 2](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[実行プランのキャッシュと再利用](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)
