---
title: レポート サーバー アプリケーションで利用可能なメモリの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- memory [Reporting Services]
- memory thresholds [Reporting Services]
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 80215f23b2544a442600a97112f3d0e2650f55e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103966"
---
# <a name="configure-available-memory-for-report-server-applications"></a>レポート サーバー アプリケーションで利用可能なメモリの構成
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、利用可能なすべてのメモリを使用できますが、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サーバー アプリケーションに割り当てることのできる合計メモリ リソース量に上限を設けることによって、既定の動作をオーバーライドすることができます。 また、しきい値を設定することにより、メモリの圧迫度 (低、中、高) に応じて、要求の優先度付けや処理の方法を変えることもできます。 メモリ圧迫の度合いが低い場合、レポート サーバーは、対話型のレポート処理またはオンデマンドのレポート処理に若干高い優先度を割り当てます。 メモリ圧迫の度合いが高い場合、レポート サーバーは、さまざまな手法を用いながら、利用できる限られたリソースで稼働状態を保ちます。  
  
 このトピックでは、指定できる構成設定について取り上げ、さらに、要求の処理に影響するメモリ不足が発生した場合に、サーバーがどのように対処するかについて説明します。  
  
## <a name="memory-management-policies"></a>メモリ管理ポリシー  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、特定のアプリケーションや処理要求の種類に対して割り当て可能なメモリ量を調整することによってシステム リソースの制約に対処します。 レポート サーバー サービスとして実行され、メモリ管理の対象となるアプリケーションには、次のものがあります。  
  
-   レポート マネージャー (レポート サーバーの Web フロントエンド アプリケーション)  
  
-   レポート サーバー Web サービス (対話型のレポート処理およびオンデマンドの要求用)  
  
-   バックグラウンド処理アプリケーション (定期的なレポート処理、サブスクリプション配信、およびデータベース メンテナンス用)  
  
 メモリ管理ポリシーは、プロセス内の個々のアプリケーションに対してではなく、レポート サーバー サービス全体に対して適用されます。  
  
 システムでメモリ不足が生じていなければ、各サーバー アプリケーションは、要求を受け取る前に、あらかじめ、ある程度のメモリを起動時に確保するため、実際に要求を受け取ったときには最大限のパフォーマンスで動作します。 メモリが不足してくると、レポート サーバーは、次の表に示すように、そのプロセス モデルを調整します。  
  
|メモリ不足|サーバーの対処|  
|---------------------|---------------------|  
|Low|引き続き現在の要求を処理します。 ほとんどの場合、新しい要求が受け付けられます。 バックグラウンド処理アプリケーションに送られる要求には、レポート サーバー Web サービスに送られる要求よりも低い優先度が割り当てられます。|  
|Medium|引き続き現在の要求を処理します。 通常、新しい要求が受け付けられます。 バックグラウンド処理アプリケーションに送られる要求には、レポート サーバー Web サービスに送られる要求よりも低い優先度が割り当てられます。 3 つのサーバー アプリケーションに対して割り当てられるメモリはすべて減らされます。また、Web サービス要求用にできるだけ多くのメモリを確保するため、バックグラウンド処理アプリケーションに割り当てられるメモリは、他のアプリケーションよりも大きく削減されます。|  
|高|メモリ割り当てがさらに削減されます。 多くのメモリを要求するサーバー アプリケーションは拒否されます。 現在の要求はスローダウンされ、完了までにより多くの時間がかかるようになります。 新しい要求は受け付けられません。 レポート サーバーは、メモリ内のデータ ファイルをディスクにスワップします。<br /><br /> メモリ制約が深刻化し、新しい要求を処理できるだけのメモリが存在しない場合、現在の要求が完了するまでの間、レポート サーバーは HTTP 503 (サーバー利用不可) エラーを返します。 場合によっては、メモリ不足を直ちに解消するために、アプリケーション ドメインがリサイクルされることもあります。|  
  
 メモリ不足に対するレポート サーバーの対処をシナリオごとにカスタマイズすることはできませんが、メモリの圧迫度 (高、中、低) に応じた対処を構成設定で指定することはできます。  
  
