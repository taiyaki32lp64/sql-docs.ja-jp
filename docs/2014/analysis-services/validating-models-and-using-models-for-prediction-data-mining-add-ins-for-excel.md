---
title: モデルの検証とモデルを使用して予測 (データ マイニング Excel 用アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97268dac1fef029bc35ff702ace0d422ee296d65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065498"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>モデルの検証と予測用モデルの使用 (Excel 用データ マイニング アドイン)
  モデルのテストと検証は、データ マイニング プロセスにおける重要な手順です。 実際のデータに対するマイニング モデルの性能を、運用環境に配置する前に知っておく必要があります。  
  
 データ マイニング アドインには、構築したモデルをテストし、そのモデルを使用して予測と提案を作成するためのツールが含まれています。  
  
## <a name="accuracy-chart"></a>精度チャート  
 **精度チャート**ウィザードでは、予測クエリを作成し、リフト チャートまたは散布図を作成してデータ マイニング モデルのパフォーマンスを評価します。 ほぼ同じ構造を持つ 2 つのモデルを区別し、どちらの予測精度が高いかを調べるにはリフト チャートが有効です。  
  
 [精度チャート&#40;SQL Server データ マイニング アドイン&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>分類マトリックス  
 **分類マトリックス**ウィザードを使用して、分類モデルのパフォーマンスを評価する予測クエリを作成できます。 モデルによって生成された正確な予測と不正確な予測を両方示す概要グラフが出力されます。 分類マトリックスは、モデルによって値が正しく予測された頻度だけでなく、モデルによって最も頻繁に誤って予測された値も示されるので、非常に便利なツールです。  
  
 [分類マトリックス&#40;SQL Server データ マイニング アドイン&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>利益チャート  
 **利益チャート**ウィザードでは、データ マイニング モデルを使用する利点を比較検討し、偽陽性と偽陰性のコストを評価できます。  
  
 この種類のチャートでは、モデルの予測精度が測定され、単位あたりのコストと全体のコストが組み込まれます。  
  
 [利益チャート&#40;SQL Server データ マイニング アドイン&#41;](profit-chart-sql-server-data-mining-add-ins.md)します。  
  
## <a name="cross-validation"></a>クロス検証  
 クロス検証は、データ セットの妥当性を評価しデータ セットに対するマイニング モデルの精度を評価するための、データ マイニング コミュニティで確立された方法です。 クロス検証では、データ セットをサブセットに分割し、モデルの作成、トレーニング、およびテストを各サブセットに対して繰り返し実行します。  
  
 **クロス検証**ウィザードによって、データを分割するフォールドの数を指定することができ、これらのセクション間で相違点を統計的に説明するクロス検証レポートを提供します。 これに基づいて、モデルが、すべてのトレーニング データに対して適切に機能しているか、特定のサブセットに偏っているかを判断できます。  
  
 [クロス検証&#40;SQL Server データ マイニング アドイン&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>クエリ ウィザード  
 **クエリ**ウィザードは対話型のツールであり、予測クエリを構築するのに役立ちます。 クエリによって、提案や将来の予測などを生成する方法が定義されます。  
  
 **クエリ**ウィザード、モデルを選択してからテーブルまたは範囲、または単一の値として、入力データを指定し、ウィザードを使用して、出力先の列を選択できます。 また、確率スコアやその他の有用な統計情報を生成する関数をクエリに追加することもできます。  
  
 [クエリ&#40;SQL Server データ マイニング アドイン&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>詳細クエリ エディター  
 **詳細クエリ エディター**すべての種類の作成にカスタム クエリを実行しているものからの DMX ステートメントをビルドするのに役立つ、対話型ダイアログ ボックスので構成された設定とモデルの削除、新しいモデルをトレーニング、またはセットの新しいデータを作成します。  
  
 [詳細データ マイニング クエリ エディター](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>関連項目  
 [探索とデータのクリーニング](exploring-and-cleaning-data.md)   
 [データ マイニング モデルを作成します。](creating-a-data-mining-model.md)   
 [展開して、マイニング モデルのスケーリング&#40;データ マイニング Excel 用アドイン&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
