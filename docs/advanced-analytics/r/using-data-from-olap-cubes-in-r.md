---
title: R での OLAP キューブからのデータの使用
description: この記事では、olapR API について説明します。また、多次元キューブ データベースを初めて使用する R ユーザーのために、OLAP と MDX の概要についても説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2da5cbf0fd3fbc5b8fe1105261fff98625d590e5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727316"
---
# <a name="using-data-from-olap-cubes-in-r"></a>R での OLAP キューブからのデータの使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** パッケージは、Microsoft により、Machine Learning Server および SQL Server で使用するために提供される R パッケージです。これにより、MDX クエリを実行して、OLAP キューブからデータを取得できます。 このパッケージでは、リンク サーバーの作成や、フラット化した行セットのクリーンアップは必要ありません。OLAP データを R から直接使用できます。

この記事では API について説明します。また、多次元キューブ データベースを初めて使用する R ユーザーのために、OLAP と MDX の概要についても説明します。

> [!IMPORTANT]
> Analysis Services のインスタンスは、従来の多次元キューブまたは表形式モデルのいずれかをサポートできますが、両方をサポートすることはできません。 したがって、キューブに MDX クエリを作成する前に、Analysis Services インスタンスに多次元モデルが含まれていることを確認してください。

## <a name="what-is-an-olap-cube"></a>OLAP キューブとは

