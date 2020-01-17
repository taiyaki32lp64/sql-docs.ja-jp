---
title: DMX の Select ステートメントを理解する |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8cc28e9394cabee4dd32e8e84ee02517de415a75
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893069"
---
# <a name="understanding-the-dmx-select-statement"></a>DMX SELECTステートメントについて
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [SELECT](../dmx/select-dmx.md)ステートメントは、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のデータ マイニング拡張機能 (DMX) で作成するほとんどのクエリの基礎になります。 このステートメントでは、データ マイニング モデルの参照や予測などのさまざまなタスクを実行することができます。  
  
 **SELECT**ステートメントを使用して実行できるタスクは次のとおりです:  
  
-   データマイニングモデルを参照します。 スキーマ行セットは、モデルの構造を定義します。  
  
-   マイニングモデル列の使用可能な値を検出します。  
  
-   マイニングモデル内のノードに割り当てられているケースを参照するか、代表的なケースを取得します。  
  
-   さまざまな入力を使用した予測の作成。  
  
-   マイニングモデルをコピーします。  
  
 これらの各タスクでは、データ*ドメイン*を呼び出す別のデータセットを使用します。 データドメインは、ステートメントの**from**句で定義します。  
  
-   データのセットを定義するルールや予測の作成に使用する式など、データマイニングモデル自体のオブジェクトを検索します。  
  
     その場合は、モデル自体に格納されているメタデータを確認する必要があります。 したがって、データドメインはデータマイニングスキーマ行セットの列です。  
  
-   モデルの作成に使用されたケースから詳細情報を取得する必要があるとします。  
  
     この場合は、データ ドメインであるマイニング構造にドリルスルーして、Gender、Bike Buyer などの列の各行を確認します。  
  
 **重要:** 式の一覧または **WHERE** 句に含まれているものは全て、 **FROM** 句で定義されているデータ ドメインから取得する必要があります。データ ドメインを混在させることはできません。 データ ドメインを混在させることはできません。  
  
##  <a name="Select_Types"></a>SELECT型  
 **SELECT**ステートメントの構文は、さまざまなタスクをサポートしています。 これらのタスクを実行するには、以下のパターンを使用します。  
  
-   [予測](#Predicting)  
  
-   [ブラウザー](#Browsing)  
  
-   [,](#Copying)  
  
-   [有効化](#Drillthrough)  
  
###  <a name="Predicting"></a>予測  
 次の種類のクエリを使用して、マイニングモデルに基づいて予測を実行できます。  
  
 予測結合**SELECT**ステートメントの**FROM**句と**WHERE**句の中に、ブラウズまたは予測**SELECT**ステートメントのいずれかを含めることができます。  
  
|クエリの型|説明|  
|----------------|-----------------|  
|SELECT FROM [自然] 予測結合|マイニング モデル内の列を内部データ ソースの列に結合させることで作成される予測を返します。<br /><br /> このクエリの種類のドメインは、モデルからの予測可能列と入力データソースの列です。<br /><br /> [モデル&#62;予測&#60;から DMX へ&#40;の結合を選択します&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [予測クエリ &#40;データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|モデルから *\<選択 >*|マイニング モデルにのみ基づいた、予測可能な列の最も可能性の高い状態を返します。 このクエリの型は、空の予測結合で予測を作成するための近道となります。<br /><br /> このクエリの型のドメインは、モデルからの予測可能列です。<br /><br /> [&#62;モデル&#40;DMX &#60;から選択&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [予測クエリ &#40;データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Select 型に戻る](#Select_Types)  
  
###  <a name="Browsing"></a>ブラウザー  
 マイニング モデルの内容を参照するには、次のクエリの型を使用します。  
  
|クエリの型|説明|  
|----------------|-----------------|  
|*\<モデルから DISTINCT を選択 >*|指定された列のマイニングモデルからすべての状態値を返します。<br /><br /> このクエリの種類のデータドメインはデータマイニングモデルです。<br /><br /> [&#62;モデル&#40;DMX から&#60;DISTINCT を選択&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [コンテンツ クエリ &#40;データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|*\<モデル >* から選択します。情報|マイニング モデルを説明する内容を返します。<br /><br /> このクエリの種類のデータドメインは、コンテンツスキーマ行セットです。<br /><br /> [[モデル&#60;&#62;から] を選択します。コンテンツ&#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [コンテンツ クエリ &#40;データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|*\<モデル >* から選択します。DIMENSION_CONTENT|マイニング モデルを説明する内容を返します。<br /><br /> このクエリの種類のデータドメインは、コンテンツスキーマ行セットです。<br /><br /> [[モデル&#60;&#62;から] を選択します。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|*\<モデル >* から選択します。PMML|この機能をサポートするアルゴリズムに対して、マイニング モデルの Predictive Model Markup Language (PMML) 表記法を返します。<br /><br /> このクエリの型のドメインは PMML スキーマ行セットです。<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|  
  
 [Select 型に戻る](#Select_Types)  
  
###  <a name="Copying"></a>,  
 マイニングモデルとそれに関連付けられているマイニング構造を新しいモデルにコピーし、ステートメント内でモデルの名前を変更することができます。  
  
|クエリの型|説明|  
|----------------|-----------------|  
|新しいモデルの選択 >  *\<*|マイニングモデルのコピーを作成します。<br /><br /> このクエリの種類のドメインは、データマイニングモデルです。<br /><br /> [SELECT &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Select 型に戻る](#Select_Types)  
  
###  <a name="Drillthrough"></a>有効化  
 モデルの学習に使用されたケース、またはケースの表記を参照するには、次のクエリの型を使用します。  
  
|クエリの型|説明|  
|----------------|-----------------|  
|*\<モデル >* から選択します。場合|マイニングモデルのトレーニングに使用するケースを返します。<br /><br /> このクエリの種類のドメインは、データマイニングモデルです。<br /><br /> [[モデル&#60;&#62;から] を選択します。DMX &#40;のケース&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [DMX を使用したドリルスルー クエリの作成](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|*\<モデル >* から選択します。SAMPLE_CASES|マイニング モデルのトレーニングに使用されたケースを表すサンプル ケースを返します。<br /><br /> このクエリの種類のドメインは、データマイニングモデルです。<br /><br /> [[モデル&#60;&#62;から] を選択します。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|*\<構造 >* から選択します。 場合|マイニングモデルのトレーニングで一部の詳細が使用されていない場合でも、基になるマイニング構造から詳細なデータ行を返します。<br /><br /> [[構造&#60;&#62;から] を選択します。場合](../dmx/select-from-structure-cases.md)<br /><br /> [ドリルスルー クエリ &#40;データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Select 型に戻る](#Select_Types)  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
