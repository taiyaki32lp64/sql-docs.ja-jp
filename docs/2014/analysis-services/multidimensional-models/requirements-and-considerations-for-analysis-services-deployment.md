---
title: 要件と考慮事項の Analysis Services の配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d41f61233bbbcb6c49d4980a3265726280627860
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073171"
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Analysis Services の配置に関する要件と注意点
  あるソリューションのパフォーマンスと可用性は、多くの因子に左右されます。たとえば、基になるハードウェアの機能、サーバーの配置トポロジ、ソリューションの特性 (たとえば、パーティションが複数サーバーに分散されているとか、リレーショナル エンジンへの直接アクセスを必要とする ROLAP ストレージを使用するなど)、サービス レベル契約、データ モデルの複雑さなどです。  
  
## <a name="memory-and-processor-requirements"></a>メモリおよびプロセッサの要件  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、次のような場合、より大きなメモリおよびプロセッサ リソースが必要です。  
  
-   大規模または複雑なキューブを処理する場合。 このようなキューブには、小規模または単純なキューブよりも大きなメモリおよびプロセッサ リソースが必要です。  
  
-   1 つのデータベース内のキューブ数が増加した場合。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の 1 つのインスタンス内のデータベース数が増加した場合。  
  
-   1 つのコンピューター上の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンス数が増加した場合。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] リソースに同時にアクセスするユーザー数が増加した場合。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で使用可能なメモリおよびプロセッサ リソースの量は、SQL Server のエディション、オペレーティング システム、ハードウェアの機能、および仮想プロセッサまたは物理プロセッサのどちらを使用しているかによって異なります。 詳細については、次のリンクをご覧ください。  
  
 [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [SQL Server のエディション別の計算容量制限](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
 [最大容量仕様 &#40;Analysis Services&#41;](olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>必要なディスク領域  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インストールのさまざまな側面とオブジェクト処理に関連するタスクによって、必要なディスクの空き容量が異なります。 次の一覧では、このような要件について説明します。  
  
 キューブ  
 大きなファクト テーブルを持つキューブでは、小さなファクト テーブルを持つキューブよりも大きなディスク空き容量が必要です。 同様に、小さなエクステントでも、多くの大きなディメンションを持つキューブでは、ディメンション メンバーが少ないキューブよりも大きなディスク空き容量が必要です。 通常、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースでは、基になるリレーショナル データベースに保存されている同じデータに必要な空き容量の約 20% が必要です。  
  
 集計  
 集計で必要な追加、集計するために比例した空き容量より多くの集計があるより多くの領域が必要です。 不要な集計を作成しないようにするには、通常、集計に必要な追加の空き容量が、基になるリレーショナル データベースに保存されているデータのサイズの約 10% を超えないようにする必要があります。  
  
 データ マイニング  
 既定では、マイニング構造によって、トレーニングされるデータセットがディスクにキャッシュされます。 このキャッシュされたデータをディスクから削除するには、マイニング構造オブジェクトで **[構造消去の処理]** の処理オプションを使用できます。 詳細については、「[処理の要件および注意事項 (データ マイニング)](../data-mining/processing-requirements-and-considerations-data-mining.md)」を参照してください。  
  
 オブジェクト処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、処理が終了するまで、処理トランザクションで処理中のオブジェクトのコピーがディスクに保存されます。 処理が終了すると、オブジェクトの処理済みのコピーによって元のオブジェクトが置き換えられます。 このため、処理する各オブジェクトの 2 番目のコピー用に十分な空き容量を確保する必要があります。 たとえば、1 つのトランザクションでキューブ全体を処理する場合、キューブ全体の 2 番目のコピーを保存するために十分なハード ディスク容量が必要です。  
  
##  <a name="BKMK_Availability"></a> 可用性に関する注意点  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 環境では、ハードウェアまたはソフトウェアの障害によって、キューブまたはマイニング モデルをクエリに使用できない場合があります。 また、キューブも処理する必要があるので使用できない場合があります。  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>ハードウェアまたはソフトウェアの障害時における可用性の提供  
 ハードウェアやソフトウェアでは、さまざまな理由により障害が発生します。 ただし、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インストールの可用性を維持すると、そのような障害の原因をトラブルシューティングできるだけでなく、障害が発生した場合にユーザーがシステムの使用を続行できるように代替のリソースを提供することもできます。 サーバーのクラスター化と負荷分散は、通常、ハードウェアまたはソフトウェアの障害が発生した場合に可用性の維持に必要な代替のリソースを提供するために使用されます。  
  
 ハードウェアまたはソフトウェアの障害が発生した場合に可用性を維持するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] をフェールオーバー クラスターに配置することを検討してください。 フェールオーバー クラスターでは、なんらかの理由でプライマリ ノードで障害が発生した場合や、プライマリ ノードを再起動する必要がある場合、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のクラスター化によってセカンダリ ノードにフェールオーバーされます。 フェールオーバーは非常に短時間で行われ、その後にユーザーがクエリを実行すると、そのクエリはセカンダリ ノードで実行されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスにアクセスします。 フェールオーバー クラスターの詳細については、次を参照してください。 [Windows Server テクノロジ。フェールオーバー クラスター](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)します。  
  
 可用性の問題に対する別の解決方法としては、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを 2 つ以上の実稼働サーバーに配置することです。 Windows サーバーのネットワーク負荷分散 (NLB) 機能を使用して、実稼働サーバーを 1 つのクラスターに結合できます。 NLB クラスターでは、クラスター内のサーバーがハードウェアまたはソフトウェアの問題が原因で使用できない場合、NLB サービスによって使用可能なサーバーにクエリするように指示されます。  
  
### <a name="providing-availability-while-processing-structural-changes"></a>構造的変更の処理時における可用性の提供  
 キューブに特定の変更を行うと、キューブが処理されるまで使用できなくなることがあります。 たとえば、キューブ内のディメンションに構造的変更を行うと、ディメンションを再処理した場合でも、変更したディメンションを使用する各キューブも処理する必要があります。 このようなキューブを処理しない限り、そのキューブをクエリできません。また、変更したディメンションが含まれているキューブに基づいたマイニング モデルもクエリできません。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの 1 つまたは複数のキューブに影響を与える可能性がある構造的変更を処理しているときに可用性を確保するには、ステージング サーバーを組み込むか、データベースの同期ウィザードを使用することを検討してください。 この機能を使用すると、ステージング サーバー上でデータとメタデータを更新し、実稼働サーバーとステージング サーバーの同期をオンラインで実行できます。 詳細については、「 [Analysis Services データベースの同期](synchronize-analysis-services-databases.md)」を参照してください。  
  
 ソース データの増分更新を簡単に処理するには、プロアクティブ キャッシュを有効にします。 プロアクティブ キャッシュでは、新しいソース データを使用してキューブが更新されます。手動での処理は必要なく、キューブの可用性に影響を与えることもありません。 詳細については、「[プロアクティブ キャッシュ (パーティション)](../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)」をご覧ください。  
  
##  <a name="BKMK_Scalability"></a> スケーラビリティに関する注意点  
 同じコンピューター上に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の複数のインスタンスがあると、パフォーマンスの問題が発生する場合があります。 このような問題を解決する 1 つの方法は、サーバー上のプロセッサ、メモリ、およびディスク リソースを増やすことです。 ただし、複数のコンピューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスをスケーリングすることが必要な場合もあります。  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>複数のコンピューターにおける Analysis Services のスケーリング  
 複数のコンピューターで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインストールをスケーリングするには、いくつかの方法があります。 これらのオプションについては、次の一覧をご覧ください。  
  
-   1 つのコンピューターに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の複数のインスタンスがある場合は、1 つまたは複数のインスタンスを別のコンピューターに移動できます。  
  
-   1 つのコンピューターに複数の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースがある場合は、1 つまたは複数のデータベースを別のコンピューターの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の独自のインスタンスに移動できます。  
  
-   1 つまたは複数のリレーショナル データベースから [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースにデータが提供される場合は、これらのデータベースを別のコンピューターに移動できます。 データベースを移動する前に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースと基になるデータベース間に存在するネットワークの速度と帯域幅を検討してください。 ネットワークが低速であるか混雑している場合、基になるデータベースを別のコンピューターに移動すると、処理のパフォーマンスが低下します。  
  
-   処理クエリのパフォーマンスに影響を与えます削減クエリ負荷のときに処理できない場合は、ステージング サーバーに移行して、処理タスク、実稼働サーバーとステージング サーバーの同期をオンラインを実行することを検討してください。 詳細については、「 [Analysis Services データベースの同期](synchronize-analysis-services-databases.md)」を参照してください。 また、リモート パーティションを使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の複数のインスタンスに処理を分散することもできます。 リモート パーティションの処理では、ローカル コンピューターのリソースではなく、リモート サーバーのプロセッサおよびメモリ リソースを使用します。 リモート パーティションの管理の詳細については、「[リモート パーティションの作成と管理 &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)」を参照してください。  
  
-   クエリのパフォーマンスは低いが、ローカル サーバーのプロセッサおよびメモリ リソースを増やすことができない場合は、2 つ以上の実稼働サーバーに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを配置することを検討してください。 ネットワーク負荷分散 (NLB) を使用して、サーバーを 1 つのクラスターに結合できます。 NLB クラスターでは、クエリは NLB クラスター内のすべてのサーバーに自動的に分散されます。  
  
  
