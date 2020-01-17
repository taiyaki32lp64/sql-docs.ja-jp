---
title: SQL Server 2014 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bceabba9b490be6bc2c51b4fdcce9b6b131eb0ce
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74683477"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services は、意思決定支援およびビジネスインテリジェンス (BI) ソリューションで使用される分析データエンジンであり、Excel、Reporting Services レポートなどのビジネスレポートとクライアントアプリケーションの分析データを提供します。サードパーティの BI ツール。 

## <a name="about-sql-server-analysis-services-documentation"></a>SQL Server Analysis Services のドキュメントについて

ドキュメントはバージョン別に分けられます。 現在は SQL Server 2014 Analysis Services ドキュメントにあります。

- SQL Server 2012 以前の詳細については、 [SQL Server 前のバージョンのドキュメント](https://docs.microsoft.com/previous-versions/sql/)を参照してください。
- SQL Server 2014 の詳細については、 [SQL Server 2014 のオンラインブック](../2014-toc/index.yml)を参照してください。
- SQL Server 2016 以降の詳細については、 [MICROSOFT SQL のドキュメント](https://docs.microsoft.com/sql/)を参照してください。
- Azure Analysis Services の詳細については、 [Azure Analysis Services のドキュメント](https://docs.microsoft.com/azure/analysis-services/)を参照してください。

## <a name="analysis-services-workflow"></a>Analysis Services ワークフロー

一般的なワークフローには、OLAP または表形式のデータモデルを構築し、そのモデルをデータベースとしてサーバーインスタンスに配置し、データを読み込むようにデータベースを処理してから、データアクセスを許可する権限を割り当てることがあります。 準備が完了すると、複数の用途を持つこのデータ モデルに、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] をデータ ソースとしてサポートしている任意のクライアント アプリケーションがアクセスできるようになります。  
  
 モデルを作成するには、SQL Server Data Tools を使用します (「 [Analysis Services で使用されるツールとアプリケーション](tools-and-applications-used-in-analysis-services.md)」を参照)。表形式または多次元およびデータマイニングプロジェクトテンプレートのいずれかを選択します。 プロジェクト テンプレートには、モデルで必要とされるすべてのオブジェクトのフォルダーが含まれています。 ウィザードを使用して、データ ソース、データ ソース ビュー、ディメンション、キューブ、ロールなど、すべての基本的な要素を作成することができます。  
  
 モデルは、外部データ システムから取得したデータによって作成されます。通常は外部データ システムとして、SQL Server または Oracle リレーショナル データベース エンジンでホストされているデータ ウェアハウスを使用します (テーブル モデルでは、追加のデータ ソースの種類もサポートされています)。 モデルは、キューブなどのクエリ オブジェクトを指定しますが、複数のキューブ、計算、KPI (ビジネス ロジック、ナビゲーションやドリルスルー動作などの相互作用をカプセル化する) で使用できるディメンションも指定します。  
  
 モデルを使用するには、特定のサーバーモードでデータベースを実行するサーバーインスタンスに配置します。これにより、Excel または他のアプリケーションを介して接続する承認されたユーザーがデータを使用できるようになります。  
  
 インスタンスは、次の3つのサーバーモードのいずれかでインストールできます。  
  
-   テーブル インスタンスとしてインストールし、テーブル モデルを実行します。  
  
-   多次元およびデータ マイニングのインスタンスとしてインストールし、OLAP キューブとデータ マイニング モデルを実行します (既定)。  
  
-   PowerPivot for SharePoint としてインストールし、SharePoint 上で PowerPivot と Excel データ モデルを実行します (PowerPivot for SharePoint は中間層のデータ エンジンであり、SharePoint でホストされているデータ モデルの読み込み、クエリ、更新を実行します)。  
  
 同じデータ エンジンを、3 つの方法で使用できます。 サーバー モードはインストール中に設定され、後で変更できないことに注意してください。 別のモードが必要な場合は、新しいインスタンスをインストールする必要があります。  
  
 Analysis Services に関する基本ドキュメントは、作成するプロジェクトの種類に対応するセクション別に分類されます。 それぞれのモードまたは機能領域の詳細については、次のリンクから選択してください。  
  
 **領域ごとのコンテンツの参照**  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン") [SSAS&#41;&#40;テーブルソリューションと多次元ソリューションの比較](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン") [Analysis Services インスタンス管理](instances/analysis-services-instance-management.md)  
  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")[テーブルモデリング &#40;SSAS 表形式&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")[多次元モデリング &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")[データマイニング &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![小さいファイルフォルダーアイコン](../../2014/integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン") [PowerPivot for SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]機能はエディションによって異なります。 多次元およびデータ マイニング モデルは Standard Edition で使用できますが、上位エディションに比べると機能が少なくなっています。 テーブル モデルと PowerPivot for SharePoint はプレミアム機能であり、Standard Edition のライセンスでは使用できません。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Analysis Services チュートリアル &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [SQL Server 2014 のインストール](../database-engine/install-windows/installation-for-sql-server.md)   
 [開発者ガイド &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server リソースセンター](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
