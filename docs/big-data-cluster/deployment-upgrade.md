---
title: 新しいリリースにアップグレードする
titleSuffix: SQL Server Big Data Clusters
description: SQL Server ビッグ データ クラスターを新しいリリースにアップグレードする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f44ef17a712d0d5a19707cf94e7d3e4196a2aba3
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706307"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]をアップグレードする方法

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、SQL Server ビッグ データ クラスターを新しいリリースにアップグレードする方法に関するガイダンスを提供します。 この記事の手順は、プレビュー リリースから SQL Server 2019 サービス アップデート リリースにアップグレードする方法に特に当てはまります。

## <a name="backup-and-delete-the-old-cluster"></a>以前のクラスターをバックアップして削除する

現時点では、ビッグ データ クラスターにはインプレース アップグレードはなく、新しいリリースにアップグレードする唯一の方法は、クラスターを手動で削除して再作成することです。 各リリースには、以前のバージョンと互換性のない固有のバージョンの `azdata` があります。 また、古いクラスターで新しいノードにコンテナー イメージをダウンロードする必要があった場合は、最新のイメージがクラスター上の古いイメージと互換性がない可能性があります。 コンテナー設定の展開構成ファイルで `latest` イメージ タグを使用した場合にのみ、新しいイメージがプルされることに注意してください。 既定では、各リリースには、SQl Server のリリース バージョンに対応する固有のイメージ タグがあります。 最新のリリースにアップグレードするには、次の手順に従います。

1. 以前のクラスターを削除する前に、SQL Server マスター インスタンス上と HDFS 上のデータをバックアップします。 SQL Server マスター インスタンスの場合は、[SQL Server のバックアップと復元](data-ingestion-restore-database.md)を使用できます。 HDFS の場合は、[`curl` を使用してデータをコピーできます](data-ingestion-curl.md)。

1. `azdata delete cluster` コマンドを使用して、古いクラスターを削除します。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > クラスターと一致するバージョンの `azdata` を使用します。 新しいバージョンの `azdata` で古いクラスターを削除しないでください。

   > [!Note]
   > `azdata bdc delete` コマンドを発行すると、そのビッグ データ クラスター名で示される名前空間内で作成されたすべてのオブジェクトは削除されますが、名前空間自体は削除されません。 名前空間は、空で、他のアプリケーションが中に作成されていない限り、後の展開に再利用できます。

1. 古いバージョンの `azdata` をアンインストールします。

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 最新バージョンの `azdata` をインストールします。 次のコマンドでは、最新のリリースから `azdata` がインストールされます。

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 各リリースで、`azdata` の `n-1` バージョンへのパスが変更されます。 以前に `azdata` をインストールしている場合でも、新しいクラスターを作成する前に、最新のパスから再インストールする必要があります。

## <a id="azdataversion"></a> azdata のバージョンを確認する

新しいビッグ データ クラスターを展開する前に、`--version` パラメーターを指定して、最新バージョンの `azdata` を使用していることを確認します。

```bash
azdata --version
```

## <a name="install-the-new-release"></a>新しいリリースをインストールする

以前のビッグ データ クラスターを削除し、最新の `azdata` をインストールしたら、現在の展開手順に従って、新しいビッグ データ クラスターを展開します。 詳細については、「[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する方法](deployment-guidance.md)」を参照してください。 次に、必要なデータベースまたはファイルを復元します。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] とは](big-data-cluster-overview.md)の概要に関するページを参照してください。
