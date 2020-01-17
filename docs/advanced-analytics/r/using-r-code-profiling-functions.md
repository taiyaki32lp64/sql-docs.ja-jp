---
title: R コード プロファイル関数の使用
description: R プロファイリング関数を使用して内部関数呼び出しに関する情報を返すことによって、SQL Server での R 計算のパフォーマンスを向上させ、結果を高速化します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e03ae1a8c4cdab87f46f63da6271886b4518b5e3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715016"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>R コード プロファイル関数を使用してパフォーマンスを向上させる
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server のリソースとツールを使用して R スクリプトの実行を監視できるほか、他の R パッケージが提供するパフォーマンス ツールを使用して、内部関数の呼び出しに関する情報を取得できます。 

> [!TIP]
> この記事では、作業を開始するための基本的なリソースについて説明します。 専門家によるガイダンスとしては、[Hadley Wickham 著 "Advanced R"](http://adv-r.had.co.nz) の「*Performance*」の章をお勧めします。

## <a name="using-rprof"></a>rprof の使用

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) は、基本パッケージ [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1) に含まれる関数で、既定で読み込まれます。 

一般に *rprof* 関数は、指定した間隔でファイルに呼び出し履歴を記述することで機能します。 その後、[*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 関数を使用して、出力ファイルを処理できます。 *rprof* の利点の 1 つは、サンプリングを実行するため、監視によるパフォーマンスの負荷を軽減することです。

コードで R プロファイルを使用するには、この関数を呼び出してパラメーター (書き込まれるログ ファイルの場所の名前など) を指定します。 コードでプロファイルをオンまたはオフにできます。 基本的な使用法を次の構文に示します。 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> この関数を使用するには、コードを実行するコンピューターに Windows Perl がインストールされている必要があります。 このため、R 環境での開発中にコードをプロファイルし、デバッグ済みのコードを SQL Server に展開することをお勧めします。  


## <a name="r-system-functions"></a>R システム関数

R 言語には、システム変数の内容を返すための多くの基本パッケージ関数が含まれています。 たとえば、R コードの一部として、`Sys.timezone` を使用して現在のタイム ゾーンを取得したり、`Sys.Time` を使用して R からシステム時刻を取得することがあります。 

個別の R システム関数の情報を取得するには、R コマンド プロンプトから、R `help()` 関数の引数として関数名を入力します。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>R のデバッグとプロファイル

既定でインストールされる Microsoft R Open のドキュメントには、R 言語の拡張機能の開発に関するマニュアルが含まれており、[プロファイルとデバッグ](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)の詳細について説明しています。 お使いのコンピューターでこちらから同じドキュメントを取得できます。C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual

## <a name="see-also"></a>参照

+ [utils R パッケージ](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ [Hadley Wickham 著 "Advanced R"](http://adv-r.had.co.nz)
