---
title: Analysis Services 処理オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], processing
- OLAP objects [Analysis Services]
ms.assetid: c7e1f66f-16ca-43da-b8c7-4d3e1fa8b58d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9d83baaecbfdba3612acbdcf7a80c9093aac519
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073290"
---
# <a name="processing-analysis-services-objects"></a>Analysis Services オブジェクトの処理
  処理は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの種類 ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース、キューブ、ディメンション、メジャー グループ、パーティション、データ マイニング構造、およびデータ マイニング モデル) に影響します。 オブジェクトごとに、オブジェクトの処理レベルを指定するか、または [既定の処理] オプションを指定して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が自動的に最適な処理レベルを選択するようにできます。 各オブジェクトに適用できる異なるレベルの処理の詳細については、「[処理オプションと設定 &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)」を参照してください。  
  
 処理によって悪影響が発生しないようにするために、処理動作の結果を確認する必要があります。 たとえば、ディメンションを完全に処理すると、そのディメンションに依存するすべてのパーティションが自動的に未処理の状態に設定されます。 これにより、影響を受けるキューブは、依存するパーティションが処理されるまで、クエリに使用できなくなります。  
  
 このトピックのセクションは次のとおりです。  
  
 [データベースの処理](#bkmk_procdb)  
  
 [ディメンションの処理](#bkmk_procdim)  
  
 [キューブの処理](#bkmk_proccube)  
  
 [メジャー グループの処理](#bkmk_procmeasure)  
  
 [パーティションの処理](#bkmk_procpartition)  
  
 [データ マイニング構造とデータ マイニング モデルの処理](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> データベースの処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、データベースにはデータではなく、オブジェクトが含まれています。 データベースを処理するとき、モデルにデータを格納するディメンション、パーティション、マイニング構造、マイニング モデルなどのオブジェクトを再帰的に処理するようサーバーに指示します。  
  
 データベースを処理すると、データベースに含まれているパーティション、ディメンション、およびマイニング モデルの一部またはすべてが処理されます。 実際の処理の種類は、各オブジェクトの状態および選択した処理オプションによって異なります。 詳細については、「[Processing Options and Settings (Analysis Services)](processing-options-and-settings-analysis-services.md)」(処理オプションと設定 (Analysis Services)) を参照してください。  
  
##  <a name="bkmk_proccube"></a> キューブの処理  
 キューブは、メジャー グループおよびパーティションのラッパー オブジェクトと考えることができます。 キューブは、ディメンションと 1 つ以上のメジャーで構成されており、パーティションに保存されます。 ディメンションでは、データをキューブにレイアウトする方法を定義します。 キューブを処理すると、SQL クエリが実行されてファクト テーブルから値が取得され、キューブ内の各メンバーに適切なメジャー値が設定されます。 キューブ内のノード固有のパスとして、値または計算可能値を使用できます。  
  
 キューブを処理すると、キューブ内の未処理のディメンションと、キューブのメジャー グループ内の一部またはすべてのパーティションが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって処理されます。 処理の詳細は、処理を開始したときのオブジェクトの状態および選択した処理オプションによって異なります。 処理オプションの詳細については、「[処理オプションと設定 &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)」を参照してください。  
  
 キューブの処理によって、関連ファクト データを保存する機械処理可能なファイルが作成されます。 集計が作成されている場合は、集計データ ファイルに保存されます。 キューブは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーまたは次のソリューション エクスプローラーから参照できます。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> ディメンションの処理  
 ディメンションを処理すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、ディメンション テーブルに対するクエリが作成および実行され、処理に必要な情報が返されます。  
  
|Country|販売地域|状態|  
|-------------|------------------|-----------|  
|米国|West|California|  
|米国|West|Oregon|  
|米国|West|Washington|  
  
 処理自体は、表形式のデータを、使用可能な階層に変換します。 これらの階層は、メンバー名をすべて連結したもので、内部的には一意の数値パスによって表されます。 次の例は、階層のテキスト表現です。  
  
||  
|-|  
|[United States]|  
|[United States].[West]|  
|[United States].[West].[California]|  
|[United States].[West].[Oregon]|  
|[United States].[West].[Washington]|  
  
 ディメンションの処理では、計算されるメンバーは作成または更新されません。計算されるメンバーはキューブ レベルで定義されます。 計算されるメンバーは、キューブ定義の更新時に影響を受けます。 また、ディメンションの処理では、集計も作成または更新されません。 ただし、ディメンションの処理により、集計が削除される場合があります。 集計は、パーティションの処理中にのみ、作成または更新されます。  
  
 ディメンションを処理する場合は、そのディメンションが複数のキューブで使用されている可能性があるので注意が必要です。 ディメンションを処理すると、それらのキューブには未処理のマークが付き、クエリには使用できなくなります。 ディメンションと関連キューブを同時に処理するには、バッチ処理の設定を使用します。 詳細については、「 [バッチ処理 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_procmeasure"></a> メジャー グループの処理  
 メジャー グループを処理すると、メジャー グループ内の一部またはすべてのパーティションと、メジャー グループに含まれている未処理のディメンションが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって処理されます。 処理ジョブの詳細は、選択した処理オプションによって異なります。 キューブ内の他のメジャー グループに影響を与えずに、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 内の 1 つまたは複数のメジャー グループを処理できます。  
  
> [!NOTE]  
>  個々のメジャー グループは、プログラムによって処理するか、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を使用して処理できます。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]では、個々のメジャー グループを処理できませんが、パーティション単位で処理できます。  
  
##  <a name="bkmk_procpartition"></a> パーティションの処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を効果的に管理するには、データをパーティション分割する必要があります。 パーティションの処理は、ハード ディスクの使用状況および空き領域の制約と、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]によるデータ構造の制約を考慮する必要があるため、独特な処理になります。 クエリの応答時間の速さと処理のスループットの高さを維持するには、定期的にパーティションの作成、処理、およびマージを行う必要があります。 パーティションのマージでは、冗長データの統合を考慮し、このようなデータの管理を行うことが非常に重要になります。 詳細については、「[Analysis Services でのパーティションのマージ &#40;SSAS - 多次元&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)」を参照してください。  
  
 パーティションを処理する場合は、選択した処理オプションに応じて、パーティションとそのパーティションに含まれている未処理のディメンションが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって処理されます。 パーティションの使用による処理上の利点がいくつかあります。 パーティションは、キューブ内の他のパーティションに影響を与えずに処理できます。 パーティションは、セルの書き戻しを必要とするデータの保存に便利です。 書き戻しは、新しいデータをパーティションに書き戻して予測される変更の影響を確認することによって、ユーザーが what-if 分析を実行できる機能です。 書き戻しパーティションは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のセルの書き戻し機能を使用する場合に必要です。 パーティションを並列処理すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって処理能力がより有効に使用され、合計処理時間を大幅に短縮できるので便利です。 パーティションは順番に処理することもできます。  
  
##  <a name="bkmk_procdm"></a> データ マイニング構造とデータ マイニング モデルの処理  
 マイニング構造では、データ マイニング モデルの作成元となるデータ ドメインが定義されます。 1 つのマイニング構造に複数のマイニング モデルを含めることができます。 マイニング構造は、関連付けられたマイニング モデルとは別個に処理できます。 マイニング構造を別個に処理する場合、マイニング構造にはデータ ソースのトレーニング データが設定されます。  
  
 データ マイニング モデルを処理すると、トレーニング データがマイニング モデル アルゴリズムに渡され、そのデータ マイニング アルゴリズムを使用するモデルのトレーニングが行われ、コンテンツが作成されます。 データ マイニング モデル オブジェクトの詳細については、「[マイニング構造 &#40;Analysis Services - データ マイニング&#41;](../data-mining/mining-structures-analysis-services-data-mining.md)」を参照してください。  
  
 マイニング構造とモデルの処理の詳細については、「[処理の要件および注意事項 &#40;Data Mining&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [処理するためのツールと方法 &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [バッチ処理 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [多次元モデル オブジェクトの処理](processing-a-multidimensional-model-analysis-services.md)  
  
  
