---
title: 比率サンプリング変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtrans.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 27d3ff9ef1c6296a6bec2040f9caefd477568bfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900148"
---
# <a name="percentage-sampling-transformation"></a>比率サンプリング変換
  比率サンプリング変換は、変換入力行の比率を選択することにより、サンプル データセットを作成します。 サンプル データセットとは、変換入力からランダムに行を選択し、その結果、入力のサンプルとなるデータセットのことです。  
  
> [!NOTE]  
>  比率サンプリング変換は、指定した比率に加え、サンプル出力に行を含めるかどうかを決定するアルゴリズムを使用します。 したがって、サンプル出力の行数は、指定した比率を正確に反映しない場合があります。 たとえば、25,000 行の入力データセットに対して 10% を指定した場合、2,500 行のサンプルが生成されず、サンプルの行がこの数を多少前後することがあります。  
  
 比率サンプリング変換は、特にデータ マイニングに役立ちます。 この変換を使用すると、データセットをランダムに 2 つのデータセットに分割できます。たとえば、1 つをデータ マイニング モデルの学習用に、もう 1 つはそのモデルのテスト用に分割します。  
  
 また、比率サンプリング変換は、パッケージ開発用のサンプル データセットを作成するうえで役立ちます。 比率サンプリング変換をデータ フローに適用すると、データの特性を保持したまま、データセットのサイズを一様に縮小できます。 したがって、テスト パッケージは、サイズは小さいが代表的なデータセットを使用するため、実行速度は速くなります。  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>比率サンプリング変換の構成  
 サンプリング シードを指定して、変換が行の選択に使用する乱数ジェネレーターの動作を変更できます。 同じサンプリング シードが使用される場合、この変換は、常に同じサンプル出力を作成します。 シードを指定しない場合、この変換はオペレーティング システムのティック数を使用して乱数を作成します。 したがって、パッケージの開発やテスト中に変換結果を確認する際は標準シードを使用するように選択し、パッケージの稼働時にはランダム シードを使用するように変更します。  
  
 この変換は、行サンプリング変換と同様です。ただし、行サンプリング変換は、指定する入力行数を選択してサンプル データセットを作成します。 詳細については、「 [Row Sampling Transformation](row-sampling-transformation.md)」を参照してください。  
  
 比率サンプリング変換には、`SamplingValue` カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力と 2 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[比率サンプリング変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [比率サンプリング変換エディター](../../percentage-sampling-transformation-editor.md)」を参照してください。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
