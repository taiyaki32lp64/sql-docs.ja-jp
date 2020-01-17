---
title: 行サンプリング変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowsamplingtrans.f1
- sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql13.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 432c461f90f89eb625e923af342f7c96f323709c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297828"
---
# <a name="row-sampling-transformation"></a>行サンプリング変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  行サンプリング変換を使用すると、入力データセットからランダムに選択されたサブセットを取得できます。 出力サンプルの正確なサイズを指定したり、乱数ジェネレーターのシード値を指定できます。  
  
 ランダム サンプリング用のアプリケーションには、多くの種類があります。 たとえば、ある会社がくじ引きを行って、ランダムに選択された 50 人の社員を当選者とする場合、社員データベースに対して行サンプリング変換を行い、正確な数の当選者を生成できます。  
  
 また、行サンプリング変換は、パッケージの開発中にサイズは小さいが標本化されたデータセットを作成する際に便利です。 十分に標本化されたデータがあれば、パッケージの実行とデータ変換のテストを行うことができます。この場合、完全なデータセットではなくランダム サンプルを使用するため、より迅速にテストできます。 テスト パッケージで使用されるサンプル データセットは常に同じサイズであるため、サンプル サブセットを使用することで、パッケージのパフォーマンスの問題をより簡単に判別することもできます。  
  
 この変換は、比率サンプリング変換と同様です。ただし、比率サンプリング変換は、入力行数の比率を選択してサンプル データセットを作成します。 「 [比率サンプリング変換](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)」をご覧ください。  
  
## <a name="configuring-the-row-sampling-transformation"></a>行サンプリング変換の構成  
 行サンプリング変換は、指定された数の変換入力行を選択してサンプル データセットを作成します。 変換入力からの行の選択はランダムに行われるため、結果サンプルは入力の標本となります。 乱数ジェネレーターで使用するシード値を指定すると、変換による行の選択方法を制御することもできます。  
  
 同じ変換入力で同じランダム シードを使用すると、常に同じサンプル出力が作成されます。 シードを指定しない場合、この変換はオペレーティング システムのティック数を使用して乱数を作成します。 したがって、パッケージの開発およびテスト中に変換結果を確認するためにテスト中は同じシード値を使用し、パッケージの実稼働時にランダム シードへ変更することができます。  
  
 行サンプリング変換には、 **SamplingValue** カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../../integration-services/expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../../integration-services/expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」をご覧ください。  
  
 この変換は、1 つの入力と 2 つの出力をとります。 エラー出力はありません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックを参照してください。  
  
## <a name="row-sampling-transformation-editor-sampling-page"></a>行サンプリング変換エディター ([サンプリング] ページ)
  **[行サンプリング変換エディター]** ダイアログ ボックスを使用すると、指定された行数を使用して、入力の一部をサンプルに分割できます。 この変換は、入力を 2 つの別個の出力に分割します。  
  
### <a name="options"></a>オプション  
 **[行数]**  
 サンプルとして使用する入力における行数を指定します。  
  
 このプロパティの値は、プロパティ式を使用して指定することができます。  
  
 **[サンプル出力名]**  
 サンプリングされた行を含める出力の一意な名前を指定します。 指定した名前は、SSIS デザイナー内に表示されます。  
  
 **[選択されていない出力名]**  
 サンプリングから除外された行を含む出力の一意な名前を指定します。 指定した名前は、SSIS デザイナー内に表示されます。  
  
 **[次のランダム シードを使用する]**  
 変換でサンプルを作成するために使用する乱数ジェネレーターのサンプリング シードを指定します。 このオプションは、開発およびテスト用にのみ使用することをお勧めします。 ランダム シードを指定しなかった場合は、Microsoft Windows のティック数がシードとして使用されます。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  