OLAP は、オンライン分析処理 (Online Analytical Processing) の略です。 OLAP ソリューションは、長期間にわたり重要なビジネス データをキャプチャし格納するために、幅広く使用されています。 OLAP データは、多様なツール、ダッシュボード、視覚エフェクトでビジネス分析に使用されます。 詳細については、「[Online analytical processing](https://en.wikipedia.org/wiki/Online_analytical_processing)」(オンライン分析処理) を参照してください。

Microsoft には [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services) が用意されています。この機能を使用すると、_キューブ_または_表形式モデル_の形式で、OLAP データを設計、配置、クエリできます。 キューブとは多次元データベースのことです。 _ディメンション_は、データのファセットまたは R の要因に似ています。ディメンションを使用して、集計や分析をするデータのサブセットを特定します。 たとえば、時間は重要なディメンションですので、多くの OLAP ソリューションでは、データをスライスして集計する際に使用する複数のカレンダーが、既定で定義されています。 

パフォーマンス上の理由から、OLAP データベースは、しばしばサマリー (または_集計_) を事前に計算し、高速に取得できるよう格納します。 サマリーは、数値データに適用できる数式を表す*メジャー*に基づいています。 ディメンションを使用してデータのサブセットを定義し、それからそのデータに対しメジャーを計算します。 たとえば、メジャーを使用して、複数の四半期にわたる特定の製品ラインの合計売上から税金を差し引いて計算し、特定の供給者への平均輸送費や、支払済年度累計賃金などを報告することができます。

多次元式 (MDX) は、キューブのクエリに使用される言語です。 通常、MDX クエリには、1 つ以上のディメンションを含むデータ定義と、少なくとも 1 つのメジャーが含まれますが、MDX クエリはかなり複雑になり、ローリングウィンドウ、累積平均、合計、順位、またはパーセンタイルが含まれます。 

MDX クエリの作成を開始する際に役立つ用語を以下に示します。

+ *スライス*は、1 つのディメンションの値を使用して、キューブのサブセットを取得することです。

+ *ダイス* は、複数のディメンションに対して値の範囲を指定してサブキューブを作成することです。

+ *ドリルダウン* は、概要から詳細情報に移動することです。

+ *ドリルアップ* は、集計の詳細情報から概要に移動することです。

+ *ロールアップ* は、ディメンションに関するデータを要約することです。

+ *ピボット* は、キューブまたはデータの選択を回転させることです。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>olapR を使って MDX クエリを作成する方法

以下の記事では、キューブに対してクエリを作成または実行するための構文の例を、詳しく説明します。

+ [R を使って MDX クエリを作成する方法](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** パッケージでは、MDX クエリを作成する方法が 2 つサポートされています。

- **MDX ビルダーを使用します。** パッケージ内の R 関数を使用し、キューブを選択して、軸とスライサーを設定することにより、単純な MDX クエリを生成します。 こうすれば、従来の OLAP ツールにアクセスできなかったり、MDX 言語を深く理解していなくても、有効な MDX クエリを簡単に構築できます。

    MDX は複雑になる可能性があるため、この方法を使用してあらゆる MDX クエリを作成することはできません。 ただし、この API は、N ディメンションのスライス、ダイス、ドリルダウン、ロールアップ、ピボットなど、最も一般的で便利な操作をほぼすべてサポートしています。

+ **整形式の MDX をコピーして貼り付けます。** 手動で作成し、任意の MDX クエリに貼り付けることができます。 このオプションは、再利用する既存の MDX クエリがある場合、または構築するクエリが複雑すぎて **olapR** で処理できない場合に最適です。

    SSMS や Excel など、任意のクライアント ユーティリティを使用して MDX を構築した後、クエリ文字列を保存します。 この MDX 文字列を、**olapR** パッケージにおいて、*SSAS クエリハンドラー*の引数として指定します。 プロバイダーは、指定された Analysis Services サーバーに対してクエリを送信し、結果を R に戻します。 

MDX クエリを構築する方法や、既存の MDX クエリを実行する方法例については、「[How to Create MDX Queries using R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)」(R を使用して MDX クエリを作成する方法) を参照してください。

## <a name="known-issues"></a>既知の問題

このセクションでは、**olapR** パッケージに関する既知の問題と一般的な質問を紹介していきます。

### <a name="tabular-model-support"></a>表形式モデル サポート

表形式モデルを含む Analysis Services のインスタンスに接続すると、`explore` 関数は戻り値 TRUE の成功を報告します。 ただし、表形式モデル オブジェクトは多次元オブジェクトとは異なり、多次元データベースの構造は、表形式モデルのそれとは異なります。

データ分析式 (DAX) は通常表形式モデルで使用される言語ですが、MDX を既によく理解している場合は、表形式モデルに有効な MDX クエリをデザインできます。 olapR コンストラクターを使用して、表形式モデルに有効な MDX クエリを作成することはできません。

ただし、MDX クエリは、表形式モデルからデータを取得するには、効率がよくありません。 R で使用するために表形式モデルからデータを取得する必要がある場合には、代わりに以下の方法を検討してください。

+ モデルで DirectQuery を有効にし、SQL Server のリンク サーバーとしてサーバーを追加します。 
+ 表形式モデルがリレーショナル データ マート上に構築されている場合には、ソースから直接データを取得します。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>インスタンスに表形式モデルと多次元モデルのどちらかが含まれているかを確認するには

単独の Analysis Services インスタンスに含めるモデルの種類は 1 つだけですが、複数のモデルを含めることができます。 理由としては、表形式モデルと多次元モデルには、データの格納や処理を行う方法を制御する基本的な違いがあるためです。 たとえば、表形式モデルはメモリに格納され、列ストア インデックスを利用して、非常に高速な計算を実行します。 多次元モデルでは、データはディスクに格納され、集計は事前に定義され、MDX クエリを使用して取得されます。

SQL Server Management Studio などのクライアントを使って Analysis Services に接続する場合には、データベースのアイコンを見れば、サポートされているモデルの種類を一目で確認できます。

また、サーバーのプロパティを表示・照会して、インスタンスからサポートされているモデルの種類を確認することもできます。 **サーバー モード** プロパティでは、_多次元_、_表形式_の 2 つの値がサポートされています。

この 2 種類のモデルに関する一般情報については、次の記事を参照してください。

+ [多次元モデルと表形式モデルの比較](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

サーバー プロパティのクエリの詳細については、次の記事を参照してください。

+ [OLE DB for OLAP Schema 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>書き戻しはサポートされていません

カスタム R 計算の結果をキューブに書き戻すことはできません。

一般に、キューブで書き戻しが有効になっている場合でも、限られた操作のみがサポートされ、追加の構成が必要になることがあります。 このような操作には、MDX の使用をお勧めします。

+ [書き込み許可ディメンション](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [書き込み許可パーティション](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [セルデータへのカスタム アクセス権の設定](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>実行時間の長い MDX クエリは、キューブの処理を妨げます

**olapR** パッケージは読み取り操作のみを実行しますが、実行時間の長い MDX クエリでは、キューブの処理を妨げるロックが作成されることがあります。 返されるデータの量を把握できるよう、常に MDX クエリを事前にテストしてください。

ロックされているキューブに接続しようとすると、SQL Server データ ウェアハウスに到達できないというエラーが表示されることがあります。 推奨される解決策としては、リモート接続の有効化、サーバーまたはインスタンス名の確認などがありますが、事前に接続が開いていた可能性を考慮してください。

SSAS 管理者は、開いているセッションを識別し終了することによって、ロックの問題を回避できます。 タイムアウト プロパティをサーバー レベルで MDX クエリに適用し、実行時間の長いクエリをすべて強制終了することもできます。

## <a name="resources"></a>リソース

OLAP や MDX クエリの初心者であれば、以下の Wikipedia 記事を参照してください。 

+ 「[OLAP Cubes](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX queries](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)」(OLAP キューブ MDX クエリ)
