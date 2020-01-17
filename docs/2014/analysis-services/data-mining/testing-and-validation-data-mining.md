---
title: テストと検証 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing data mining models
- comparing mining models
- continuous attribute charts
- data mining [Analysis Services], models
- charts [Analysis Services]
- predictive modeling [Analysis Services]
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- confidence scores [data mining]
- displaying mining accuracy
- predictions [Analysis Services], comparing mining models
- scoring [data mining]
- lift charts [Analysis Services]
- classification matrix [Analysis Services]
- CRISP-DM
- accuracy testing [data mining]
ms.assetid: 197144f5-21ed-4009-b448-fe412fb3916c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 159760722a62969b79ce738e7928739ff2bb15ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082798"
---
# <a name="testing-and-validation-data-mining"></a>テストおよび検証 (データ マイニング)
  検証とは、実際のデータに対するマイニング モデルの性能を評価するプロセスです。 運用環境に配置する前に品質や特性を理解してマイニング モデルを検証しておくことが重要です。  
  
 このセクションでは、モデルの品質に関するいくつかの基本的な概念について説明し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に用意されているモデル検証のための戦略について説明します。 大規模なデータ マイニング プロセス内でモデルの検証がどのように位置付けられているかの概要については、「 [データ マイニング ソリューション](data-mining-solutions.md)」を参照してください。  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>データ マイニング モデルのテストと検証の方法  
 データ マイニング モデルの品質や特性を評価する方法は多数あります。  
  
-   統計的妥当性の各種メジャーを使用して、データまたはモデルに問題があるかどうかを判定します。  
  
-   データをトレーニング セットとテスト セットに分割して、予測の精度をテストします。  
  
-   発見されたパターンが目標とするビジネス シナリオにおいて有意であるかどうか、ビジネスの専門家にデータ マイニング モデルの結果を評価してもらいます。  
  
 これらの方法はすべてデータ マイニング手法として有用であり、特定の問題に対応するためにモデルの作成、テスト、および調整を行うときに繰り返し使用されます。 モデルが満足できるものであること、または十分なデータがあることを単独で示すことができる包括的な規則はありません。  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>データ マイニング モデルを検証するための基準の定義  
 通常、データ マイニングの評価基準は、精度、信頼性、および実用性に分類されます。  
  
 *精度* は、モデルの結果が提供されたデータ内の属性と密接な関係があるかどうかを示すメジャーです。 精度のメジャーは各種ありますが、精度のメジャーはすべて、使用されるデータに依存します。 実際には、値が不足していたり概算値であったり、複数のプロセスによってデータが変更されている場合があります。 特に調査と開発のフェーズでは、データの特性がきわめて均一である場合は特に、データ内に一定量のエラーを認める必要があります。 たとえば、過去の売上に基づいて特定の店舗の売上を予測するモデルは、その店舗で継続的に誤った会計手続きが行われていたとしても、密接な相関関係を持ち非常に正確なモデルになります。 したがって、精度の測定は、信頼性の評価とのバランスを取る必要があります。  
  
 *信頼性* は、異なるデータセットに対するデータ マイニング モデルの性能を示します。 提供されるテスト データに関係なく同じ種類の予測が生成される場合や同種の一般的パターンが発見される場合、データ マイニング モデルは信頼性が高いと見なされます。 たとえば、誤った会計手続きが行われていた店舗に対して生成されたモデルは、他の店舗用にはうまく一般化できず、信頼性がないことになります。  
  
 *実用性* には、モデルによって有用な情報が提供されるかどうかを示す各種のメトリックが含まれます。 たとえば、店舗の場所と売上の相関関係を求めるデータ マイニング モデルの場合、高い精度と信頼性を持つと評価される一方で、同じ場所にさらに店舗を追加してその結果を一般化することができないという理由で実用的でない可能性があります。 さらに、このデータ マイニング モデルでは、特定の場所でなぜ売上が多いのかという基本的な業務上の疑問点に対する回答が示されません。 また、モデルはデータ内の相互相関に基づいているので、モデルが成果を挙げているように見えても実際は無意味である場合もあります。  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>マイニング モデルのテストと検証のツール  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、データ マイニング ソリューションを検証するための複数の方法をサポートすると共に、データ マイニング テスト手法のすべてのフェーズをサポートしています。  
  
-   テスト セットとトレーニング セットへのデータのパーティション分割。  
  
-   同じソース データの異なる組み合わせでトレーニングおよびテストを行うためのモデルのフィルター処理。  
  
-   *リフト* と *ゲイン*の測定。 *リフト チャート* は、ランダムな推測と比較したときにデータ マイニング モデルを使用したことによる改善を視覚化するための方法です。  
  
-   データセットの *相互検証* の実行  
  
-   *分類マトリックス*の生成。 これらのチャートでは、良い推量と悪い推量をテーブルに並べ替えて、モデルによるターゲット値の予測精度を簡単に評価できるようにします。  
  
-   回帰式の適合性を評価するための *散布図* の作成。  
  
-   推奨設定の価値を評価するために財務的利益またはコストをマイニング モデルの使用に関連付ける *利益チャート* の作成。  
  
 これらの基準は、データ マイニング モデルが業務上の質問に答えるものであるかを判断するためのものではなく、予測分析でデータの信頼性を評価するため、および開発プロセスで特定の繰り返し処理を使用するかどうかの決定を導きだすために使用できる客観的な測定値を提供するものです。  
  
 このセクションのトピックでは、各方法の概要を説明すると共に、SQL Server のデータ マイニングを使用して作成したモデルの精度を測定するプロセスの手順を説明します。  
  
### <a name="related-topics"></a>関連項目  
  
|トピック|リンク|  
|------------|-----------|  
|ウィザードまたは DMX コマンドを使用してテスト用データ セットを設定する方法を学ぶ|[トレーニング データ セットとテスト データ セット](training-and-testing-data-sets.md)|  
|マイニング構造内のデータの分布と代表性をテストする方法を学ぶ|[相互検証 &#40;Analysis Services - データ マイニング&#41;](cross-validation-analysis-services-data-mining.md)|  
|[!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]で用意されている精度チャートの種類について学ぶ|[リフト チャート (Analysis Services - データ マイニング)](lift-chart-analysis-services-data-mining.md)<br /><br /> [利益チャート (Analysis Services - データ マイニング)](profit-chart-analysis-services-data-mining.md)<br /><br /> [散布図 (Analysis Services - データ マイニング)](scatter-plot-analysis-services-data-mining.md)|  
|真陽性、偽陽性、真陰性、および偽陰性の実際の数値を評価する分類マトリックス (混同マトリックスと呼ばれることもある) の作成方法について学びます。|[分類マトリックス &#40;Analysis Services - データ マイニング&#41;](classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング ツール](data-mining-tools.md)   
 [データ マイニング ソリューション](data-mining-solutions.md)   
 [テストおよび検証タスク、および操作方法 (データ マイニング)](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
