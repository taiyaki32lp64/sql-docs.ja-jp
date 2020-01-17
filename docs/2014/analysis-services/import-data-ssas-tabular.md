---
title: データのインポート (SSAS 表形式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7eb3fe1157ba40466cc619f504255084aa845fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080616"
---
# <a name="import-data-ssas-tabular"></a>データのインポート (SSAS テーブル)
  テーブル モデルにはさまざまなソースからデータをインポートできます。 このセクションの各トピックでは、データ インポート ウィザードを使用してデータ ソースに接続し、モデル プロジェクトにインポートするデータを選択する方法について説明します。  
  
> [!IMPORTANT]  
>  膨大な数の行を格納するテーブルがモデルに存在する場合、モデルの作成中はデータの一部だけをインポートするようにお勧めします。 データの一部のみをインポートすることによって、処理時間を短縮し、ワークスペース データベースのサーバー リソースの消費を抑えることができます。  
  
 テーブルのインポート ウィザードを使用すると、次のデータ ソースからデータをインポートできます。  
  
|**Data Source**|**[説明]**|  
|---------------------|---------------------|  
|**リレーショナル データベース**|リレーショナル データ ソースには以下が含まれます。<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Microsoft SQL Server 並列データ ウェアハウス<br /><br /> Microsoft Access<br /><br /> [Oracle]<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**多次元ソース**|Microsoft SQL Server Analysis Services キューブ|  
|**データ フィード**|データ フィードには以下が含まれます。<br /><br /> Microsoft Reporting Services レポート<br /><br /> Azure DataMarket データセット<br /><br /> パブリック プロバイダーまたは企業プロバイダーからの atom フィード|  
|**テキスト ファイル**|テキスト ファイルには以下が含まれます。<br /><br /> Excel ファイル (.xls)<br /><br /> テキスト ファイル (.txt)|  
  
 テーブルのインポート ウィザードを使用してのデータのインポートに加え、コピーされたデータ (クリップボードから) をテーブルに貼り付けることもできます。 貼り付けられたデータの動作は、他のデータ ソースからインポートされたデータの動作とは異なります。 テーブル内に貼り付けられたデータには、接続名またはソース データ プロパティはありません。 貼り付けられたデータは、Model.bim ファイルに保存されます。 プロジェクトまたは Model.bim ファイルを保存すると、貼り付けられたデータも保存されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|トピック|説明|  
|-----------|-----------------|  
|[リレーショナル データ ソースからのインポート&#40;SSAS 表形式&#41;](import-from-a-relational-data-source-ssas-tabular.md)|Microsoft SQL Server、Oracle、Teradata データベースなどのリレーショナル データ ソースからデータをインポートする方法について説明します。|  
|[多次元データ ソースからのインポート&#40;SSAS 表形式&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|多次元の SQL Server Analysis Services キューブからデータをインポートする方法について説明します。|  
|[データ フィードからのインポート&#40;SSAS 表形式&#41;](import-from-a-data-feed-ssas-tabular.md)|Microsoft Reporting Services レポートや Azure Data Market データセットなどのデータ フィードからデータをインポートする方法について説明します。|  
|[テキスト ファイルからインポート&#40;SSAS 表形式&#41;](import-from-a-text-file-ssas-tabular.md)|Microsoft Excel ブックやテキスト ファイルからデータをインポートする方法について説明します。|  
|[データのコピーと貼り付け &#40;SSAS テーブル&#41;](copy-and-paste-data-ssas-tabular.md)|モデル デザイナーで [貼り付け] および [貼り付け追加] を使用し既存のテーブルにデータを追加する方法について説明します。|  
  
  