## <a name="when-to-customize-memory-management-settings"></a>メモリ管理設定をカスタマイズするタイミング  
 メモリ圧迫度を低、中、高という 3 つの範囲に分けたとき、既定の設定では、その範囲が均等にはなっていません。 既定では、低メモリ圧迫度ゾーンの方が、中と高のメモリ圧迫度ゾーンよりも大きくとられています。 これは、処理負荷が均等に分布する場合や一定の割合で増減する場合に最適な構成です。 このシナリオでは、ゾーンからゾーンへの遷移が段階的であるため、レポート サーバーはその対処を余裕を持って調整できます。  
  
 負荷が急激に増加するような場合は、既定の設定を変更する必要があります。 処理負荷の急激な増加が発生した場合、メモリ不足がまったく生じていない状態から、メモリ割り当てエラーの状態へと、きわめて短時間の間に遷移することが考えられます。 たとえば、メモリを激しく消費するレポートの複数のインスタンスが同時に開始されて実行された場合などが該当します。 この種の処理負荷に対処するためには、メモリ消費が中レベルまたは高レベルに達したことをレポート サーバーに認識させ、できるだけ早期に処理をスローダウンさせる必要があります。 こうすることで、より多くの要求を完了させることができます。 そのためには、`MemorySafetyMargin` の値を低く設定して、低メモリ圧迫度ゾーンを他のゾーンよりも小さくする必要があります。 これにより、中～高レベルのメモリ圧迫が発生した場合の対応を早めることができます。  
  
## <a name="configuration-settings-for-memory-management"></a>メモリ管理の構成設定  
 レポート サーバーのメモリ割り当てを制御する構成設定には、`WorkingSetMaximum`、`WorkingSetMinimum`、`MemorySafetyMargin`、および `MemoryThreshold` があります。  
  
-   使用可能なメモリの範囲は、`WorkingSetMaximum` および `WorkingSetMinimum` によって定義されます。 これらを構成することで、レポート サーバー アプリケーションに使用可能なメモリの範囲を設定できます。 たとえば、同じコンピューターで複数のアプリケーションをホストしているとき、レポート サーバーに対し、同じコンピューター上の他のアプリケーションとは異なる割合で、システム リソースを使用させることもできます。  
  
-   `MemorySafetyMargin` および `MemoryThreshold` は、低、中、高の各メモリ圧迫度の境界を設定します。 その各状態について、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、レポート処理やその他の要求が、コンピューターで利用可能なメモリ量に合わせて適切に処理されるように修正措置を行います。 低、中、高の各圧迫度を評価する際の基準を構成設定で指定できます。  
  
     構成設定を変更することはできますが、変更したからといってレポート処理のパフォーマンスが向上するわけではありません。 構成設定の変更によってパフォーマンスが向上するのは、要求が完了前に破棄された場合だけです。 サーバーのパフォーマンスを向上させる最適な方法は、レポート サーバーまたは個々のレポート サーバー アプリケーションを専用のコンピューターに配置することです。  
  
 次の図は、メモリの圧迫度を低、中、高に分ける際に使用される設定の組み合わせを示しています。  
  
 ![メモリの状態の構成設定](../media/rs-memoryconfigurationzones.gif "メモリの状態の構成設定")  
  
 次の表では、`WorkingSetMaximum`、`WorkingSetMinimum`、`MemorySafetyMargin`、`MemoryThreshold` の各設定について説明します。 構成設定は、 [RSReportServer.config ファイル](rsreportserver-config-configuration-file.md)で指定されます。  
  
