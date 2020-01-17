---
title: データ マイニング クエリ変換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 44cdff7d7b6813e6fbdf52282621d8845d0643b9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890524"
---
# <a name="data-mining-query-transformation"></a>データ マイニング クエリ変換
  データ マイニング クエリ変換は、データ マイニング モデルに対して予測クエリを実行します。 この変換には、データ マイニング拡張機能 (DMX) クエリを作成するためのクエリ ビルダーが含まれています。 このクエリ ビルダーを使用すると、DMX 言語を使用して、既存のマイニング モデルに対して変換入力データを評価する、カスタム ステートメントを作成できます。 詳細については、「[データ マイニング拡張機能 (DMX) リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)」を参照してください。  
  
 同じデータ マイニング構造で複数のモデルが構築されている場合、1 回の変換で複数の予測クエリを実行することもできます。 詳細については、「[データマイニングクエリインターフェイス](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)」を参照してください。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>データ マイニング クエリ変換の構成  
 データ マイニング クエリ変換は、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] プロジェクト、またはマイニング構造とマイニング モデルを含む [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../../connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[データ マイニング クエリ変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[データ マイニング クエリ変換エディター] ([マイニング モデル] タブ)](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [[データ マイニング クエリ変換エディター] &#40;[マイニング モデル] タブ&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
