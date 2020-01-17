---
title: 以前のバージョンの SQL Server にデータ マイニング ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [Analysis Services]
- holdout [data mining]
- deploy [Analysis Services]
- time series [Analysis Services]
- deploying [Analysis Services - data mining]
- synchronization [Analysis Services]
- deployment [Analysis Services]
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc721d58c69b0275c9846863f761d60db66e5aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084683"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>SQL Server の以前のバージョンへのデータ マイニング ソリューションの配置
  ここでは、 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] のインスタンスで作成されたデータ マイニング モデルまたはデータ マイニング構造を、SQL Server 2005 Analysis Services を使用するデータベースに配置しようとする際、または SQL Server 2005 で作成されたモデルを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスに配置する際に発生する可能性のある、互換性に関する既知の問題について説明します。  
  
 SQL Server 2000 Analysis Services のインスタンスへの配置はサポートされていません。  
  
 [タイム シリーズ モデルの配置](#bkmk_TimeSeries)  
  
 [提示されたパーティションを使用するモデルの配置](#bkmk_Holdout)  
  
 [フィルターを使用するモデルの配置](#bkmk_Filter)  
  
 [データベース バックアップからの復元](#bkmk_Backup)  
  
 [データベースの同期の使用](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> タイム シリーズ モデルの配置  
 Microsoft Time Series アルゴリズムは、SQL Server 2008 で補完的なアルゴリズムの ARIMA が追加され、機能が拡張されています。 タイム シリーズ アルゴリズムの変更に関する詳細については、「 [Microsoft Time Series アルゴリズム](microsoft-time-series-algorithm.md)」を参照してください。  
  
 したがって、新しい ARIMA アルゴリズムを使用するタイム シリーズ マイニング モデルを SQL Server 2005 Analysis Services のインスタンスに配置すると、動作が異なる場合があります。  
  
 ARTXP モデルと ARIMA モデルを組み合わせた予測を制御するパラメーター PREDICTION_SMOOTHING を明示的に設定している場合に、このモデルを SQL Server 2005 のインスタンスに配置すると、パラメーターが無効であるというエラーが Analysis Services で発生します。 このエラーを防ぐには、PREDICTION_SMOOTHING パラメーターを削除し、モデルを純粋な ARTXP モデルに変換する必要があります。  
  
 反対に、SQL Server 2005 Analysis Services を使用して作成されたタイム シリーズ モデルを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスに配置する場合、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でマイニング モデルを開くと、最初に定義ファイルが新しい形式に変換され、既定では、2 つの新しいパラメーターがすべてのタイム シリーズ モデルに追加されます。 パラメーター FORECAST_METHOD が既定値 MIXED で追加され、パラメーター PREDICTION_SMOOTHING が既定値 0.5 で追加されます。 ただし、モデルを再処理するまで、モデルは引き続き ARTXP のみを予測に使用します。 モデルの再処理が終わるとすぐ、予測に ARIMA と ARTXP の両方が使用されます。  
  
 したがって、モデルが変更されないようにするには、モデルを参照するだけにして、決して処理を行わないようにします。 あるいは、FORECAST_METHOD パラメーターまたは PREDICTION_SMOOTHING パラメーターを明示的に設定することもできます。  
  
 混合モデルを設定する方法については、「 [Microsoft Time Series アルゴリズム テクニカル リファレンス](microsoft-time-series-algorithm-technical-reference.md)」を参照してください。  
  
 モデルのデータ ソースに使用されるプロバイダーが SQL Client Data Provider 10 の場合、データ ソース定義も変更して、SQL Server Native Client の前のバージョンを指定する必要があります。 そうしないと、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] で、プロバイダーが登録されていないことを示すエラーが発生します。  
  
##  <a name="bkmk_Holdout"></a> 提示されたパーティションを使用するモデルの配置  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] で、データ マイニング モデルのテストに使用する提示されたパーティションを含むマイニング構造を作成する場合、マイニング構造を SQL Server 2005 インスタンスに配置できますが、パーティションの情報は失われます。  
  
 SQL Server 2005 Analysis Services でマイニング構造を開くと、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] でエラーが発生し、提示されたパーティションを削除するためにそのマイニング構造が再生成されます。  
  
 プロパティ ウィンドウに、提示されたパーティションのサイズを使用可能なで不要になった構造が再構築した後ただし、値\<ddl100_100:HoldoutMaxPercent > 30\</ddl100_100:HoldoutMaxPercent >)、ASSL スクリプト ファイルに存在する可能性があります。  
  
##  <a name="bkmk_Filter"></a> フィルターを使用するモデルの配置  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] で、マイニング モデルにフィルターを適用する場合、モデルを SQL Server 2005 インスタンスに配置できますが、フィルターは適用されません。  
  
 マイニング モデルを開くと、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でエラーが発生し、フィルターを削除するためにモデルが再生成されます。  
  
##  <a name="bkmk_Backup"></a> データベース バックアップからの復元  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で作成されたデータベース バックアップを SQL Server 2005 のインスタンスに復元することはできません。 復元を実行すると、SQL Server Management Studio でエラーが発生します。  
  
 SQL Server 2005 Analysis Services データベースのバックアップを作成して [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンス上に復元する場合、前のセクションで示したようにすべてのタイム シリーズ モデルが変更されます。  
  
##  <a name="bkmk_Synch"></a> データベースの同期の使用  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] から SQL Server 2005 へのデータベースの同期はサポートされていません。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースの同期を試みると、サーバーはエラーを返し、データベースの同期は失敗します。  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services の旧バージョンとの互換性](../analysis-services-backward-compatibility.md)  
  
  
