---
title: 事前トレーニング済みモデルのインストール
description: 感情分析およびイメージの特性付けのための事前トレーニング済みのモデルを SQL Server Machine Learning Services (R または Python) または SQL Server R Services に追加します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97da2ed795d002fa47900eb21ead90b48b525387
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727560"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>事前トレーニング済みの機械学習モデルを SQL Server にインストールする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では Powershell を使用して、"*感情分析*" および "*イメージの特性付け*" のための事前トレーニング済みの機械学習モデルを、R または Python が統合されている SQL Server インスタンスに追加する方法について説明します。 事前トレーニング済みのモデルは Microsoft によって構築され、すぐに使用できる状態で、インストール後のタスクとしてインスタンスに追加されます。 これらのモデルの詳細については、この記事の「[リソース](#bkmk_resources)」セクションを参照してください。

インストールが完了すると、事前トレーニング済みのモデルは、MicrosoftML (R) ライブラリと microsoftml (Python) ライブラリの特定の機能を強化する実装の詳細と見なされます。 モデルを表示、カスタマイズ、または再トレーニングしないでください (そうすることもできません)。また、これらをカスタム コードの独立したリソースとして扱うことや、他の関数と組み合わせて使用することもできません。 

事前トレーニング済みのモデルを使用するには、次の表に示す関数を呼び出します。

| R 関数 (MicrosoftML) | Python 関数 (microsoftml) | 使用方法 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | テキスト入力に対して正/負のセンチメント スコアを生成します。 |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 画像ファイル入力からテキスト情報を抽出します。 |

## <a name="prerequisites"></a>Prerequisites

機械学習アルゴリズムは、計算を集中的に行います。 すべてのサンプル データを使用したチュートリアルの完了など、低から中レベルのワークロードには 16 GB の RAM を使用することをお勧めします。

事前トレーニング済みのモデルを追加するには、コンピューターおよび SQL Server に対する管理者権限が必要です。

外部スクリプトを有効にし、SQL Server LaunchPad サービスが実行されている必要があります。 インストール手順では、これらの機能を有効にして確認する手順について説明します。 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[MicrosoftML R パッケージ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)または [microsoftml Python パッケージ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)には、事前トレーニング済みモデルが含まれています。

[SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) には、機械学習ライブラリの両方の言語バージョンが含まれているため、ユーザー側でこれ以上の操作をしなくてもこの前提条件は満たされます。 ライブラリが存在するため、この記事で説明されている PowerShell スクリプトを使用して、事前トレーニング済みのモデルをこれらのライブラリに追加できます。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[MicrosoftML R package](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) には、事前トレーニング済みモデルが含まれています。

[SQL Server R Services](sql-r-services-windows-install.md) は、R 専用であり、すぐに使用可能な [MicrosoftML パッケージ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)が含まれていません。 MicrosoftML を追加するには、[コンポーネントのアップグレード](../install/upgrade-r-and-python.md)を行う必要があります。 コンポーネントのアップグレードの利点の 1 つは、事前トレーニング済みのモデルを同時に複数追加できるため、PowerShell スクリプトを実行する必要がないことです。 ただし、既にアップグレードしたが、事前トレーニング済みのモデルを最初に追加しなかった場合は、この記事の説明に従って PowerShell スクリプトを実行できます。 これは両方のバージョンの SQL Server で機能します。 その前に、`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library` に MicrosoftML ライブラリが存在することを確認してください。
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>事前トレーニング済みのモデルがインストールされているかどうかを確認する

R モデルと Python モデルのインストール パスは次のとおりです。

+ R の場合: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Python の場合: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

モデル ファイル名を次に示します。

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

モデルが既にインストールされている場合は、[検証手順](#verify)に進んで利用可能かどうかを確認します。

## <a name="download-the-installation-script"></a>インストール スクリプトをダウンロードする

[https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) をクリックして、ファイル **Install-MLModels.ps1** をダウンロードします。

## <a name="execute-with-elevated-privileges"></a>昇格された特権で実行する

1. PowerShell を開始します。 タスクバーで、PowerShell プログラム アイコンを右クリックし、 **[管理者として実行]** を選択します。
2. インストール スクリプト ファイルへの完全修飾パスを入力し、インスタンス名を含めます。 Downloads フォルダーおよび既定のインスタンスがある場合、コマンドは次のようになります。

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**出力**

インターネットに接続された SQL Server Machine Learning Services の既定のインスタンスで、R と Python を使用している場合、次のようなメッセージが表示されます。

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>インストールの確認

まず、[mxlibs フォルダー](#file-location)に新しいファイルがあるかどうかを確認します。 次に、デモ コードを実行して、モデルがインストールされて機能していることを確認します。 

### <a name="r-verification-steps"></a>R の検証手順

1. C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64 にある **RGUI.EXE** を開始します。

2. コマンド プロンプトに次の R スクリプトを貼り付けます。

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. Enter キーを押して、センチメント スコアを表示します。 出力は次のようになります。

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Python の検証手順

1. C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES にある **Python.exe** を開始します。

2. コマンド プロンプトに次の Python スクリプトを貼り付けます

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. Enter キーを押してスコアを出力します。 出力は次のようになります。

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> デモ スクリプトが失敗した場合は、最初にファイルの場所を確認してください。 SQL Server の複数のインスタンスがあるシステム、またはスタンドアロン バージョンと並行して実行されているインスタンスの場合、インストール スクリプトによって環境が誤って読み取られ、ファイルが間違った場所に配置される可能性があります。 通常は、ファイルを正しい mxlib フォルダーに手動でコピーすることで問題が解決されます。

## <a name="examples-using-pre-trained-models"></a>事前トレーニング済みのモデルを使用した例

次のリンクには、事前トレーニング済みのモデルを呼び出すコード例が含まれています。

+ [コード サンプル:テキスト フィーチャライザーを使用した感情分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>調査とリソース

現在使用できるモデルは、感情分析とイメージ分類のためのディープ ニューラル ネットワーク (DNN) モデルです。 事前トレーニング済みのモデルはすべて、Microsoft の [Computation Network Toolkit](https://cntk.ai/Features/Index.html) (**CNTK**) を使用してトレーニングされています。

各ネットワークの構成は、次の参照実装に基づいています。

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

これらのディープ ラーニング モデルで使用されるアルゴリズムの詳細と、CNTK を使用したこれらの実装方法とトレーニング方法については、次の記事を参照してください。

+ [Microsoft の研究者のアルゴリズムが ImageNet の課題のマイルストーンを設定](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft Computational Network Toolkit では、最も効率的な分散型ディープ ラーニングの計算パフォーマンスが提供される](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>参照

+ [SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [SQL Server のインスタンス内の R および Python コンポーネントをアップグレードする](../install/upgrade-r-and-python.md)
+ [R 用の MicrosoftML パッケージ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Python 用の microsoftml パッケージ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
