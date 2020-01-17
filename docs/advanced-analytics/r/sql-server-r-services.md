---
title: SQL Server 2016 R Services とは
titleSuffix: ''
description: R Services は、リレーショナル データを使用して R スクリプトを実行することができる SQL Server 2016 の機能です。 オープンソースのパッケージとフレームワーク、および予測分析と機械学習用の Microsoft R パッケージを使用できます。 スクリプトは、SQL Server の外部またはネットワーク経由でデータを移動することなく、データベース内で実行されます。 この記事では、SQL Server R Services の基本について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 99aba9748e7ee6d53aabb18919324243740d996a
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149926"
---
# <a name="what-is-sql-server-2016-r-services"></a>SQL Server 2016 R Services とは
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services は、リレーショナル データを使用して R スクリプトを実行することができる SQL Server 2016 の機能です。 オープンソースのパッケージとフレームワーク、および予測分析と機械学習用の [Microsoft R パッケージ](#packages)を使用できます。 スクリプトは、SQL Server の外部またはネットワーク経由でデータを移動することなく、データベース内で実行されます。 この記事では、SQL Server R Services の基本について説明します。

> [!Note]
> R Services は SQL Server 2017 以降から [Machine Learning Services](../what-is-sql-server-machine-learning.md) に名前が変更されました。また、Python と R の両方をサポートしています。

## <a name="what-is-r-services"></a>R Services とは?

SQL Server R Services を使用すると、データベース内で R スクリプトを実行できます。 この機能を使用して、データの準備とクリーンアップ、特徴エンジニアリング、およびデータベース内での機械学習モデルのトレーニング、評価、およびデプロイを行うことができます。 この機能により、データが存在する場所でスクリプトが実行され、ネットワークを介して別のサーバーにデータが転送されなくなります。

R の基本ディストリビューションは R Services に含まれています。 Microsoft パッケージ [RevoScaleR](../r/ref-r-revoscaler.md)、[MicrosoftML](../r/ref-r-microsoftml.md)、[olapR]../r/ref-r-olapr.md)、および [sqlrutils](../r/ref-r-sqlrutils.md) for R に加え、オープンソースのパッケージとフレームワークを使用できます。

R Services では、SQL Server での R スクリプトの実行に機能拡張フレームワークを使用します。 このしくみについては以下を参照してください。

+ [機能拡張フレームワーク](../concepts/extensibility-framework.md)
+ [R の拡張機能](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>R Services でできること

R Services を使用して、SQL Server 内で機械学習モデルとディープ ラーニング モデルを構築およびトレーニングできます。 また、既存のモデルを R Services にデプロイし、予測にリレーショナル データを使用することもできます。

SQL Server R Services を使用できる予測の種類の例には、次のものがあります。

|||
|-|-|
|分類/カテゴリ|顧客からのフィードバックを肯定的なカテゴリと否定的なカテゴリに自動的に分割します|
|回帰/予測の連続値|サイズと場所に基づいて家の価格を予測します|
|異常検出|不正な銀行取引を検出します |
|推奨事項|以前の購入に基づいて、オンラインの顧客が購入する商品を提案します|

### <a name="how-to-execute-r-scripts"></a>R スクリプトを実行する方法

R Services で R スクリプトを実行するには、次の 2 つの方法があります。

+ 最も一般的な方法は、T-SQL ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用することです。

+ また、任意の R クライアントを使用して、実行をリモートの SQL Server にプッシュするスクリプト (*リモート計算コンテキスト*と呼ばれます) を書くこともできます。 詳細については、[データ サイエンス クライアントの R 開発を設定する](../r/set-up-a-data-science-client.md)方法に関する記事を参照してください。

<a name="packages"></a>

## <a name="r-packages"></a>R パッケージ

Microsoft のエンタープライズ パッケージに加えて、オープンソース パッケージとフレームワークを使用できます。 最も一般的なオープンソースの R パッケージは、R Services にプレインストールされています。 Microsoft の次の R パッケージも含まれています。

| [パッケージ] | [説明] |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | スケーラブルな R の主要パッケージ。データの変換と操作、統計の概要、視覚化、多くの形式のモデリング。 さらに、このパッケージの関数により、並列処理に使用できるコア全体にワークロードが自動的に分散されます。 |
| [MicrosoftML (R)](../r/ref-r-microsoftml.md) | テキスト分析、画像分析、感情分析のカスタム モデルを作成する機械学習アルゴリズムを追加します。 |
| [olapR](../r/ref-r-olapr.md) | SQL Server Analysis Services OLAP キューブに対する MDX クエリに使用される R 関数。 |
| [sqlrutils](../r/ref-r-sqlrutils.md) | T-SQL ストアド プロシージャで R スクリプトを使用し、そのストアド プロシージャをデータベースに登録し、[R 開発環境](../r/set-up-a-data-science-client.md)からストアド プロシージャを実行するメカニズム。 |
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) は、Microsoft の R の拡張ディストリビューションです。 これは、統計分析とデータ サイエンスの機能が一式そろったオープンソース プラットフォームです。 R に基づき、100% の互換性があり、パフォーマンスと再現性を向上させる追加機能が含まれています。 |

## <a name="how-do-i-get-started-with-rservices"></a>RServices の基本的な使用方法

1. [SQL Server 2016 R Services をインストールします](../install/sql-r-services-windows-install.md)

1. 開発ツールを構成します。 使用できるもの:

    + T-SQL およびストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して R スクリプトを実行する [Azure Data Studio](../../azure-data-studio/what-is.md) または [SQL Server Management Studio (SSMS)](../../ssms/sql-server-management-studio-ssms.md)。
    + スクリプトを実行する開発用のノート PC またはワークステーション上の R。 [RevoScaleR](../r/ref-r-revoscaler.md) を使用してデータをローカルにプルすることや、リモートから SQL Server に実行をプッシュすることができます。 詳細については、[データ サイエンス クライアントの R 開発を設定する](../r/set-up-a-data-science-client.md)方法に関する記事を参照してください。

1. 最初の R スクリプトを作成します

    + クイック スタート: [SQL Server でシンプルな R スクリプトを作成して実行する](../tutorials/quickstart-r-create-script.md)
    + クイック スタート: [R で予測モデルを作成してトレーニングする](../tutorials/quickstart-r-train-score-model.md)
    + チュートリアル:[T-SQL で R を使用する](../tutorials/sqldev-in-database-r-for-sql-developers.md):データの探索、特徴エンジニアリングの実行、モデルのトレーニングとデプロイ、予測の作成 (5 部構成シリーズ)
    + チュートリアル:[R ツールで R Services を使用する](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md):データの探索、グラフとプロットの作成、特徴エンジニアリングの実行、モデルのトレーニングとデプロイ、予測の作成 (6 部構成シリーズ)

## <a name="next-steps"></a>次の手順

+ [SQL Server 2016 R Services をインストールする](../install/sql-r-services-windows-install.md)
+ [R 開発用にデータ サイエンス クライアントを設定する](../r/set-up-a-data-science-client.md)