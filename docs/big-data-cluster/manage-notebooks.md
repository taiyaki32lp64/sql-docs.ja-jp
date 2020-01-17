---
title: Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを管理する
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Azure Data Studio のノートブックを使用して、ビッグ データ クラスターの管理とトラブルシューティングを行います。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 860524daa5e6ab2db17fdf95cf5aa785aeb4fdf7
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844287"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを管理する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、ノートブックを含む Azure Data Studio の拡張機能を提供します。 ノートブックには、SQL Server 2019 ビッグ データ クラスターを管理するために Azure Data Studio で使用できるドキュメントとコードが用意されています。

もともとは、オープン ソース プロジェクトとして実装され、[ノートブック](notebooks-guidance.md)は [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download) 内に組み込まれていました。 テキスト セル内のテキストに対してはマークダウンを、また、コード セル内にコードを記述するには利用可能なカーネルの 1 つを使用できます。

ノートブックを使用して、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] に対してビッグ データ クラスターを展開できます。

ノートブックに加え、ユーザーは Jupyter Book と呼ばれるノートブックのコレクションを表示できます。 Jupyter Book には、ノートブックのコレクション内を移動できる目次が用意されています。これにより、必要なノートブックを見つけたり、SQL Server のトラブルシューティングを行ったり、クラスターの状態を表示したりすることができます。

## <a name="prerequisites"></a>Prerequisites

ノートブックを開くには、次のコンポーネントが必要です。

* [Azure Data Studio Insiders ビルド](https://aka.ms/azuredatastudio-rc)の最新バージョン
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 拡張機能が Azure Data Studio にインストールされている

これらのコンポーネントに加えて、SQL Server 2019 ビッグ データ クラスターを展開するには、次のコンポーネントも必要です。

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>ノートブックのトラブルシューティングへのアクセス
ノートブックのトラブルシューティングにアクセスするには、次の 3 つの方法があります。

### <a name="command-palette"></a>コマンド パレット
1. **[ビュー]**  >  **[コマンド パレット]** を選択します。
2. 「**Jupyter Books:SQL Server 2019 Guide**」と入力します。

SQL Server ビッグ データ クラスターに関連するトラブルシューティング ノートブックを含む Jupyter Book が含まれている Jupyter Books Viewlet が開きます。

### <a name="sql-master-dashboard"></a>SQL マスター ダッシュボード
1. Azure Data Studio Insider をインストールした後、SQL Server ビッグ データ クラスター インスタンスに接続します。
2. インスタンスに接続した後、 **[接続]** の下のサーバー名を右クリックし、 **[管理]** を選択します。
3. ダッシュボードで、 **[SQL Server ビッグ データ クラスター]** をクリックします。 **[SQL Server 2019 ガイド]** を選択して、必要なノートブックを含む Jupyter Book を開きます。
    ![ダッシュボードの Jupyter ノートブック](media/manage-notebooks/jupyter-book-button.png)

1. 完了する必要があるタスクのノートブックを選択します。

### <a name="controller-dashboard"></a>コントローラー ダッシュボード
1. **[接続]** ビューで、 **[SQL Server ビッグ データ クラスター]** を展開します。
2. コントローラーのエンドポイントの詳細を追加します。
3. コントローラーに接続した後、エンドポイントを右クリックし、 **[管理]** を選択します。
4. ダッシュボードが読み込まれたら、 **[トラブルシューティング]** を選択して Jupyter Book トラブルシューティング ガイドを開きます。

## <a name="use-troubleshooting-notebooks"></a>ノートブックのトラブルシューティングの使用
1. Jupyter Book の目次で必要なトラブルシューティング ガイドを見つけます。
1. ノートブックは最適化されているので、 **[セルの実行]** を選択する必要があるだけです。 この操作により、ノートブックが完了するまで、ノートブック内の各セルが個別に実行されます。
1. エラーが検出された場合、Jupyter Book は、エラーを修正するために実行できるノートブックを提案します。 推奨される手順に従って、もう一度ノートブックを実行します。

## <a name="next-steps"></a>次の手順
Azure Data Studio のノードブックの詳細については、「[SQL Server でノートブックを使用する方法](notebooks-guidance.md)」を参照してください。
