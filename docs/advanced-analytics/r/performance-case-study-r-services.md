---
title: 結果のパフォーマンス チューニング
description: この記事では、さまざまな最適化方法をテストした 2 つのケース スタディの方法、結果、および結論をまとめています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 068b7aa3c068b10b787b99bba26c12a2b680bcd3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727410"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services のパフォーマンス: 結果とリソース
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

これは、R Services のパフォーマンスの最適化について説明する、シリーズの最後となる 4 番目の記事です。 この記事では、さまざまな最適化方法をテストした 2 つのケース スタディの方法、結果、および結論をまとめています。

2 つのケース スタディには異なる目標がありました。

+ R Services 開発チームによる最初のケース スタディでは、特定の最適化手法の影響の測定を試みました。
+ データ サイエンティスト チームによる 2 番目のケース スタディでは、特定の大規模なスコアリング シナリオに最も適した最適化手法を決定するために、複数の方法が実験されました。

このトピックでは、最初のケース スタディの結果の詳細を示します。 2 番目のケース スタディでは、全体の結果について概要を説明します。 このトピックの最後には、すべてのスクリプトとサンプル データ、および元の作成者が使用したリソースへのリンクがあります。

## <a name="performance-case-study-airline-dataset"></a>パフォーマンス ケース スタディ:Airline データセット

SQL Server R Services 開発チームによるこのケース スタディでは、さまざまな最適化の効果をテストしました。 Airline データセットに対して 1 つの rxLogit モデルが作成され、スコアリングが実行されました。 個々の影響を評価するために、トレーニングおよびスコアリング プロセス中に最適化が適用されました。

