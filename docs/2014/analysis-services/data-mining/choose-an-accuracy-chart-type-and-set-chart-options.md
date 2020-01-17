---
title: 精度チャートの種類と設定を選択してグラフのオプション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d9f375eb2d55c396000b7c2d7a14614153861e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085822"
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>精度チャートの種類の選択とグラフのオプションの設定
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、マイニング モデルの有効性を判断する複数の方法を提供します。 各モデルまたは構造に対して作成できる精度チャートの種類は、以下の要因によって異なります。  
  
-   モデルの作成に使用したアルゴリズムの種類  
  
-   予測可能な属性のデータ型  
  
-   測定する予測可能な属性の数  
  
 このトピックでは、各種の精度チャートの概要について説明します。  
  
 **注:** グラフとその定義は保存されません。 グラフが含まれているウィンドウを閉じた場合は、グラフを作成し直す必要があります。  
  
## <a name="accuracy-chart-types"></a>精度チャートの種類  
 選択するグラフの種類によっては、さらにオプションを構成したり、グラフを参照したり、グラフをクリップボードにコピーして Excel でデータを操作したりできます。  
  
#### <a name="lift-chart"></a>リフト チャート  
 モデルおよびテスト用データのオプションを構成した後、 **[リフト チャート]** タブをクリックすると、結果が表示されます。 グラフをクリップボードにコピーしたり、個々の傾向線やデータ ポイントの詳細をマイニング凡例で確認したりすることもできます。  
  
#### <a name="profit-chart"></a>利益チャート  
 モデルおよびテスト用データのオプションを構成した後、 **[リフト チャート]** タブをクリックし、 **[グラフの種類]** ボックスの一覧の **[利益チャート]** を選択します。利益チャートのオプションを設定して **[OK]** をクリックすると、結果が表示されます。  
  
 必要に応じて **[利益チャートの設定]** ダイアログ ボックスを繰り返し使用して、別のコストでグラフを再表示してみることもできます。 マイニング凡例には、各モデルの推定利益に関する詳細情報が含まれています。 グラフとマイニング凡例の内容をクリップボードにコピーして、Excel で操作することもできます。  
  
#### <a name="scatter-plot"></a>散布図  
 適切な種類のモデルが選択されている場合に **[リフト チャート]** タブをクリックすると、グラフの種類が自動的に **[散布図]** に設定されて、散布図が表示されます。 それ以上の構成はできません。 グラフをクリップボードにコピーして、Excel やその他のアプリケーションにグラフィックとして貼り付けることもできます。  
  
#### <a name="classification-matrix"></a>分類マトリックス  
 分類マトリックスの場合は、 **[入力の選択]** タブを使用してモデルおよびテスト用データを選択した後、 **[分類マトリックス]** タブをクリックすると、結果が表示されます。  
  
 分類マトリックスの内容はすべてのモデルの種類で同じであり、構成することはできません。 グラフ内のデータをクリップボードにコピーして、Excel で操作することができます。  
  
#### <a name="cross-validation-report"></a>クロス検証レポート  
 クロス検証レポートの場合は、ソリューション エクスプローラーでマイニング構造またはマイニング モデルを選択した後、 **[クロス検証]** タブをクリックして、関連するすべてのオプションを構成します。その後、 **[結果の取得]** をクリックすると、レポートが生成されます。 それ以上の構成はできません。  
  
 クロス検証レポートの形式はすべてのモデルの種類で同じであり、構成することはできません。 ただし、レポートの内容は、分析するモデルの種類や、予測可能な属性のデータ型によって異なります。 レポートの結果をクリップボードにコピーして、データを Excel で操作することもできます。  
  
  