|要素|説明|  
|-------------|-----------------|  
|`WorkingSetMaximum`|メモリのしきい値を指定します。この値を超えた場合、レポート サーバー アプリケーションに対する、新しいメモリ割り当て要求は許可されません。<br /><br /> 既定では、コンピューターで使用可能なメモリ量が `WorkingSetMaximum` として設定されます。 この値は、サービスの開始時に検出されます。<br /><br /> この設定は、手動で追加しない限り、RSReportServer.config ファイルには存在しません。 レポート サーバーによって使用されるメモリ量を少なくしたい場合は、RSReportServer.config ファイルにこの要素と値を追加します。 有効な値は、0 から整数型の最大値までです。 この値はキロバイト単位で指定します。<br /><br /> `WorkingSetMaximum` の値に達すると、レポート サーバーは新しい要求を受け付けなくなります。 現在実行中の要求は最後まで実行されます。 メモリ使用量が `WorkingSetMaximum` で指定した値を下回った場合のみ、新しい要求が受け付けられます。<br /><br /> `WorkingSetMaximum` 値に達した後、既存の要求によって引き続き追加のメモリが消費された場合、レポート サーバーのすべてのアプリケーション ドメインがリサイクルされます。 詳細については、「 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)」を参照してください。|  
|`WorkingSetMinimum`|リソース消費の下限を指定します。全体的なメモリ使用量がこの値を下回っている場合、レポート サーバーはメモリを解放しません。<br /><br /> 既定では、この値がサービスの開始時に計算されます。 初回メモリ割り当て要求時に `WorkingSetMaximum` の 60% として計算されます。<br /><br /> この設定は、手動で追加しない限り、RSReportServer.config ファイルには存在しません。 この値をカスタマイズするには、RSReportServer.config ファイルに `WorkingSetMinimum` 要素を追加する必要があります。 有効な値は、0 から整数型の最大値までです。 この値はキロバイト単位で指定します。|  
|`MemoryThreshold`|`WorkingSetMaximum` を上限として、メモリ圧迫の度合いを高レベルと中レベルに分けたとき、その境界を定義するパーセンテージを指定します。 レポート サーバーは、メモリの使用状況がこの値に達した場合、要求の処理速度を落とし、別のサーバー アプリケーションに対して割り当てられるメモリ量を変更します。 既定値は 90 です。 この値は、`MemorySafetyMargin` で設定する値より大きくする必要があります。|  
|`MemorySafetyMargin`|`WorkingSetMaximum` を上限として、メモリ圧迫の度合いを中レベルと低レベルに分けたとき、その境界を定義するパーセンテージを指定します。 メモリには、システム用に予約され、レポート サーバーの処理には使用できない領域も存在します。この値は、使用可能なメモリに対するパーセンテージを示します。 既定値は 80 です。|  
  
> [!NOTE]  
>  `MemoryLimit` および `MaximumMemoryLimit` の設定は、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは廃止されています。 既存のインストールをアップグレードした場合、または、該当する設定を含んだ RSReportServer.config ファイルを使用している場合、これらの値は読み取られません。  
  
#### <a name="example-of-memory-configuration-settings"></a>メモリの構成設定の例  
 次の例は、カスタム メモリ構成値を使用したレポート サーバー コンピューターの構成設定を示しています。 `WorkingSetMaximum` または `WorkingSetMinimum` を追加する場合は、その要素と値を RSReportServer.config ファイルに入力する必要があります。 どちらの値も、サーバー アプリケーションに割り当てる RAM のサイズ (キロバイト単位) を整数で指定します。 次の例では、レポート サーバー アプリケーションに対するメモリの合計割当量が 4 GB を超えないように指定しています。 `WorkingSetMinimum` の既定値 (`WorkingSetMaximum` の 60%) を使用する場合は、そちらを省略し、RSReportServer.config ファイルには `WorkingSetMaximum` だけを指定するということでもかまいません。 この例では、実際にどのように追加すればよいかを示すために、`WorkingSetMinimum` を省略せずに記載しています。  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### <a name="about-aspnet-memory-configuration-settings"></a>ASP.NET のメモリの構成設定について  
 レポート サーバー Web サービスとレポート マネージャーは [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] アプリケーションですが、どちらのアプリケーションも、IIS 5.0 互換モードで実行される [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] アプリケーションの machine.config (`processModel` セクション) に指定されているメモリ構成設定は参照しません。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、メモリの構成設定を RSReportServer.config ファイルからのみ読み取ります。  
  
## <a name="see-also"></a>参照  
 [RSReportServer 構成ファイル](rsreportserver-config-configuration-file.md)   
 [RSReportServer 構成ファイル](rsreportserver-config-configuration-file.md)   
 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)  
  
  
