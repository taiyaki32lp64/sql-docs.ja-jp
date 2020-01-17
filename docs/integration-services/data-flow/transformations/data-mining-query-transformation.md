---
title: データ マイニング クエリ変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e3b6783969376b20921d960e79c8909b5fda4aa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291463"
---
# <a name="data-mining-query-transformation"></a>データ マイニング クエリ変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ マイニング クエリ変換は、データ マイニング モデルに対して予測クエリを実行します。 この変換には、データ マイニング拡張機能 (DMX) クエリを作成するためのクエリ ビルダーが含まれています。 このクエリ ビルダーを使用すると、DMX 言語を使用して、既存のマイニング モデルに対して変換入力データを評価する、カスタム ステートメントを作成できます。 詳細については、「[データ マイニング拡張機能 (DMX) リファレンス](../../../dmx/data-mining-extensions-dmx-reference.md)」を参照してください。  
  
 同じデータ マイニング構造で複数のモデルが構築されている場合、1 回の変換で複数の予測クエリを実行することもできます。 詳細については、「 [データ マイニング クエリ ツール](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)」を参照してください。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>データ マイニング クエリ変換の構成  
 データ マイニング クエリ変換は、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] プロジェクト、またはマイニング構造とマイニング モデルを含む [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../../../integration-services/connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>[データ マイニング クエリ変換エディター] ([マイニング モデル] タブ)
  **[データ マイニング クエリ変換エディター]** ダイアログ ボックスの **[マイニング モデル]** タブを使用すると、データ マイニング構造とそのマイニング モデルを選択できます。  
  
### <a name="options"></a>オプション  
 **接続**  
 リスト ボックスを使用して既存の Analysis Services 接続を選択するか、以下に説明する **[新規作成]** ボタンを使用して新しい接続を作成します。  
  
 **[新規作成]**  
 **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **マイニング構造**  
 使用できるマイニング モデル構造の一覧から選択します。  
  
 **[マイニング モデル]**  
 選択したデータ マイニング構造に関連付けられているマイニング モデルの一覧を表示します。  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>[データ マイニング クエリ変換エディター] ([クエリ] タブ)
  **[データ マイニング クエリ変換エディター]** ダイアログ ボックスの **[クエリ]** タブを使用すると、予測クエリを作成できます。  
  
### <a name="options"></a>オプション  
 **[データ マイニング クエリ]**  
 データ マイニング拡張機能 (DMX) クエリを、テキスト ボックスに直接入力します。  
  
 **[新しいクエリの作成]**  
 **[新しいクエリの作成]** をクリックし、グラフィカルなクエリ ビルダーを使用して、データ マイニング拡張機能 (DMX) クエリを作成します。  
  
