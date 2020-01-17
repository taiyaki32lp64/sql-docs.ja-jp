---
title: 多次元モデル内のパーティション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00d17af3ce46ee5b20a730e536321140bb69f4ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073328"
---
# <a name="partitions-in-multidimensional-models"></a>多次元モデル内のパーティション
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、 *パーティション* は、メジャー グループに読み込まれるファクト データの物理ストレージを提供します。 各メジャー グループに対して 1 つのパーティションが自動的に作成されますが、さらにデータを分割する追加のパーティションを作成するのが一般的です。そうすることで、処理効率が上がり、クエリ パフォーマンスが向上します。  
  
 処理効率が上がるのは、1 つ以上のサーバーでパーティションを個別に処理することも並列処理することもできるためです。 クエリの実行速度が向上するのは、各パーティションを、結果として応答時間が短縮されるストレージ モードと集計の最適化を使用するように構成できるためです。 たとえば、新しいデータが含まれるパーティションに MOLAP ストレージを選択すると、通常は ROLAP よりも高速になります。 同様に、日付でパーティション分割する場合、新しいデータが含まれるパーティションは、アクセス頻度の低い古いデータが含まれるパーティションよりもさらに最適化されます。 パーティションごとにストレージと集計デザインが異なると、その後のマージ操作に悪影響を及ぼします。 個々のパーティションを最適化する前に、マージがパーティション管理の戦略に必要な要素であるかどうかを必ず検討してください。  
  
> [!NOTE]  
>  Business Intelligence Edition および Enterprise Edition では複数のパーティションがサポートされています。 Standard Edition では、複数のパーティションがサポートされていません。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>パーティション分割方法を設計する際の重要な考慮事項  
 パーティション間でデータが重複しないなど、キューブのデータの整合性はキューブのパーティション間に分散するデータに依存します。 データがパーティションから集約される場合、複数のパーティションに存在するすべてのデータ要素は、それぞれ別のデータ要素として集約されることになります。 この結果、不正確な集約とエラーを生じるデータがエンド ユーザーに提供される可能性があります。 たとえば、製品 X の売上取引がファクト テーブルの 2 つのパーティションで重複している場合、製品 X の売上の集約には、重複する取引の会計が二重に含まれる可能性があります。  
  
 パーティションはマージできます。マージ機能は、すべてのストレージおよびデータ更新手段で使用できます。 パーティションは、ストレージ モードと集計デザインが同じ場合にのみマージできます。 将来マージ可能なパーティションを作成するには、パーティションの作成時に別のパーティションの集計デザインをコピーします。 また、作成したパーティションを編集して、別のパーティションの集計デザインをコピーすることもできます。 マージした後のパーティションでデータが重複すると、キューブのデータの正確性が損なわれるため、パーティションのマージは慎重に行う必要があります。  
  
## <a name="local-partitions"></a>ローカル パーティション  
 ローカル パーティションは、1 つのサーバー上で定義、処理、および保存されるパーティションです。 キューブに大きなメジャー グループがある場合は、処理がパーティション全体で並行して行われるようにパーティション分割します。 並列処理は高速で実行できるのが利点です。 1 つのパーティションの処理ジョブは、別の処理ジョブが開始される前に終了する必要がないので、並行して実行できます。 詳細については、「[ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)」を参照してください。  
  
## <a name="remote-partitions"></a>リモート パーティション  
 リモート パーティションは、1 つのサーバー上で定義されますが、別のサーバーで処理および保存が行われます。 データおよびメタデータのストレージを複数のサーバーに分散するには、リモート パーティションを使用します。 通常、開発から運用に移行すると、分析対象のデータのサイズは数倍に大きくなります。 このように大きなデータがある場合は、そのデータを複数のコンピューターに分散することも 1 つの方法です。 これは、1 つのコンピューターですべてのデータを保持できないためだけでなく、複数のコンピューターでデータを並行して処理する必要があるためです。 詳細については、「 [リモート パーティションの作成と管理 (Analysis Services)](create-and-manage-a-remote-partition-analysis-services.md)」を参照してください。  
  
## <a name="aggregations"></a>集計  
 集計とは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で高速なクエリ応答を実現するために、キューブ データを事前に計算してまとめたものです。 メジャー グループに作成される集計の数は、ストレージに制限を設定するか、パフォーマンスを制限するか、集計の作成プロセスを一定期間実行した後に適宜停止することによって制御できます。 必ずしも集計を増やすことが優れているとは限りません。 新しい集計を作成するたびに、ディスク領域と処理時間に関してコストが発生します。 30% のパフォーマンス向上のために集計を作成した後は、テストまたは経験において必要と判断した場合のみその数を増やすことをお勧めします。詳細については、「[集計のデザイン (Analysis Services - 多次元)](designing-aggregations-analysis-services-multidimensional.md)」を参照してください。  
  
## <a name="partition-merging-and-editing"></a>パーティションのマージと編集  
 2 つのパーティションで同じ集計デザインを使用している場合は、その 2 つのパーティションを 1 つにマージできます。 たとえば、月ごとにパーティション分割された在庫ディメンションがある場合、各月の末日に、その月のパーティションを年度累計のパーティションにマージできます。 この方法では、現在の月のパーティションを短時間で処理および分析できる一方、その年の残りの月はマージ時にのみ再処理する必要があります。 その再処理には時間がかかるため、それほど頻繁に実行しなくてもかまいません。 パーティションのマージ プロセスの管理については、「 [Analysis Services でのパーティションのマージ (SSAS - 多次元)](merge-partitions-in-analysis-services-ssas-multidimensional.md)」を参照してください。 使用してキューブ パーティションを編集する、**パーティション**キューブ デザイナーのタブを参照してください[編集または削除パーティション&#40;Analysis Services - 多次元&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)します。  
  
## <a name="related-topics"></a>関連項目  
  
|トピック|説明|  
|-----------|-----------------|  
|[ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)|データが重複しないようにフィルターまたは異なるファクト テーブルを使用してデータをパーティション分割する方法について説明します。|  
|[パーティション ストレージの設定 (Analysis Services - 多次元)](set-partition-storage-analysis-services-multidimensional.md)|パーティションのストレージの構成方法について説明します。|  
|[編集または削除パーティション&#40;Analysis Services - 多次元&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|パーティションを表示し、編集する方法について説明します。|  
|[Analysis Services でのパーティションのマージ (SSAS - 多次元)](merge-partitions-in-analysis-services-ssas-multidimensional.md)|データが重複しないように異なるファクト テーブルまたはデータ スライスを持つパーティションをマージする方法について説明します。|  
|[パーティションの書き戻しの設定](set-partition-writeback.md)|パーティションへの書き込みを許可する手順について説明します。|  
|[リモート パーティションの作成と管理 (Analysis Services)](create-and-manage-a-remote-partition-analysis-services.md)|リモート パーティションを作成して管理する方法について説明します。|  
  
  
