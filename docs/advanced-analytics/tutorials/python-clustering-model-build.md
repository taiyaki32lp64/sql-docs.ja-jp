---
title: Python のチュートリアル:クラスター モデルをビルドする
description: この 4 部構成のチュートリアル シリーズのパート 3 では、K-Means モデルをビルドして、SQL Server Machine Learning Services を使用して Python でクラスタリングを実行します。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669686d0163b9ce1c362e7cdf2814c7a95bfaa8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727103"
---
# <a name="tutorial-build-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>チュートリアル:モデルを Python にビルドし、SQL Server Machine Learning Services で顧客を分類する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この 4 部構成のチュートリアル シリーズのパート 3 では、クラスタリングを実行するために、Python で K-Means モデルをビルドします。 このシリーズの次の部では、SQL Server Machine Learning Services を使用して、このモデルを SQL データベースにデプロイします。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * K-Means アルゴリズムのクラスター数を定義する
> * クラスタリングを実行する
> * 結果を分析する

[パート 1 ](python-clustering-model.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[パート 2 ](python-clustering-model-prepare-data.md)では、SQL データベースからデータを準備してクラスタリングを実行する方法を学びました。

[パート 4 ](python-clustering-model-deploy.md)では、新しいデータに基づいて Python でクラスタリングを実行できるストアド プロシージャを SQL データベースに作成する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

* このチュートリアルのパート 3 は、[**パート 1** ](python-clustering-model.md)の前提条件を満たし、[**パート 2** ](python-clustering-model-prepare-data.md)の手順を完了していることを前提としています。

## <a name="define-the-number-of-clusters"></a>クラスターの数を定義する

顧客データのクラスター化には、データをグループ化する最も単純かつ有名な方法の 1 つ、**K-Means** クラスタリング アルゴリズムを使用します。
K-Means の詳細については、[K-means クラスタリング アルゴリズムの詳細ガイド](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)に関するページを参照してください。

このアルゴリズムでは、次の 2 つの入力を受け取ります。データ自体、および定義済みの数値 "*k*" は、生成するクラスターの数を表します。
出力は、クラスター間でパーティション分割された入力データを持つ *k* クラスターとなっています。

K-means が目指すのは、項目を k クラスターにグループ化して、同じクラスター内のすべての項目が互いに類似し、他のクラスター内の項目とは可能な限り異なるようにすることです。

アルゴリズムで使用するクラスターの数を決定するには、抽出されたクラスターの数によって、グループ内の平方和のプロットを使用します。 使用するクラスターの数は、プロットの曲がっている部分または "カギ" の部分になります。

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![カギ線グラフ](./media/python-tutorial-elbow-graph.png)

グラフに基づいて、*k = 4* の値をまず試します。 *k* 値は、顧客を 4 つのクラスターにグループ化します。

## <a name="perform-clustering"></a>クラスタリングを実行する

次の Python スクリプトでは、sklearn パッケージの KMeans 関数を使用します。

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>結果を分析する

K-Means を使用したクラスタリングが完了したため、次の手順では結果を分析して、実行可能な情報を見つけられるかどうかを確認します。

前のスクリプトから出力されたクラスタリングの平均値とクラスター サイズを確認します。

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

4 つのクラスターは、[パート 1 ](python-clustering-model-prepare-data.md#separate-customers)で定義した変数を使用して指定されます。

* *orderRatio* = 注文返品率 (注文の総数に対する部分的または完全に返品された注文の総数)
* *itemsRatio* = アイテム返品率 (購入されたアイテムの総数に対する返品されたアイテムの総数)
* *monetaryRatio* = 返品金額率 (合計購入金額に対する返されたアイテムの合計金額)
* *frequency* = 返品の頻度

多くの場合、K-Means を使用したデータ マイニングでは結果をさらに詳しく分析し、各クラスターについて理解を深めるためにさらに手順を進める必要がありますが、これにより良いスタートを切ることができるようになります。
これらの結果を解釈するいくつかの方法を次に示します。

* クラスター 0 は、アクティブでない (すべての値が 0 である) 顧客のグループである可能性があります。
* クラスター 3 は、戻り値の動作の観点では目立つグループであるように見えます。

クラスター 0 は、アクティブでないことが明らかな顧客のセットです。 場合によっては、このグループをターゲットにしたマーケティング策を講じることで、購買を促すことができるかもしれません。 次の手順では、クラスター 0 の顧客の電子メールアドレスをデータベースに照会して、マーケティング メールを送信できるようにします。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、SQL Server から tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次の手順

このチュートリアル シリーズのパート 3 では、次の手順を完了しました。

* K-Means アルゴリズムのクラスター数を定義する
* クラスタリングを実行する
* 結果を分析する

作成した機械学習モデルをデプロイするには、このチュートリアル シリーズのパート 4 の手順に従います。

> [!div class="nextstepaction"]
> [チュートリアル: SQL Server Machine Learning Services を使用して Python でクラスタリング モデルをデプロイする](python-clustering-model-deploy.md)