- GitHub:SQL Server 最適化スタディの[サンプル データとスクリプト](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>テスト メソッド

1. Airline データセットは、10 万行からなる 1 つのテーブルで構成されます。 ダウンロードされ、SQL Server に一括で読み込まれました。
2. テーブルのコピーが 6 つ作成されました。
3. ページ圧縮、行圧縮、インデックス作成、列形式のデータストアなどの SQL Server 機能をテストするために、テーブルのコピーにさまざまな変更を適用しました。
4. 各最適化が適用される前後で、パフォーマンスを測定しました。

| テーブル名| [説明]|
|------|------|
| *airline* | `rxDataStep` を使用して元の xdf ファイルから変換されたデータ。|                          |
| *airlineWithIntCol*   | *DayOfWeek* が文字列ではなく整数に変換されています。 また、*rowNum* 列が追加されています。|
| *airlineWithIndex*    | *airlineWithIntCol* テーブルと同じデータですが、*rowNum* 列を使用する 1 つのクラスター化インデックスが含まれます。|
| *airlineWithPageComp* | *airlineWithIndex* テーブルと同じデータですが、ページ圧縮が有効になっています。 また、*CRSDepTime* と *ArrDelay* から計算された、*CRSDepHour* と *Late* の 2 つの列が追加されています。 |
| *airlineWithRowComp*  | *airlineWithIndex* テーブルと同じデータですが、行圧縮が有効になっています。 また、*CRSDepTime* と *ArrDelay* から計算された、*CRSDepHour* と *Late* の 2 つの列が追加されています。 |
| *airlineColumnar*     | 1 つのクラスター化インデックスを含む単票形式ストア。 このテーブルには、クリーンアップされた csv ファイルのデータが含まれます。|

各テストは、次の手順で行いました。

1. R ガベージ コレクションは各テストの前に発生します。
2. ロジスティック回帰モデルは、テーブル データに基づいて作成されました。 各テストの *rowsPerRead* の値は 500000 に設定されます。
3. トレーニング済みのモデルを使用して、スコアが生成されました
4. 各テストは 6 回実行されました。 最初の実行 ("コールド ラン") の時間は破棄されました。 不定期な外れ値を考慮するために、残りの 5 回の実行の中で**最長**の時間も破棄されました。 それ以外の 4 回の実行の平均値から、各テストの平均実行時間を計算します。
5. テストは、*reportProgress* パラメーターの値が 3 (= 時間と進行状況をレポートする) の状態で実行されました。 各出力ファイルには、IO にかかった時間、遷移時間、および計算時間に関する情報が含まれます。 これらの時間はトラブルシューティングと診断に役立ちます。
6. コンソールの出力も、出力ディレクトリ内のファイルに送られました。
7. テスト スクリプトは、これらのファイル内の時間を処理し、平均実行時間を計算します。

たとえば、1 回のテストでの時間の結果を次に示します。 関心がある主な時間は、**合計読み取り時間** (IO 時間) と **遷移時間** (計算のプロセスを設定するオーバーヘッド) です。

**サンプルのタイミング**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

R Services または RevoScaleR の関数についての問題のトラブルシューティングに役立つように、テスト スクリプトをダウンロードして変更することをお勧めします。

### <a name="test-results-all"></a>テスト結果 (すべて)

このセクションでは、各テストの前後の結果を比較します。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>圧縮と列テーブル ストアでのデータ サイズ

最初のテストでは、データのサイズを小さくするための、圧縮および列形式のテーブルの使用を比較します。

| テーブル名            | [行]     | 予約済み。   | data       | index_size | 未使用  | 節約率 (予約済み) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/a        | 368 KB  | 93%                 |

**結論**

列ストア インデックスを適用したものが最も大きなデータ サイズの削減を達成でき、ページ圧縮がそれに続きました。

#### <a name="effects-of-compression"></a>圧縮の効果

このテストでは、行圧縮、ページ圧縮、および圧縮なしの利点を比較しました。 3 つの異なるデータ テーブルのデータに対して、`rxLinMod` を使用してモデルをトレーニングしました。 すべてのテーブルで同じ式とクエリが使用されました。

| テーブル名            | テスト名       | numTasks | 平均時間 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - 並列| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - 並列 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - 並列  | 4        | 5.2375       |

**結論**

圧縮単体では役に立たないようです。 この例では、圧縮を処理する CPU の増加が、IO 時間の短縮を相殺しています。

ただし、*numTasks* を 4 に設定してテストを並列実行すると、平均時間が短縮されます。

データ セットの量が増えると、圧縮の効果はさらに顕著になる可能性があります。 圧縮はデータ セットと値によって変わるため、自らのデータ セットに圧縮が与える効果を判別するには実験することをお勧めします。

### <a name="effect-of-windows-power-plan-options"></a>Windows の電源プラン オプションの効果

この実験では、`rxLinMod` が *airlineWithIntCol* テーブルで使用されました。 Windows の電源プランは、 **[バランス]** または **[高パフォーマンス]** に設定されていました。 すべてのテストで *numTasks* は 1 に設定されました。 テストは 6 回を 1 セットとして、両方の電源オプションで 2 セット実施し、結果の変動を調査しました。

**[ハイ パフォーマンス]** 電源オプション:

| テスト名 | \# を実行します。 | 経過時間 | 平均時間 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.57 秒 |              |
|           | 2      | 3.45 秒 |              |
|           | 3      | 3.45 秒 |              |
|           | 4      | 3.55 秒 |              |
|           | 5      | 3.55 秒 |              |
|           | 6      | 3.45 秒 |              |
|           |        |              | 3.475        |
|           | 1      | 3.45 秒 |              |
|           | 2      | 3.53 秒 |              |
|           | 3      | 3.63 秒 |              |
|           | 4      | 3.49 秒 |              |
|           | 5      | 3.54 秒 |              |
|           | 6      | 3.47 秒 |              |
|           |        |              | 3.5075       |

**[バランス]** 電源オプション:

| テスト名 | \# を実行します。 | 経過時間 | 平均時間 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.89 秒 |              |
|           | 2      | 4.15 秒 |              |
|           | 3      | 3.77 秒 |              |
|           | 4      | 5 秒    |              |
|           | 5      | 3.92 秒 |              |
|           | 6      | 3.8 秒  |              |
|           |        |              | 3.91         |
|           | 1      | 3.82 秒 |              |
|           | 2      | 3.84 秒 |              |
|           | 3      | 3.86 秒 |              |
|           | 4      | 4.07 秒 |              |
|           | 5      | 4.86 秒 |              |
|           | 6      | 3.75 秒 |              |
|           |        |              | 3.88         |

**結論**

Windows **[ハイ パフォーマンス]** 電源プランを使用すると、実行時間がより安定し、かつ高速になります。

#### <a name="using-integer-vs-strings-in-formulas"></a>数式での整数の使用と、文字列の使用の比較

このテストでは、文字列要素による一般的な問題を回避するために、R コードを変更した場合の影響を評価しました。 具体的には、2 つのテーブルを使用して、`rxLinMod` を使用してモデルをトレーニングしました。1 番目のテーブルでは、要素は文字列として格納されています。2 番目のテーブルでは、要素は整数として格納されています。

+ *airline* テーブルでは、[DayOfWeek] 列には文字列が含まれています。 _colInfo_ パラメーターを使用して、要素のレベル (月曜日、火曜日、…) を指定しました。

+  *airlineWithIndex* テーブルの場合、[DayOfWeek] は整数です。 _colInfo_ パラメーターは指定されませんでした。

+ どちらの場合も、同じ式 `ArrDelay ~ CRSDepTime + DayOfWeek` が使用されました。

| テーブル名          | テスト名   | 平均時間 |
|---------------------|-------------|--------------|
| *airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**結論**

要素に文字列ではなく整数を使用すると、明確な利点があります。

### <a name="avoiding-transformation-functions"></a>変換関数の回避

このテストでは、`rxLinMod` を使用してモデルをトレーニングしましたが、次の 2 回の実行の間でコードが変更されました。

+ 最初の実行では、モデルのビルドの一部として変換関数が適用されました。 
+ 2 番目の実行では、特徴の値が事前計算済みで使用可能であったため、変換関数は必要ありませんでした。

| テスト名             | 平均時間 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**結論**

変換関数を使用**しない**場合、トレーニング時間が短縮されました。 言い換えると、事前に計算され、テーブルに保存されている列を使用すると、モデルのトレーニングが高速になりました。

変換が多く、データセットのサイズが大きい (1 億行以上) 場合は、さらに節約率が高くなることが予想されます。

### <a name="using-columnar-store"></a>列ストアの使用

このテストでは、列データ ストアとインデックスを使用した場合のパフォーマンス上の利点を評価しました。 同じモデルが `rxLinMod` を使用してトレーニングされ、データ変換は行われませんでした。

+ 最初の実行では、データ テーブルでは標準の行ストアが使用されました。
+ 2 番目の実行では、列ストアが使用されました。

| テーブル名         | テスト名 | 平均時間 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**結論**

標準の行ストアよりも、列ストアのほうがパフォーマンスが向上しています。 大きなデータセット (1 億行以上) では、パフォーマンスの大きな違いが期待できます。

### <a name="effect-of-using-the-cube-parameter"></a>Cube パラメーターを使用した場合の効果

このテストの目的は、事前計算済みの **cube** パラメーターを使用する RevoScaleR のオプションにより、パフォーマンスを向上できるかどうかを判断することでした。 次の式を使用して、`rxLinMod` を使用してモデルをトレーニングしました。

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

テーブルでは、*DayOfWeek* 要素が文字列として格納されています。

| テスト名     | Cube パラメーター | numTasks | 平均時間 | 単一行予測 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**結論**

Cube パラメーター引数を使用すると、パフォーマンスが明らかに向上します。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>rxDTree モデルの maxDepth を変更した場合の効果

この実験では、`rxDTree` アルゴリズムを使用して *airlineColumnar* テーブルにモデルを作成しました。 このテストでは *numTasks* は 4 に設定されました。 ツリーの深さの変更が実行時間に与える影響を実証するために、*maxDepth* にはいくつかの異なる値が使用されました。

| テスト名       | maxDepth | 平均時間 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**結論**

ツリーの深さが増えると、ノードの総数は指数関数的に増加します。 また、モデル作成時の経過時間も大幅に増加しています。

### <a name="prediction-on-a-stored-model"></a>格納済みモデルでの予測

このテストの目的は、トレーニング済みのモデルが現在実行中のコードの一部として生成されるのではなく、SQL Server テーブルに保存される場合の、スコアリングのパフォーマンスへの影響を判断することでした。 スコアリングのために、格納されているモデルはデータベースから読み込まれ、メモリ内の 1 行のデータ フレーム (ローカルのコンピューティング コンテキスト) を使用して予測が作成されます。

テスト結果から、モデルを保存する時間と、モデルの読み込みと予測にかかる時間がわかります。

| テーブル名 | テスト名 | 平均時間 (モデルのトレーニング) | モデルの保存/読み込みの時間|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09 (予測する時間を含む) |

**結論**

トレーニング済みのモデルをテーブルから読み込むことで、より迅速に予測を行うことができます。 モデルの作成とスコアリングの実行のすべてを、同じスクリプト内で実行しないことをお勧めします。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>ケース スタディ:履歴書照合タスクの最適化

履歴書照合モデルは、Microsoft のデータ サイエンティストの Ke Huang によって、SQL Server での R コードのパフォーマンスをテストするために開発されました。そうすることにより、データ サイエンティストがスケーラブルなエンタープライズ レベルのソリューションを作成する助けとなりました。

### <a name="methods"></a>メソッド

大規模なデータセットを含む複雑な R ソリューションで予測モデルをトレーニングするために、RevoScaleR パッケージと MicrosoftML パッケージの両方が使用されました。 SQL クエリと R コードは、すべてのテストで同一でした。 テストは、SQL Server がインストールされた単一の Azure VM で実施されました。 そして作成者は、SQL Server によって提供される次の最適化を使用する場合としない場合とで、スコアリング時間を比較しました。

- イン メモリ テーブル
- ssNoVersion
- [リソース ガバナー]

R スクリプトの実行時にソフト NUMA の効果を評価するために、データ サイエンス チームは 20 個の物理コアを持つ Azure 仮想マシンでソリューションをテストしました。 これらの物理コアでは、各ノードに 5 個のコアが含まれるように、自動的に 4 個のソフト NUMA ノードが作成されました。

R ジョブへの影響を評価するために、履歴書照合シナリオでは CPU アフィニティ化が適用されました。 4 個の **SQL リソース プール**と 4 個の**外部リソース プール**が作成されました。そして CPU アフィニティが指定され、各ノードで同じ CPU セットが使用されるようになりました。

ハードウェアの使用率を最適化するために、各リソース プールは別のワークロード グループに割り当てられました。 これは、ソフト NUMA と CPU アフィニティが物理 NUMA ノードの物理メモリを分割できないためです。したがって、定義上、同じ物理 NUMA ノードに基づくすべてのソフト NUMA ノードは、同じ OS メモリ ブロック内のメモリを使用する必要があります。 つまり、メモリとプロセッサ間のアフィニティはありません。

この構成を作成するために、次のプロセスを使用しました。

1. SQL Server に既定で割り当てられるメモリの量を減らします。

2. R ジョブを並行して実行するために、4 個の新しい共有元を作成します。

3. 各ワークロード グループがリソース プールに関連付けられるように、4 個のワークロード グループを作成します。

4. 新しいワークロード グループおよび割り当てを使用して、Resource Governor を再起動します。

5. ユーザー定義の分類子関数 (UDF) を作成し、異なるワークロード グループに異なるタスクを割り当てます。

6. 適切なワークロード グループに関数を使用するように、Resource Governor 構成を更新します。

### <a name="results"></a>[結果]

履歴書照合の検討で、最高のパフォーマンスが得られた構成は次のとおりです。

-   4 つの内部リソース プール (SQL Server 用)

-   4 つの外部リソース プール (外部スクリプト ジョブ用)

-   各リソース プールが、特定のワークロード グループに関連付けられている

-   各リソース プールが、異なる CPU に割り当てられている

-   内部メモリの最大使用量 (SQL Server 用) = 30%

-   R セッションで使用する最大メモリ = 70%

履歴書照合モデルの場合、外部スクリプトの使用が非常に多く、他のデータベース エンジン サービスは実行されていませんでした。 そのため、外部スクリプトに割り当てられたリソースを 70% に増加しました。その結果、スクリプトのパフォーマンスに関して最適な構成となりました。

この構成には、異なる値を使用して実験することによってたどり着きました。 もし、異なるハードウェアや別のソリューションを使用している場合は、最適な構成が異なる場合があります。 ケースに最適な構成を見つけるには、常に実験することです。

最適化されたソリューションでは、20 コアのコンピューター上で 110 万行のデータ (100 個の特徴を含む) が、8.5 秒未満でスコアリングされました。 最適化により、スコアリング時間に関するパフォーマンスが大幅に向上しました。

またこの結果は、**特徴の数**がスコアリング時間に大きな影響を与えたことを示唆しています。 予測モデルで多くの特徴が使用された場合、改善はさらに顕著になりました。

詳細については、このブログ記事と付随するチュートリアルをお読みになることをお勧めします。

-   [SQL Server での機械学習の最適化に関するヒントとコツ](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

多くのユーザーは、R (または Python) ランタイムが初めて読み込まれたときに、短い一時停止が発生することに気付いています。 このため、これらのテストで説明したように、最初の実行時間は通常測定されますが、後に破棄されます。 後続のキャッシュにより、最初の実行と 2 回目の実行の間で、パフォーマンスが顕著に異なる場合があります。 また、SQL Server と外部ランタイム間でデータが移動される場合、特にデータが SQL Server から直接読み込まれるのではなくネットワーク経由で渡される場合にも、オーバーヘッドが発生します。

パフォーマンスへの影響はタスクによって大きく異なるため、これらすべての理由に対して、この最初の読み込む時間を軽減する唯一のソリューションはありません。 たとえば、バッチでの単一行のスコアリングではキャッシュが行われます。そのため、連続したスコアリング操作がはるかに高速になり、モデルも R ランタイムも再読み込みされません。 [ネイティブ スコアリング](../sql-native-scoring.md)を使用して、R ランタイム全体が読み込まれないようにすることもできます。

大規模なモデルをトレーニングしたり、大きなバッチでスコアリングしたりする場合、データの移動を回避したり、ストリーミングや並列処理を行ったりすることによる利益と比較して、オーバーヘッドはごくわずかであるかもしれません。 その他のパフォーマンス ガイダンスについては、こちらのブログ記事を参照してください。

+ [1 秒あたり 100 万トランザクションで、R を使用して不正行為を検出する](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>リソース

これらのテストの開発で使用された情報、ツール、およびスクリプトへのリンクを次に示します。

+ パフォーマンス テスト スクリプトとデータへのリンク:[SQL Server 最適化スタディのサンプル データとスクリプト](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 履歴書照合ソリューションについての説明記事:[SQL Server R Services の最適化に関するヒントとコツ](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 履歴書照合ソリューションのための SQL 最適化で使用されるスクリプト:[GitHub リポジトリ](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Windows サーバーの管理について学習する

+ [64 ビット版 Windows 用の適切なページ ファイルのサイズを確認する方法](https://support.microsoft.com/kb/2860880)

+ [NUMA について](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server で NUMA をサポートする方法](https://technet.microsoft.com/library/ms180954.aspx)

+ [ソフト NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>SQL Server の最適化について学習する

+ [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [メモリ最適化テーブルの概要](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ 「[実証: イン メモリ OLTP のパフォーマンスの向上](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [データの圧縮](../../relational-databases/data-compression/data-compression.md)

+ [テーブルまたはインデックスの圧縮の有効化](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [テーブルまたはインデックスの圧縮の無効化](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>SQL Server の管理について学習する

+ [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor の概要](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services のリソース管理](resource-governance-for-r-services.md)

+ [R 用のリソース プールを作成する方法](how-to-create-a-resource-pool-for-r.md)

+ [Resource Governor を構成する例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>ツール

+ [DISKSPD ストレージ ロード ジェネレーター/パフォーマンス テスト ツール](https://github.com/microsoft/diskspd)

+ [FSUtil ユーティリティ リファレンス](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>このシリーズの他の記事

[R のパフォーマンス チューニング - 概要](sql-server-r-services-performance-tuning.md)

[R のパフォーマンス チューニング - SQL Server の構成](sql-server-configuration-r-services.md)

[R のパフォーマンス チューニング - R コードとデータの最適化](r-and-data-optimization-r-services.md)

[パフォーマンス チューニング - ケース スタディの結果](performance-case-study-r-services.md)
