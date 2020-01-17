---
title: レッスン 2:ループの追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a542b2828a2ea6803a6b4174396e57c7e9d3af4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767554"
---
# <a name="lesson-2-adding-looping"></a>レッスン 2:ループの追加
  「[レッスン 1: プロジェクトと基本パッケージ作成](lesson-1-create-a-project-and-basic-package-with-ssis.md)、単一のフラット ファイル ソースからデータを抽出、変換された、参照変換を使用してデータおよびにデータが最後に読み込まれているパッケージを作成し、 **FactCurrency**ファクト テーブルの**AdventureWorksDW2012**サンプル データベース。  
  
 しかし、抽出、変換、読み込み (ETL) プロセスでフラット ファイルを 1 つだけ使用することはほとんどありません。 通常の ETL プロセスでは、複数のフラット ファイル ソースからデータを抽出します。 複数のソースからデータを抽出するには、反復型の制御フローが必要となります。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、反復やループをパッケージへ簡単に追加できるようになりました。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージ全体をループさせる 2 種類のコンテナーがあります。1 つは Foreach ループ コンテナー、もう 1 つは For ループ コンテナーです。 Foreach ループ コンテナーが列挙子を使用してループを実行するのに対し、For ループ コンテナーは、通常、変数式を使用します。 このレッスンでは Foreach ループ コンテナーを使用します。  
  
 パッケージで Foreach ループ コンテナーを使用すれば、指定した列挙子の各メンバーについて、制御フローを繰り返すことができます。 Foreach ループ コンテナーでは、次のものを列挙できます。  
  
-   ADO レコードセット行  
  
-   ADO .Net スキーマ情報  
  
-   ファイル構造とディレクトリ構造  
  
-   システム変数、パッケージ変数、ユーザー変数  
  
-   変数に含まれる列挙可能なオブジェクト  
  
-   コレクション内のアイテム  
  
-   XML パス言語 (XPath) 式内のノード  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト (SMO)  
  
 このレッスンでは、レッスン 1 で作成した単純な ETL パッケージを修正し、Foreach ループ コンテナーの機能を活用します。 また、ユーザー定義のパッケージ変数を設定し、フォルダー内のすべてのフラット ファイルに対し、チュートリアル パッケージが反復処理を実行できるようにします。 前のレッスンを完了していない場合は、チュートリアルに含まれている、レッスン 1 を完了した状態のパッケージをコピーすることもできます。  
  
 このレッスンでは、データ フローは変更せずに、制御フローのみを変更します。  
  
> [!IMPORTANT]  
>  このチュートリアルには、 **AdventureWorksDW2012** サンプル データベースが必要です。 **AdventureWorksDW2012**をインストールしてデプロイする方法の詳細については、「 [Reporting Services Product Samples Project on CodePlex (CodePlex でのサービス製品サンプルのレポート)](https://go.microsoft.com/fwlink/p/?LinkID=526910)」をご覧ください。  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンの内容は次のとおりです。  
  
-   [ステップ 1: レッスン 1 パッケージのコピー](lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [手順 2:追加して、Foreach ループ コンテナーの構成](lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [ステップ 3:フラット ファイル接続マネージャーの変更](lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [手順 4:レッスン 2 のチュートリアル パッケージのテスト](lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
 [ステップ 1: レッスン 1 パッケージのコピー](lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>参照  
 [For ループ コンテナー](control-flow/for-loop-container.md)  
  
  
