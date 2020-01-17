---
title: スライスのソース キューブ (データ マイニング ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb156d5c0a3c1332e748878ddebda1772b80696
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068594"
---
# <a name="slice-source-cube-data-mining-wizard"></a>Slice Source Cube (Data Mining Wizard)
  **[ソース キューブのスライス]** ダイアログ ボックスを使用すると、モデルのトレーニング用に使用するデータを制限できます。 通常、キューブには、すべての店舗、すべての地域、すべての製品など、多くの異なるディメンションと属性に関連するデータが含まれています。 属性の無限の組み合わせに対してモデルのトレーニングを実行することは実用的ではないため、このダイアログ ボックスを使用して、モデルのトレーニングで利用する特定のセットを選択します。  
  
 たとえば、AdventureWorks キューブで、特定の製品ライン、地域、または年でスライスを実行し、データの一部を取得することができます。  
  
 スライスおよびキューブについて詳しく理解していない場合は、次の記事を確認することをお勧めします。  
  
-   [パーティションの Slice プロパティを設定&#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [ローカル パーティションの作成と管理 (Analysis Services)](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  動的 MDX 関数 ([Generate (MDX)](/sql/mdx/generate-mdx) または [Except (MDX)](/sql/mdx/except-mdx-function) など) はパーティションの Slice プロパティでサポートされていないことに注意してください。 明示的な組またはメンバー参照を使用して、スライスを定義する必要があります。  
>   
>  使用するのではなく、たとえば、 [:&#40;範囲&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx)範囲を定義するには、特定の年で各メンバーを列挙する必要があるとします。  
>   
>  複雑なスライスを定義する必要がある場合は、XMLA Alter スクリプトを使用して、スライスで組を定義することをお勧めします。 続けて、ascmd コマンド ライン ツールまたは SSIS [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) を使用してスクリプトを実行し、指定したメンバーのセットをパーティション処理の直前に作成します。  
  
 **詳細情報。**[データ マイニング ウィザード&#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)、[リレーショナル マイニング構造の作成](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>および  
 **Dimension**  
 スライスするディメンションを選択します。  
  
 **Hierarchy**  
 スライスする階層を選択します。 任意の階層レベルを選択できますが、モデルで使用される属性は、選択したレベルに存在する属性のみです。  
  
 たとえば、地理階層を選択し、レベルとして国を選択する場合は、属性として市を使用するモデルを構築することはできません。 逆に、スライスする階層レベルとして市を選択すると、国に基づくマイニング モデルを作成することはできません。  
  
 **[演算子]**  
 スライス式の作成に使用する演算子を選択します。  
  
 たとえば、階層として地理を選択した場合は、演算子を選択できます = し、ヨーロッパにのみキューブ データを取得する、フィルターとして「ヨーロッパ」を入力します。  
  
 **[フィルター式]**  
 選択したディメンションでキューブをフィルター処理するときに条件として使用する式を入力します。  
  
 **パラメーター**  
 このオプションは、データ マイニング モデルでは使用されません。  
  
## <a name="see-also"></a>参照  
 [ウィザードの完了&#40;データ マイニング ウィザード&#41;](completing-the-wizard-data-mining-wizard.md)   
 [データ マイニング ウィザードの F1 ヘルプ&#40;Analysis Services - データ マイニング&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [マイニング モデル列の使用法の指定&#40;データ マイニング ウィザード&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
