---
title: PowerPivot データ アクセス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f5d2045601f72c3536fbf2d4e469eb5eb20fbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071250"
---
# <a name="powerpivot-data-access"></a>PowerPivot データ アクセス
  このトピックでは、SharePoint ライブラリにパブリッシュされる PowerPivot ブックからデータを取得する方法について説明します。  
  
 PowerPivot データは Excel ブック内に格納されます。 接続文字列は、SharePoint サイト上のブックの URL です。  
  
 PowerPivot データは、そのデータが含まれるブックによってピボットテーブルとピボットグラフのデータとして頻繁に使用されます。 または、PowerPivot データを外部データ ソースとして使用することもできます。その場合は、ブック、ダッシュボード、またはレポートが SharePoint で別の Excel (.xlsx) ファイルに接続してデータを取得し、そのデータを後で使用します。 PowerPivot データをよく使用するクライアント ツールは Excel、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、他の Reporting Services レポート、および PerformancePoint です。  
  
 デスクトップでは、PowerPivot アドインは AMO と ADOMD.NET を使用して、クライアント ワークスペースで PowerPivot データの作成、処理、およびクエリを実行します。  
  
 SharePoint ファームでは、Excel Services はローカル MSOLAP OLE DB プロバイダーを使用して PowerPivot データに接続します。 プロバイダーは、この接続要求をファーム内の PowerPivot for SharePoint サーバーに送信します。 このサーバーがデータをロードし、クエリを実行し、結果セットを返します。  
  
##  <a name="queryproc"></a> SharePoint の PowerPivot データの照会  
 PowerPivot ブックを SharePoint ライブラリから表示すると、ブック内の PowerPivot データがファームにある Analysis Services サーバー インスタンスで個別に検出、抽出、および処理されて、同時に Excel Services によってプレゼンテーション層が描画されます。 完全に処理されたブックは、ブラウザー ウィンドウ、または PowerPivot アドインを持つ Excel 2010 デスクトップ アプリケーションで表示できます。  
  
 次の図は、クエリ処理の要求がファーム内をどのように移動するかを示しています。 PowerPivot データは Excel 2010 ブックの一部なので、クエリ処理の要求は、ユーザーが Excel ブックを SharePoint ライブラリから開いて、PowerPivot データを含むピボットテーブルまたはピボットグラフを操作したときに発生します。  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Excel Services と PowerPivot for SharePoint コンポーネントは、同じブック (.xlsx) ファイルの異なる部分を処理します。 Excel Services は、PowerPivot データを検出して、ファーム内の PowerPivot サーバーから処理を要求します。 PowerPivot サーバーは、コンテンツ ライブラリのブックからデータを抽出して読み込む [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスに要求を割り当てます。 メモリに格納されたデータは描画されたブックにマージされ、ブラウザー ウィンドウに表示するために Excel Web Access に返されます。  
  
 PowerPivot ブックのデータの一部は、PowerPivot for SharePoint によって処理されません。 ワークシートのテーブルおよびセル データは Excel Services によって処理されます。 PowerPivot for SharePoint によって処理されるのは、PowerPivot データに合わないピボットテーブル、ピボットグラフ、およびスライサーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services への接続](../instances/connect-to-analysis-services.md)   
 [テーブル モデル データ アクセス](../tabular-models/tabular-model-data-access.md)  
  
  
