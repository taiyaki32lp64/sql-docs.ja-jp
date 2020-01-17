---
title: データ マイニング モデル トレーニング変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f064ad734e90d2748b959e7fdc9d5868b22c25cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293119"
---
# <a name="data-mining-model-training-destination"></a>データ マイニング モデル トレーニング変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ マイニング モデル トレーニング変換先は、変換先が受け取るデータをデータ マイニング モデル アルゴリズムに渡すことにより、データ マイニング モデルのトレーニングを行います。 複数のデータ マイニング モデルが同じデータ マイニング構造に基づいて構築されている場合は、1 つの変換先を使用してトレーニングできます。 詳細については、「 [マイニング構造列](https://docs.microsoft.com/analysis-services/data-mining/mining-structure-columns) 」と「 [マイニング モデル列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>データ マイニング モデル トレーニング変換先の構成  
 対象になる構造とその構造に基づいて構築されているモデルのケース レベル列で、コンテンツの種類が KEY TIME または KEY SEQUENCE の列がある場合、入力データをその列で並べ替える必要があります。 たとえば、Microsoft Time Series アルゴリズムを使用して構築されたモデルでは、コンテンツの種類に KEY TIME が使用されます。 入力データが並べ替えられていない場合、そのモデルの処理が失敗する場合があります。 データを並べ替える必要がある場合、データ フロー内で事前に並べ替え変換を使用してデータを並べ替えることができます。 コンテンツの種類が KEY である列には、この要件は適用されません。 詳細については、「[コンテンツの種類 (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)」と「[並べ替え変換](../../integration-services/data-flow/transformations/sort-transformation.md)」を参照してください。  
  
> [!NOTE]  
>  データ マイニング モデル トレーニング変換先への入力は、並べ替えられている必要があります。 データを並べ替えるため、データ フロー内のデータ マイニング モデル トレーニング変換先の上流に、並べ替え変換を含めることができます。 詳細については、「 [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md)」を参照してください。  
  
 この変換先は 1 つの入力をとりますが、出力はありません。  
  
 データ マイニング モデル トレーニング変換先を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用します。 詳しくは、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [データ マイニング モデル トレーニング変換先のカスタム プロパティ](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>[データ マイニング モデル トレーニング エディター] ([接続] タブ)
  **[データ マイニング モデル トレーニング エディター]** ダイアログ ボックスの **[接続]** ページを使用すると、トレーニング用のマイニング モデルを選択できます。  
  
### <a name="options"></a>オプション  
 **[ODBC 入力先エディター]**  
 既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続の一覧から選択するか、次に示す手順で [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [新規作成] **ボタンを使用して新しい** 接続を作成します。  
  
 **[新規作成]**  
 **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **マイニング構造**  
 使用できるマイニング構造の一覧から選択するか、 **[新規作成]** をクリックして新しいマイニング構造を作成します。  
  
 **ボタンを使用して新しい**  
 **データ マイニング ウィザード**を使用して、新しいマイニング構造とマイニング モデルを作成します。  
  
 **[マイニング モデル]**  
 選択したマイニング構造に関連付けられているマイニング モデルの一覧を表示します。  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>[データ マイニング モデル トレーニング エディター] ([列] タブ)
  **[データ マイニング モデル トレーニング エディター]** ダイアログ ボックスの **[列]** タブを使用すると、入力列をマイニング構造の列にマップできます。  
  
## <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 入力列をドラッグしてマイニング構造列にマップします。  
  
 **マイニング構造列**  
 マイニング構造列の一覧を表示します。 マイニング構造列をドラッグして使用できる入力列にマップします。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 マッピングを変更または削除するには、 **[使用できる入力列]** ボックスの一覧を使用します。  
  
 **マイニング構造列**  
 マップされているかどうかに関係なく、使用できるマップ先の列を表示します。  
  
