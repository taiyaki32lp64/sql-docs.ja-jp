---
title: "レッスン 5: 追加のパッケージ配置モデルの SSIS パッケージの構成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a16217f90b9120993663d9046c8178e62451111
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する
パッケージ構成を使用すれば、開発環境の外部からランタイムのプロパティと変数を設定できます。 この構成により、配置と配信が容易で柔軟なパッケージを開発できます。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]次の種類の構成を提供します。  
  
-   XML 構成ファイル  
  
-   環境変数  
  
-   レジストリ エントリ  
  
-   親パッケージ変数  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル  
  
このレッスンでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 「レッスン 4: SSIS でエラー フロー リダイレクションを追加する」 [で作成した単純な](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) パッケージを変更し、パッケージ配置モデルを使用してパッケージの構成を利用します。 またチュートリアルに含まれている、レッスン 4 を完了した状態のパッケージをコピーすることもできます。 パッケージ構成ウィザードを使用し、Foreach ループ コンテナーの **Directory** プロパティを更新する XML 構成を作成します。具体的には、Directory プロパティにマップされているパッケージ レベル変数を使用します。 構成ファイルを作成したら、開発環境の外部から変数の値を修正し、修正したプロパティに新しいサンプル データ フォルダーを参照させます。 パッケージを再度実行すると、構成ファイルによって変数の値が生成されます。さらに、この変数は **Directory**プロパティを更新します。 結果として、パッケージにハードコーディングされた元のフォルダーのファイルではなく、新しいデータ フォルダーのファイルに対してパッケージが繰り返し実行されます。  
  
> [!IMPORTANT]  
> このチュートリアルには、 **AdventureWorksDW2012** サンプル データベースが必要です。 **AdventureWorksDW2012**をインストールしてデプロイする方法の詳細については、「 [Reporting Services Product Samples Project on CodePlex (CodePlex でのサービス製品サンプルのレポート)](http://go.microsoft.com/fwlink/p/?LinkID=526910)」をご覧ください。  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [手順 1: レッスン 4 のパッケージのコピー](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [手順 2: を有効にして、パッケージの構成を構成します。](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [手順 3: Directory プロパティの構成値を変更します。](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [手順 4: レッスン 5 のチュートリアル パッケージのテスト](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
  
-   [手順 1: レッスン 4 のパッケージのコピー](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
