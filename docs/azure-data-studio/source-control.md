---
title: ソース管理
titleSuffix: Azure Data Studio
description: Azure Data Studio でソース管理を構成する方法について説明します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c278bcf6cff451396b3d677b203f207b68fd6dc5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959286"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] でのソース管理の使用

[!INCLUDE[name-sos](../includes/name-sos-short.md)] は、バージョン管理/ソース管理用の Git をサポートします。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] での Git のサポート

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、Git ソース管理マネージャー (SCM) が付属していますが、これらの機能を使用できるようにする前に [Git (バージョン 2.0.0 以降) をインストールする](https://git-scm.com/download)必要があります。 



## <a name="open-an-existing-git-repository"></a>既存の Git リポジトリを開く

1. **[ファイル]** メニューで、 **[フォルダーを開く]** を選択します。
2. Git で追跡されるファイルが含まれているフォルダーを参照して、 **[フォルダーの選択]** をクリックします。 ここで、ローカル リポジトリ内のサブフォルダーを選択できます。


## <a name="initialize-a-new-git-repository"></a>新しい Git リポジトリを初期化する

1. **[ソース管理]** を選択して、Git アイコンを選択します。

   ![ソース管理 Git アイコン](media/source-control/source-control.png)

1. Git リポジトリとして初期化するフォルダーへのパスを入力して、**Enter** キーを押します。

   ![Git リポジトリを初期化する](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Git リポジトリの操作

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、Git 実装が VS Code から継承されていますが、追加の SCM プロバイダーは現在サポートされていません。 リポジトリを開くか、初期化した後に Git を操作する方法の詳細については、[VS コードでの Git のサポート](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)に関する記事を参照してください。


## <a name="additional-resources"></a>その他のリソース
- [Git のドキュメント](https://git-scm.com/documentation)
