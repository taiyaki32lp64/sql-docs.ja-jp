---
title: データ マイニング ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7dc221f6a81281970a9ad62ba7b16397e40e0648
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084721"
---
# <a name="deployment-of-data-mining-solutions"></a>データ マイニング ソリューションの配置
  データ マイニング プロセスの最後の手順は、実稼働環境へのモデルの配置です。 配置は、モデルをユーザーが使用できるようにし、次のようなタスクを実行できるようになるという点で重要です。  
  
-   モデルを使用して予測を作成し、業務上の意思決定を行います。 クエリを作成に使用できるツールについては、次を参照してください。[データ マイニング クエリ インターフェイス](data-mining-query-tools.md)します。  
  
-   データ マイニング機能をアプリケーションに直接埋め込みます。 マイニング構造とマイニング モデルを作成、変更、処理、および削除するためにアプリケーションで使用できる一連のオブジェクトを含んでいる分析管理オブジェクト (AMO) またはアセンブリを含めることができます。  
  
-   ユーザーが予測の要求、傾向の表示、またはモデルの比較を行うことができるレポートを作成します。  
  
 ここでは、配置オプションについて詳しく説明します。  
  
 [データ マイニング ソリューションの配置の要件](#bkmk_Reqs)  
  
 [リレーショナル ソリューションの配置](#bkmk_RelationalSltn)  
  
 [多次元ソリューションの配置](#bkmk_MDSltn)  
  
 [関連リソース](#bkmk_Resources)  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server の以前のバージョンへのデータ マイニング ソリューションの配置](deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [データ マイニング オブジェクトのエクスポートおよびインポート](export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> データ マイニング ソリューションの配置の要件  
 ソリューションの配置先となる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスは、多次元オブジェクトとデータ マイニング オブジェクトをサポートするモードで実行されている必要があります。つまり、テーブル モデルや PowerPivot データをホストするインスタンスにデータ マイニング オブジェクトを配置することはできません。  
  
 したがって、Visual Studio でデータ マイニング ソリューションを作成するときは、 **[Analysis Services 多次元およびデータ マイニング プロジェクト]** テンプレートを必ず使用してください。  
  
 ソリューションを配置すると、データ マイニングに使用されるオブジェクトが、指定された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに作成されます。作成先は、ソリューション ファイルと同じ名前のデータベースになります。  
  
###  <a name="bkmk_RelationalSltn"></a> リレーショナル ソリューションの配置  
 リレーショナル データ マイニング ソリューションを配置すると、必要なデータ マイニング オブジェクトが新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内に作成され、それらのオブジェクトは既定の設定で処理されます。 処理オプションは、構成プロパティの **[処理オプション]** を使用して変更できます。 詳細については、「[Analysis Services プロジェクトのプロパティの構成 &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)」をご覧ください。  
  
 既定では、増分変更だけが毎回配置されます。 つまり、マイニング モデルを変更すると、プロジェクトを再配置するときに、そのマイニング モデルだけが更新されます。 ただし、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを複数のクライアントが編集する場合は、このためにエラーが発生することがあります。 既定の配置モードを変更して、ソリューションが配置されるときにデータベース全体が更新されるようにするには、 **[配置モード]** プロパティを変更します。  
  
 リレーショナル データ マイニング ソリューションでは、配置しなければならないオブジェクトは、データ ソース定義、使用されたすべてのデータ ソース ビュー、マイニング構造、およびすべての依存マイニング モデルだけです。  
  
###  <a name="bkmk_MDSltn"></a> 多次元ソリューションの配置  
 多次元データ マイニング ソリューションを配置すると、このソリューションによってデータ マイニング オブジェクトがソース キューブと同じデータベース内に作成されます。  
  
 マイニング構造またはマイニング モデルを処理するときには、ソース キューブも処理する必要があります。 このため、OLAP マイニング モデルを使用するソリューションの配置には、リレーショナル データ マイニング ソリューションよりも時間がかかる場合があります。  
  
 通常、データ マイニング オブジェクトも、キューブに使用するのと同じデータ ソースおよびデータ ソース ビューを使用します。 ただし、データ マイニングの対象となるデータ ソースとデータ ソース ビューを明示的に追加することもできます。 たとえば、通常、キューブは見込み顧客についてのデータや、多次元オブジェクトで使用されない外部データを含んでいません。  
  
##  <a name="bkmk_Resources"></a> 関連リソース  
 [データ マイニング オブジェクトの移動](moving-data-mining-objects.md)  
  
 モデルがリレーショナル データのみに基づいている場合、モデルを移動するための最も簡単な方法は、DMX を使用してオブジェクトをエクスポートおよびインポートすることです。  
  
 [Analysis Services データベースの移動](../multidimensional-models/move-an-analysis-services-database.md)  
  
 モデルがデータ ソースとしてキューブを使用している場合、モデルおよびそれをサポートしているキューブ データを移動する方法の詳細については、このトピックを参照してください。  
  
 [Analysis Services プロジェクトの配置 &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの配置についての一般的な情報を提供し、プロジェクト構成の一部として設定できるプロパティについて説明しています。  
  
## <a name="see-also"></a>参照  
 [多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [データ マイニング クエリ インターフェイス](data-mining-query-tools.md)   
 [処理の要件および注意事項 &#40;データ マイニング&#41;](processing-requirements-and-considerations-data-mining.md)  
  
  
