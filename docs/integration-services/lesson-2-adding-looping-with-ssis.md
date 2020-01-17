---
title: レッスン 2:SSIS でのループの追加 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ccd3be3203aae382cda239ed6d7bdc2fa224923b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296052"
---
# <a name="lesson-2-add-looping-with-ssis"></a>レッスン 2:SSIS でのループの追加

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



「[レッスン 1: SSIS によるプロジェクトと基本パッケージの作成](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)」で、1 つのフラット ファイル ソースからデータを抽出するパッケージを作成しました。 抽出されたデータは参照変換を使用して変換されます。 最後に、パッケージによって、**AdventureWorksDW2012** サンプル データベースの **FactCurrencyRate** ファクト テーブルのコピーにそのデータが読み込まれます。  
  
抽出、変換、読み込み (ETL) プロセスでは通常、複数のフラット ファイル ソースからデータが抽出されます。 複数のソースからデータを抽出するには、反復型の制御フローが必要となります。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、繰り返しやループをパッケージに簡単に追加できます。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージ全体をループさせる 2 種類のコンテナーがあります。1 つは Foreach ループ コンテナー、もう 1 つは For ループ コンテナーです。 Foreach ループ コンテナーではループに列挙子が使用されるのに対して、For ループ コンテナーでは通常、変数式が使用されます。 このレッスンでは Foreach ループ コンテナーを使用します。  
  
パッケージで Foreach ループ コンテナーを使用すれば、指定した列挙子の各メンバーについて、制御フローを繰り返すことができます。 Foreach ループ コンテナーでは、次のものを列挙できます。  
  
-   ADO レコードセット行  
  
-   ADO .Net スキーマ情報  
  
-   ファイル構造とディレクトリ構造  
  
-   システム変数、パッケージ変数、ユーザー変数  
  
-   変数の列挙可能なオブジェクト  
  
-   コレクション内のアイテム  
  
-   XML パス言語 (XPath) 式内のノード  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト (SMO)  
  
このレッスンでは、Foreach ループ コンテナーを使用するようにレッスン 1 のサンプル ETL パッケージを変更し、そのパッケージにユーザー定義のパッケージ変数を設定します。 サンプル フォルダーで一致するファイルを反復処理する際、その変数が使用されます。   
  
このレッスンでは、データ フローは変更せずに、制御フローのみを変更します。  
  
> [!NOTE]  
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。

## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:レッスン 1 のパッケージをコピーする](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [ステップ 2:Foreach ループ コンテナーの追加および構成](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [ステップ 3:フラット ファイル接続マネージャーの変更](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [ステップ 4:レッスン 2 で作成したチュートリアル パッケージのテスト](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:レッスン 1 のパッケージをコピーする](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>参照  
[For ループ コンテナー](../integration-services/control-flow/for-loop-container.md)  
  
  
  
