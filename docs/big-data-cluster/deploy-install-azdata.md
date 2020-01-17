---
title: pip を使用して azdata をインストールする
titleSuffix: SQL Server big data clusters
description: pip を使用して、ビッグ データ クラスターをインストールおよび管理するための azdata ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aaccbae2b4acb745e2cb9ea531f382e0903b528f
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532060"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>`pip` を使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]用に `azdata` をインストールする

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、`pip` を使用して Windows または Linux 用の `azdata` ツールをインストールする方法について説明します。

Windows および Linux (Ubuntu ディストリビューション) の場合は、[パッケージ マネージャー](./deploy-install-azdata-installer.md)を使用してインストールすると、操作が簡単になります。

## <a id="prerequisites"></a> 前提条件

`azdata` は Python で記述されたコマンドライン ユーティリティです。クラスター管理者はこれを使用すると、REST API 経由でビッグ データ クラスターをブートストラップし、管理できるようになります。 最低限必要な Python バージョンは v3.5 です。 `pip` は、`azdata` ツールをダウンロードしてインストールするために必要です。 以下の手順は、Windows と Ubuntu の例です。 他のプラットフォームに Python をインストールする方法については、[Python のドキュメント](https://wiki.python.org/moin/BeginnersGuide/Download)を参照してください。
さらに、最新バージョンの `requests` Python パッケージをインストールして更新します。

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 新しいバージョンのビッグ データ クラスターをインストールする場合は、データをバックアップして以前のクラスターを削除し、`azdata` をアップグレードして新しいリリースをインストールします。 詳細については、[新しいリリースへのアップグレード](deployment-upgrade.md)に関するページを参照してください。

## <a id="windows"></a> Windows `azdata` のインストール

1. Windows クライアントで、[https://www.python.org/downloads/](https://www.python.org/downloads/) から必要な Python パッケージをダウンロードします。 Python 3.5.3 以降では、Python をインストールするときに pip3 もインストールされます。 

   > [!TIP] 
   > Python3 をインストールするときに、`PATH` に Python を追加することを選択します。 そうしない場合は、後で pip3 が配置されている場所を見つけて、`PATH` に手動で追加することができます。

1. 新しい Windows PowerShell セッションを開き、Python で最新のパスを取得します。

1. 以前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。

   CTP 3.2 または RC1 の場合は、次のコマンドを実行します。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   内の複数の
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 次のコマンドを使用して `azdata` をインストールします。

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a> Linux `azdata` のインストール

Linux では、Python 3.5 をインストールしてから、pip をアップグレードする必要があります。 次の例は、Ubuntu で動作するコマンドを示しています。 その他の Linux プラットフォームについては、[Python のドキュメント](https://wiki.python.org/moin/BeginnersGuide/Download)を参照してください。

1. 必要な Python パッケージをインストールします。

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. pip3 をアップグレードする:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 以前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。

   CTP 3.2 または RC1 の場合は、次のコマンドを実行します。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   内の複数の
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 次のコマンドを使用して `azdata` をインストールします。

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` スイッチを指定すると、`azdata` が Python ユーザー インストール ディレクトリにインストールされます。 通常、Linux 上ではこれは `~/.local/bin` です。 このディレクトリをパスに追加するか、ユーザー インストール ディレクトリに移動して、そこから `./azdata` を実行します。

## <a id="macOSX"></a> macOS または OS X に `azdata` をインストールする

macOS または OS X に `azdata` をインストールするには、次の手順を実行します。 各ステップでは、ターミナルで例を実行します。

1. macOS クライアント上で、[Homebrew](https://brew.sh) をインストールします (まだインストールしていない場合)。

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Python と pip、最小バージョン 3.0 をインストールします。

   ```
   brew install python3
   ```

1. 依存関係をインストールします。

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. 以前のリリースのツールがインストールされている場合は、まずそれをアンインストールしてから最新バージョンの `azdata` をインストールすることが重要です。 `azdata` のバージョンを削除するコマンドを次に示します。

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 次のコマンドを使用して `azdata` をインストールします。

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
