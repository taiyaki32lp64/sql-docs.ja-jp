---
title: R のチュートリアル
description: SQL Server のデータベース内分析に関する R 言語のチュートリアルについて。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c71ebfbda37e66050f868fa7676d0247e84840e
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119230"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server の R 言語のチュートリアル
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) または [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) のデータベース内分析に関する R 言語のチュートリアルについて説明します。

+ ストアド プロシージャで R コードをラップして実行する方法について説明します。
+ R ベースのモデルをシリアル化し、SQL Server データベースに保存します。
+ リモートおよびローカルの計算コンテキストについて、およびそれらを使用するタイミングについて説明します。
+ データ サイエンスと機械学習のための Microsoft R ライブラリについて検討します。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R のクイックスタートとチュートリアル

| リンク | [説明] |
|------|-------------|
| [クイックスタート: R スクリプトを作成して実行する](quickstart-r-create-script.md) | いくつかのクイックスタートの始めに、これを使用して、SQL Server Management Studio などの T-SQL クエリ エディターを使用して R 関数を呼び出すための基本的な構文を示します。 |
| [チュートリアル: データ サイエンティスト向けのデータベース内分析に関する説明](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | SQL Server を初めて使用する R 開発者向けに、このチュートリアルでは SQL Server で一般的なデータ サイエンス タスクを実行する方法について説明します。 データを読み込んで視覚化し、モデルをトレーニングして SQL Server に保存し、予測分析にモデルを使用します。 |
| [チュートリアル: SQL 開発者向けのデータベース内分析に関する説明](../tutorials/sqldev-in-database-r-for-sql-developers.md) | [!INCLUDE[tsql](../../includes/tsql-md.md)] ツールのみを使用して、完全な R ソリューションを構築し、展開します。 ソリューションを運用環境に移行することに重点を置いています。 ストアド プロシージャに R コードをラップし、R モデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに保存し、パラメーター化された呼び出しを R モデルに行い、予測を実行する方法について学習します。 |
| [チュートリアル: RevoScaleR の詳細情報](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | RevoScaleR パッケージでこの関数を使用する方法について説明します。 R と SQL Server 間でデータを移動し、特定のタスクに合わせて計算コンテキストを切り替えます。 モデルとプロットを作成し、それらを開発環境とデータベース サーバーの間で移行します。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>コード サンプル

| リンク | [説明] |
|------|-------------|
| [R と SQL Server を使用して予測モデルを作成する](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | スキー レンタル ビジネスで機械学習を使用して、今後のレンタルを予測する方法を学習します。これは、今後の需要に合わせた事業計画と人員配置に役立ちます。 |
| [R と SQL Server を使用して顧客のクラスタリングを実行する](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 教師なし学習を使用して、売上データに基づいて顧客をセグメント化します。 |

## <a name="see-also"></a>参照

+ [SQL Server の R 拡張機能](../concepts/extension-r.md)
+ [SQL Server Machine Learning Services チュートリアル](machine-learning-services-tutorials.md)

