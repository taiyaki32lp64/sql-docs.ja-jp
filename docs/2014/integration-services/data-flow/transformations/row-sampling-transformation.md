---
title: 行サンプリング変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowsamplingtrans.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 954e8b2a2f36ccab1cff97174089560913291074
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770398"
---
# <a name="row-sampling-transformation"></a>行サンプリング変換
  行サンプリング変換を使用すると、入力データセットからランダムに選択されたサブセットを取得できます。 出力サンプルの正確なサイズを指定したり、乱数ジェネレーターのシード値を指定できます。  
  
 ランダム サンプリング用のアプリケーションには、多くの種類があります。 たとえば、ある会社がくじ引きを行って、ランダムに選択された 50 人の社員を当選者とする場合、社員データベースに対して行サンプリング変換を行い、正確な数の当選者を生成できます。  
  
 また、行サンプリング変換は、パッケージの開発中にサイズは小さいが標本化されたデータセットを作成する際に便利です。 十分に標本化されたデータがあれば、パッケージの実行とデータ変換のテストを行うことができます。この場合、完全なデータセットではなくランダム サンプルを使用するため、より迅速にテストできます。 テスト パッケージで使用されるサンプル データセットは常に同じサイズであるため、サンプル サブセットを使用することで、パッケージのパフォーマンスの問題をより簡単に判別することもできます。  
  
 この変換は、比率サンプリング変換と同様です。ただし、比率サンプリング変換は、入力行数の比率を選択してサンプル データセットを作成します。 「 [比率サンプリング変換](percentage-sampling-transformation.md)」をご覧ください。  
  
## <a name="configuring-the-row-sampling-transformation"></a>行サンプリング変換の構成  
 行サンプリング変換は、指定された数の変換入力行を選択してサンプル データセットを作成します。 変換入力からの行の選択はランダムに行われるため、結果サンプルは入力の標本となります。 乱数ジェネレーターで使用するシード値を指定すると、変換による行の選択方法を制御することもできます。  
  
 同じ変換入力で同じランダム シードを使用すると、常に同じサンプル出力が作成されます。 シードを指定しない場合、この変換はオペレーティング システムのティック数を使用して乱数を作成します。 したがって、パッケージの開発およびテスト中に変換結果を確認するためにテスト中は同じシード値を使用し、パッケージの実稼働時にランダム シードへ変更することができます。  
  
 行サンプリング変換には、`SamplingValue` カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](transformation-custom-properties.md)」をご覧ください。  
  
 この変換は、1 つの入力と 2 つの出力をとります。 エラー出力はありません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[行サンプリング変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「[行サンプリング変換エディター &#40;[サンプリング] ページ&#41;](../../row-sampling-transformation-editor-sampling-page.md)」をご覧ください。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
  
