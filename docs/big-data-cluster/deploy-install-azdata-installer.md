---
title: Windows インストーラーで azdata をインストールする
titleSuffix: SQL Server big data clusters
description: SQL Server ビッグ データ クラスターをインストールおよび管理するための azdata ツールを、インストーラーを使用してインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b2e87cf96d6237521caeaae55802d2d72769603
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594336"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>Windows インストーラーで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を管理するための `azdata` をインストールする

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、Windows に SQL Server 2019 ビッグ データ クラスター用の `azdata` をインストールする方法について説明します。 Windows インストールを利用できるようになる前は、`azdata` をインストールするには `pip` が必要でした。

>Linux (Ubuntu) の場合は、[インストーラーでの `azdata` のインストール](./deploy-install-azdata-linux-package.md)に関する記事を参照してください。

現時点では、他のオペレーティング システムまたはディストリビューションに `azdata` をインストールするためのパッケージ マネージャーはありません。 これらのプラットフォームについては、[パッケージ マネージャーを使用せずに `azdata` をインストールする方法](./deploy-install-azdata.md)に関する記事を参照してください。

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Microsoft Windows インストーラーで `azdata` をインストールする

Microsoft Windows インストーラーで `azdata` をインストールするには、次のようにします。

1. `pip` を使用してインストールされた `azdata` がある場合は削除します。 Windows インストーラーを使用して `azdata` がインストールされている場合は、次のステップに進みます。
1. Windows インストーラーを使用して `azdata` をインストールします。

### <a name="uninstall-if-previous-installation-done-with-pip"></a>以前に `pip` で行われたインストールがある場合はアンインストールする

以前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。

   `azdata` のリリース候補バージョンを削除するには、次のコマンドを実行します。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

削除されたら、[Windows に `azdata` をインストールします](#install-azdata-windows)。

>[!NOTE]
>以前のインストールが MSI を使用して行われた場合、MSI インストーラーを使用する前に、現在のバージョンをアンインストールする必要はありません。

### <a id="install-azdata-windows"></a>Windows インストーラーでインストールする

Windows 上の `azdata` を、Windows インストーラーを使用してインストールまたは更新します。

[`azdata` Windows インストーラーをダウンロードします](https://aka.ms/azdata-msi)。

インストーラーでコンピューターを変更できるかどうか確認するメッセージが表示されたら、[`Yes`] をクリックします。

### <a name="uninstall-azdata-with-windows-installer"></a>Windows インストーラーで `azdata` をアンインストールする

Windows インストーラーで `azdata` をアンインストールするには、該当するオペレーティング システムの指示に従います。

| プラットフォーム      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| [スタート] > [設定] > [アプリ]                                |
| Windows 8     | [スタート] > [コントロール パネル] > [プログラム] > [プログラムのアンインストール] |

アンインストールするプログラムは `Azdata CLI` という名前です。 このアプリケーションを選択し、[`Uninstall`] ボタンをクリックします。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。