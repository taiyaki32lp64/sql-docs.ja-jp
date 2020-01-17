---
title: 手順 4:レッスン 5 のチュートリアル パッケージのテスト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30f395ed065df5974adf6146a4ee12d0c7b472f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890944"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>手順 4:レッスン 5 のチュートリアル パッケージのテスト
  パッケージを実行すると、そのときに更新される変数から `Directory` の値が取得されます。パッケージの作成時に指定した元の名前は使用されません。 この変数の値は、SSISTutorial.dtsConfig ファイルにより生成されます。  
  
 パッケージの実行時に、Directory プロパティが新しい値に更新されているかどうかを確認するには、パッケージを実行してみます。 3 つのサンプル データ ファイルのみが新しいディレクトリにコピーされるため、データ フローは 3 回だけ実行されます。元のフォルダーの 14 ファイルには反復処理は実行されません。  
  
## <a name="checking-the-package-layout"></a>パッケージ レイアウトの確認  
 パッケージをテストする前に、次の図に示すオブジェクトがレッスン 5 のパッケージの制御フローとデータ フローに含まれていることを確認します。 制御フローはレッスン 4 の制御フローと同じである必要があります。 データ フローはレッスン 4 のデータ フローと同じである必要があります。  
  
 **制御フロー**  
  
 ![パッケージ内の制御フロー](../../2014/tutorials/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
 **データ フロー**  
  
 ![パッケージ内のデータ フロー](../../2014/tutorials/media/task9lesson1data.gif "パッケージ内のデータ フロー")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>レッスン 5 で作成したチュートリアル パッケージをテストするには  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
2.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 6:プロジェクト配置モデルでパラメーターの使用](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
