---
title: 分類マトリックス (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- displaying mining accuracy
- confusion matrix [data mining]
- classification matrix [Analysis Services]
- accuracy testing [data mining]
ms.assetid: 5c12f202-2ed9-41fa-bee2-0f7ab3ff058a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 22f8733c816014bbdd29b44c4ed85d5fc3d2127d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085787"
---
# <a name="classification-matrix-analysis-services---data-mining"></a>分類マトリックス (Analysis Services - データ マイニング)
  *分類マトリックス*は、モデルのすべてのケースについて、予測値が実際の値と一致したかどうかを判断してカテゴリに分類します。 各カテゴリのすべてのケースがカウントされ、合計がマトリックスに表示されます。 分類マトリックスは統計モデルの評価に使用する標準のツールで、 *混同行列*とも呼ばれます。  
  
 **[分類マトリックス]** オプションを選択して作成されるグラフでは、実際の値が、指定した各予測状態の予測値と比較されます。 各マトリックスの行はモデルの予測値を表し、列は実際の値を表します。 分析で使用されるこれらのカテゴリは、 *偽陽性*, *真陽性*, *偽陰性*、および *真陰性*と呼ばれる場合もあります。  
  
 分類マトリックスは、間違った予測の影響を容易に理解し説明できるため、予測の結果を評価するための重要なツールです。 このマトリックスの各セルに示された数値とパーセンテージを見ると、モデルの予測が正しかった頻度がすぐにわかります。  
  
 ここでは、分類マトリックスを作成する方法と、その結果を解釈する方法について説明します。  
  
## <a name="understanding-the-classification-matrix"></a>分類マトリックスについて  
 「基本的なデータ マイニング チュートリアル」で作成したモデルを例に考えてみましょう。 ターゲット メーリング キャンペーンの作成に [TM_DecisionTree] モデルを使用し、自転車を購入する可能性が最も高いのはどの顧客かを予測することができます。 このモデルのこの期待される有用性をテストするには、結果の属性である [Bike Buyer] の値が既にわかっているデータセットを使用します。 通常は、モデルのトレーニングに使用するマイニング構造を作成したときに確保しておいたテスト データセットを使用します。  
  
 結果の有効値は、"yes" (顧客が自転車を購入する可能性が高い) と "no" (顧客が自転車を購入する可能性が低い) の 2 つだけです。 したがって、結果の分類マトリックスは、比較的単純です。  
  
## <a name="interpreting-the-results"></a>結果の解釈  
 次の表は、TM_DecisionTree モデルの分類マトリックスを示しています。 この予測可能な属性で、0 は "No" を、1 は "Yes" を意味します。  
  
|[予測]|0 (実際の値)|1 (実際の値)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1|121|373|  
  
 値 362 を含む最初の結果セルは、値 0 に対する *真陽性* の数を表します。 値 0 は顧客が自転車を購入しなかったことを表すため、この統計から、モデルが 362 のケースで、自転車を購入しない顧客について正しい値を予測したことがわかります。  
  
 その下の、値 121 を含むセルは、 *偽陽性*の数 (実際には自転車を購入しなかった顧客について購入するとモデルが予測した回数) を表します。  
  
 値 144 を含むセルは、値 1 に対する *偽陽性* の数を表します。 値 1 は顧客が自転車を購入したことを表すため、この統計から、モデルが 144 のケースで、実際には自転車を購入した顧客について購入しないと予測したことがわかります。  
  
 最後の、値 373 を含むセルは、対象の値 1 に対する真陽性の数を表します。 つまり、モデルが 373 のケースで、自転車を購入する顧客を正しく予測したことになります。  
  
 対角線上にあるセルの値を合計すると、モデルの全体的な精度を調べることができます。 一方の対角線からは正しい予測の合計数が、もう一方の対角線からは間違った予測の合計数がわかります。  
  
### <a name="using-multiple-predictable-values"></a>複数の予測可能な値の使用  
 [Bike Buyer] のケースは、取りうる値が 2 つしかないため、特に解釈が簡単です。 予測可能な属性が取りうる値が複数ある場合、分類マトリックスでは、取りうる値が増えるたびに実際の値の列が追加され、予測された各値が一致した数がカウントされます。 次の表は、3 つの値 (0、1、2) を取る別のモデルの結果を示しています。  
  
|[予測]|0 (実際の値)|1 (実際の値)|2 (実際の値)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 列が増えたためにレポートが複雑に見えますが、この追加の詳細が、間違った予測の累積コストを評価する際に非常に役立つ場合もあります。 対角線上のセルの合計を計算したり、さまざまな行の組み合わせの結果を比較したりする際には、 **[分類マトリックス]** タブの **[コピー]** ボタンをクリックして、レポートを Excel に貼り付けることができます。 また、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降をサポートする Excel 用データ マイニング クライアントなどのクライアントを使用して、回数と割合の両方を含む分類レポートを直接 Excel で作成することもできます。 詳細については、「 [SQL Server データ マイニング](https://go.microsoft.com/fwlink/?LinkID=77733)」を参照してください。  
  
## <a name="restrictions-on-the-classification-matrix"></a>分類マトリックスの制限  
 分類マトリックスは、不連続の予測可能な属性でのみ使用できます。  
  
 **[マイニング精度チャート]** デザイナーの **[入力の選択]** タブでモデルを選択する場合、複数のモデルを追加することができますが、 **[分類マトリックス]** タブではモデルごとに別のマトリックスが表示されます。  
  
## <a name="related-content"></a>関連コンテンツ  
 次のトピックには、分類マトリックスやその他のチャートの構築方法と使用方法に関する詳細な情報が含まれています。  
  
|トピック|リンク|  
|------------|-----------|  
|Targeted Mailing モデルのリフト チャートの作成方法に関するチュートリアルが含まれています。|[基本的なデータ マイニング チュートリアル](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|関連するグラフの種類について説明します。|[リフト チャート (Analysis Services - データ マイニング)](lift-chart-analysis-services-data-mining.md)<br /><br /> [利益チャート (Analysis Services - データ マイニング)](profit-chart-analysis-services-data-mining.md)<br /><br /> [散布図 (Analysis Services - データ マイニング)](scatter-plot-analysis-services-data-mining.md)|  
|マイニング モデルとマイニング構造の相互検証の使用法について説明します。|[相互検証 (Analysis Services - データ マイニング)](cross-validation-analysis-services-data-mining.md)|  
|リフト チャートおよびその他の精度チャートを作成する手順について説明します。|[テストおよび検証タスク、および操作方法 (データ マイニング)](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>参照  
 [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)  
  
  
