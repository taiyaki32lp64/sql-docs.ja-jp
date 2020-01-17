---
title: (ディメンション ウィザード) の作成方法の選択 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d44afc5bb4c352a2cb5dfd39030a52db990e3a0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069597"
---
# <a name="select-creation-method-dimension-wizard"></a>[作成方法の選択] (ディメンション ウィザード)
  **[作成方法の選択]** ページを使用すると、ディメンションの作成方法を選択できます。  
  
 **ディメンション ウィザードを開く**  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の **ソリューション エクスプローラー**で、 **プロジェクトの** [ディメンション] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] フォルダーを右クリックし、 **[新しいディメンション]** をクリックします。  
  
## <a name="options"></a>および  
 **既存のテーブルを使用します。**  
 データ ソース内の 1 つ以上のテーブルからディメンションを作成します。 ディメンションに使用できる属性は、テーブル内のデータの構造によって異なります。  
  
 詳細については、「 [Create a Dimension by Using an Existing Table](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)」(既存のテーブルを使用したディメンションの作成) を参照してください。  
  
 **データ ソースに時間テーブルを生成します。**  
 基になるデータ ソースに時間テーブルを作成し、そのテーブルを使用して時間ディメンションを作成します。 こうしたテーブルが存在せず、テーブルの作成にスクリプトを使用しない場合、このオプションを使用します。 新しい時間テーブルには、ウィザードで指定した日付範囲、属性、およびカレンダーのデータが含まれます。  
  
> [!NOTE]  
>  このオプションを使用するには、基になるデータ ソースにオブジェクトを作成する権限が必要です。 データ ソースにオブジェクトを作成する権限がない場合は、代わりに **[サーバーに時間テーブルを生成]** オプションを使用します。  
  
 詳細については、「 [Create a Time Dimension by Generating a Time Table](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)」(時間テーブルを生成して時間ディメンションを作成する) を参照してください。  
  
 **サーバーに時間テーブルを生成します。**  
 サーバーに直接時間テーブルを作成し、そのテーブルを使用して時間ディメンションを作成します。 基になるデータ ソースにオブジェクトを作成する権限がない場合に、このオプションを使用します。 新しい時間ディメンションには、ウィザードで指定した日付範囲、属性、およびカレンダーのデータが含まれます。  
  
 詳細については、「 [Create a Time Dimension by Generating a Time Table](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)」(時間テーブルを生成して時間ディメンションを作成する) を参照してください。  
  
 **データ ソースに時間以外のテーブルを生成します。**  
 基になるリレーショナル データ ソースを使用せずにディメンションをデザインし、データ ソースに必要なスキーマを生成します。 この方法は、トップダウンのモデリングと呼ばれます。  
  
> [!NOTE]  
>  このオプションを使用するには、基になるデータ ソースにオブジェクトを作成する権限が必要です。  
  
 テンプレートを使用するかどうかにかかわらず、ディメンションを構築できます。 テンプレートを使用してディメンションを構築するには、 **[テンプレート]** の一覧からテンプレートを選択します。  
  
 詳細については、「 [Create a Dimension by Generating a Non-Time Table in the Data Source](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)」(データ ソースに時間テーブル以外のテーブルを生成することによるディメンションの作成) を参照してください。  
  
 **テンプレート**  
 ディメンションの作成に使用するテンプレートを選択します。 テンプレートは、特定のビジネス用途向けの属性および階層定義の完全なセットを提供します。  
  
> [!NOTE]  
>  このオプションは、 **[データ ソースに時間テーブル以外のテーブルを生成]** オプションが選択された場合のみ使用できます。  
  
## <a name="see-also"></a>参照  
 [ディメンション ウィザードの F1 ヘルプ](dimension-wizard-f1-help.md)   
 [ディメンション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
