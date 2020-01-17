---
title: カスタム レポートを使用したスクリプトの監視
description: SQL Server Management Studio (SSMS) のカスタム レポートを使用して、外部スクリプト (Python と R) の実行、使用されたリソース、問題の診断、SQL Server Machine Learning Services のパフォーマンスの調整を監視します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: afc90985fc7c0c6d7a04cb575ee9e93a4b7b4c51
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727748"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>SQL Server Management Studio のカスタムレポートを使用して Python および R のスクリプトの実行を監視する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Management Studio (SSMS) のカスタム レポートを使用して、外部スクリプト (Python と R) の実行、使用されたリソース、問題の診断、SQL Server Machine Learning Services のパフォーマンスの調整を監視します。

これらのレポートでは、次のような詳細情報を表示できます。

- アクティブな Python または R のセッション
- インスタンスの構成設定
- 機械学習ジョブの実行統計
- R Services の拡張イベント
- 現在のインスタンスにインストールされている Python または R のパッケージ

この記事では、SQL Server Machine Learning Services 用のカスタム レポートをインストールして使用する方法について説明します。

SQL Server Management Studio のレポートの詳細については、「[Management Studio におけるカスタム レポート](../../ssms/object/custom-reports-in-management-studio.md)」を参照してください。

## <a name="how-to-install-the-reports"></a>レポートのインストール方法

レポートは SQL Server Reporting Services を使用するように設計されていますが、SQL Server Management Studio から直接使用することができます。 Reporting Services を SQL Server インスタンスにインストールする必要はありません。

これらのレポートを使用するには、次の手順を実行します。

1. GitHub から SQL Server Machine Learning Services の [SSMS カスタム レポート](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)をダウンロードします。

2. Management Studio へのレポートのコピー

    1. SQL Server Management Studio で使用されるカスタム レポート フォルダーを見つけます。 既定では、カスタム レポートはこのフォルダーに格納されます (**user_name** は Windows ユーザー名)。

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       別のフォルダーを指定したり、サブフォルダーを作成したりすることもできます。

    2. ダウンロードした *.RDL ファイルをカスタム レポート フォルダーにコピーします。

3. Management Studio でレポートを実行する

    1. Management Studio で、レポートを実行するインスタンスの **[データベース]** ノードを右クリックします。

    2. **[レポート]** 、 **[カスタム レポート]** の順にクリックします。

    3. **[ファイルを開く]** ダイアログ ボックスで、カスタム レポート フォルダーを見つけます。

    4. ダウンロードした RDL ファイルを選択し、 **[開く]** をクリックします。

## <a name="reports"></a>[レポート]

[GitHub の SSMS カスタム レポート リポジトリ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)には次のレポートが含まれています。

| レポート | [説明] |
|-|-|
| Active sessions | 現在、SQL Server インスタンスに接続し、Python または R のスクリプトを実行しているユーザー。 |
| 構成 | Machine Learning Services のインストール設定および Python または R のランタイムのプロパティ。 |
| インスタンスを構成する | Machine Learning Services を構成します。 |
| 実行の統計 | Machine Learning Services の実行統計 たとえば、外部スクリプト実行の合計数と並列実行数を取得できます。 |
| 拡張イベント | 外部スクリプトの実行に関する追加の洞察を得るために使用できる拡張イベント。 |
| パッケージ | SQL Server インスタンスにインストールされている R または Python のパッケージと、バージョンや名前などのプロパティを一覧表示します。 |
| Resource Usage | SQL Server の CPU、メモリ、IO 消費量、および外部スクリプトの実行を表示します。 外部のリソース プールのメモリ設定を表示することもできます。 |

## <a name="next-steps"></a>次の手順

- [動的管理ビュー (DMV) を使用して SQL Server Machine Learning Services を監視する](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [R Services の拡張イベント](../r/extended-events-for-sql-server-r-services.md)
