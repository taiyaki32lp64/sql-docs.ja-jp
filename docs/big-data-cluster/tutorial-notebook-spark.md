---
title: サンプルのノートブックを実行する | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] でサンプルの Spark ノートブックを読み込んで実行する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4acb5c2306064da29d3537fc881dbfc3d312ad2f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844242"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-big-data-cluster"></a>チュートリアル:SQL Server ビッグ データ クラスターでサンプルのノートブックを実行する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] で Azure Data Studio にノートブックを読み込んで実行する方法について説明します。 これにより、データ サイエンティストやデータ エンジニアは、クラスターに対して Python、R、または Scala コードを実行することができます。

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の [Spark サンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)を参照してください。

## <a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターへのサンプル データの読み込み](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>サンプルのノートブック ファイルをダウンロードする

次の手順を使用して、サンプルのノートブック ファイル **spark-sql.ipynb** を Azure Data Studio に読み込みます。

1. bash コマンド プロンプト (Linux) または Windows PowerShell を開きます。

1. サンプルのノートブック ファイルをダウンロードするディレクトリに移動します。

1. 次の **curl** コマンドを実行し、GitHub からノートブック ファイルをダウンロードします。

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>ノートブックを開く

次の手順では、Azure Data Studio でノートブック ファイルを開く方法を示しています。

1. Azure Data Studio で、ビッグ データ クラスターのマスター インスタンスに接続します。 詳細については、[ビッグ データ クラスターへの接続](connect-to-big-data-cluster.md)に関するページを参照してください。

1. **[サーバー]** ウィンドウで、HDFS/Spark ゲートウェイ接続をダブルクリックします。 その後、 **[ノートブックを開く]** を選択します。

   ![ノートブックを開く](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. **[カーネル]** とターゲット コンテキスト ( **[アタッチ先]** ) が設定されるまで待ちます。 **[カーネル]** を **PySpark3** に設定し、 **[アタッチ先]** をビッグ データ クラスター エンドポイントの IP アドレスに設定します。

   ![[カーネル] と [アタッチ先] を設定する](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>ノートブック セルを実行する

セルの左側にある [再生] ボタンを押して、各ノートブック セルを実行することができます。 セルの実行が完了した後、結果がノートブックに表示されます。

![ノートブック セルを実行する](media/tutorial-notebook-spark/run-notebook-cell.png)

サンプル ノートブック内の各セルを続けて実行します。 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] でノートブックを使用する方法の詳細については、次のリソースを参照してください。

- [SQL Server でノートブックを使用する方法](notebooks-guidance.md)
- [Azure Data Studio でノートブックを管理する方法](notebooks-how-to-manage.md)

## <a name="next-steps"></a>次の手順

ノートブックについてさらに学習します:
> [!div class="nextstepaction"]
> [ノートブックの詳細](notebooks-guidance.md)
