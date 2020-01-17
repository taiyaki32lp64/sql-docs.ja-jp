---
title: 'レッスン 5: パッケージ配置モデルのパッケージ構成の追加 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25922725e202bc7b38e2c6141a097df1af119ed2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767421"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>レッスン 5: パッケージ配置モデルのパッケージ構成の追加
  パッケージ構成を使用すれば、開発環境の外部からランタイムのプロパティと変数を設定できます。 この構成により、配置と配信が容易で柔軟なパッケージを開発できます。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、次の種類の構成が用意されています。  
  
-   XML 構成ファイル  
  
-   環境変数  
  
-   レジストリ エントリ  
  
-   親パッケージ変数  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル  
  
 このレッスンでは、単純なものを変更します[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]で作成したパッケージ[レッスン 4。エラー フロー リダイレクトの追加](lesson-4-add-error-flow-redirection-with-ssis.md)をパッケージ配置モデルを使用して、パッケージの構成を利用します。 またチュートリアルに含まれている、レッスン 4 を完了した状態のパッケージをコピーすることもできます。 パッケージ構成ウィザードを使用し、Foreach ループ コンテナーの `Directory` プロパティを更新する XML 構成を作成します。具体的には、Directory プロパティにマップされているパッケージ レベル変数を使用します。 構成ファイルを作成したら、開発環境の外部から変数の値を修正し、修正したプロパティに新しいサンプル データ フォルダーを参照させます。 パッケージをもう一度実行すると、構成ファイルは、変数の値を設定します、さらに、変数を更新、`Directory`プロパティ。 結果として、パッケージにハードコーディングされた元のフォルダーのファイルではなく、新しいデータ フォルダーのファイルに対してパッケージが繰り返し実行されます。  
  
> [!IMPORTANT]  
>  このチュートリアルには、 **AdventureWorksDW2012** サンプル データベースが必要です。 **AdventureWorksDW2012**をインストールしてデプロイする方法の詳細については、「 [Reporting Services Product Samples Project on CodePlex (CodePlex でのサービス製品サンプルのレポート)](https://go.microsoft.com/fwlink/?LinkID=526910)」をご覧ください。  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンの内容は次のとおりです。  
  
-   [ステップ 1: レッスン 4 のパッケージのコピー](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [手順 2:有効にして、パッケージの構成](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [ステップ 3:Directory プロパティの構成値の変更](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [手順 4:レッスン 5 のチュートリアル パッケージのテスト](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
  
-   [ステップ 1: レッスン 4 のパッケージのコピー](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
