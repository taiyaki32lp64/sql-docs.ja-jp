---
title: データ マイニング クエリ タスクと操作方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 24ccf065a393e9534f3f4a3f830f90e3d1d5e5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084946"
---
# <a name="data-mining-query-tasks-and-how-tos"></a>データ マイニングのクエリ タスクと操作方法
  データ マイニング モデルを利用する場合は、クエリを作成できることが不可欠です。 ここでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で提供されるツールを使用して、データ マイニング モデルに対するクエリの作成例のリンクを示します。 データ マイニング クエリとは何かに関する情報、または作成できるさまざまな種類のクエリに関する情報が必要な場合は、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。  
  
## <a name="creating-queries-with-prediction-query-builder"></a>予測クエリ ビルダーでのクエリの作成  
 予測クエリ ビルダーは、データ マイニング モデルに対するクエリをグラフィカルに作成する方法として [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の両方で提供されます。 次の各トピックでは、モデルの選択、データ ソースの指定、予測のカスタマイズ、および出力の保存の方法について説明します。  
  
-   [予測クエリ ビルダーを使用した予測クエリの作成](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [データ マイニング デザイナーでの単一クエリの作成](create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [予測クエリ ビルダーを使用した予測クエリの作成](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [予測クエリの結果の表示および保存](view-and-save-the-results-of-a-prediction-query.md)  
  
-   [手動での予測クエリの編集](manually-edit-a-prediction-query.md)  
  
-   [モデルへの予測関数の適用](apply-prediction-functions-to-a-model.md)  
  
-   [予測クエリの入力データの選択およびマップ](choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>他のデータ マイニング クエリ ツールの使用  
 予測クエリ ビルダーの使用に加えて、DMX または XMLA を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] にクエリを直接入力することもできます。 プログラムを使用して予測クエリを作成し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに送信することもできます。 次の各トピックでは、予測クエリ ビルダーの外部で予測クエリを作成および操作する方法の詳細を説明します。  
  
 [テンプレートからの単一予測クエリの作成](create-a-singleton-prediction-query-from-a-template.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のツールを使用して、予測クエリを作成および実行する方法について説明します。  
  
 [テンプレートからの単一予測クエリの作成](create-a-singleton-prediction-query-from-a-template.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に付属しているテンプレートを使用して、予測クエリにパラメーターを追加する方法について説明します。  
  
 [データ マイニング クエリのタイムアウト値の変更](change-the-time-out-value-for-data-mining-queries.md)  
 データ マイニング クエリ関連の動作を制御するサーバーのプロパティを設定する方法について説明します。  
  
 [マイニング モデルのコンテンツ クエリの作成](create-a-content-query-on-a-mining-model.md)  
 データ マイニング スキーマ行セットを使用して、マイニング モデルに格納されている詳細情報を返すクエリを作成する方法について説明します。  
  
 [XMLA を使用したデータ マイニング クエリの作成](create-a-data-mining-query-by-using-xmla.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の XMLA テンプレートを使用して、マイニング モデル コンテンツに対するクエリを作成する方法について説明します。  
  
## <a name="see-also"></a>関連項目  
 [クエリと式言語のリファレンス (Analysis Services)](https://msdn.microsoft.com/library/gg492188(SQL.130).aspx)   
 [データ マイニングのストアド プロシージャ (Analysis Services - データ マイニング)](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
