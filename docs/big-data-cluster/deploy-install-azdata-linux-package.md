---
title: インストーラーを使用して azdata を Linux にインストールする
titleSuffix: SQL Server big data clusters
description: SQL Server ビッグ データ クラスターをインストールおよび管理するためにインストーラー (Linux) を使用して azdata ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532070"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Linux 上で [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を管理するために `azdata` をインストールする

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、Linux に SQL Server 2019 ビッグ データ クラスター用の `azdata` をインストールする方法について説明します。 これらのパッケージ マネージャーが使用可能になる前は、`azdata` をインストールするために `pip` が必要でした。

パッケージ マネージャーは、さまざまなオペレーティング システムおよびディストリビューション向けに設計されています。

- Windows および Linux (Ubuntu ディストリビューション) の場合は、[パッケージ マネージャー](./deploy-install-azdata-installer.md)を使用してインストールすると、操作が簡単になります。
- Linux (Ubuntu) の場合は、[`apt` を使用して `azdata` をインストール](#azdata-apt)します

現時点では、他のオペレーティング システムまたはディストリビューションに `azdata` をインストールするためのパッケージ マネージャーはありません。 これらのプラットフォームについては、[パッケージ マネージャーを使用せずに `azdata` をインストールする方法](./deploy-install-azdata.md)に関する記事を参照してください。

## <a id="linux"></a>Linux 用の `azdata` をインストールする

Ubuntu で使用可能な `azdata` インストール パッケージは `apt` を使用して入手できます。

### <a id="azdata-apt"></a>apt (Ubuntu) を使用して `azdata` をインストールする

>[!NOTE]
>`azdata` パッケージでは、システム Python は使用されず、独自の Python インタープリターがインストールされます。

1. インストール プロセスに必要なパッケージを取得します。

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 署名キーをダウンロードし、インストールします。

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. `azdata` リポジトリ情報を追加します。

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

4. リポジトリ情報を更新し、`azdata` をインストールします。

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. インストールを確認します。

    ```bash
    azdata --version
    ```

### <a name="update"></a>更新

`azdata` のみをアップグレードします。

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>アンインストール

1. apt-get remove を使用してアンインストールします。

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. `azdata` リポジトリ情報を削除します。

    >[!NOTE]
    >今後 `azdata` をインストールする予定がある場合、この手順は必要ありません

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 署名キーを削除します。

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Azdata CLI を使用してインストールされた、不要な依存関係を削除します。

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
