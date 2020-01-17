---
title: データ マイニング (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28b623333adaced772f85572091543f124894f4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084822"
---
# <a name="data-mining-ssas"></a>データ マイニング (SSAS)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、データ マイニングを取り入れたソリューションのための統合プラットフォームを提供します。 リレーショナル データまたはキューブ データを使用して、予測分析を含むビジネス インテリジェンス ソリューションを作成できます。  
  
## <a name="benefits-of-data-mining"></a>データ マイニングの利点  
 データ マイニングでは、詳細な研究に基づいた統計原則を使用してデータ内のパターンを検出します。複雑な問題に関して合理的な意思決定を行う場合に、この情報を役立てることができます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータ マイニング アルゴリズムをデータに適用することにより、傾向の予測、パターンの識別、およびルールや提案の作成を行い、複雑なデータ セット内でイベントの順序を分析し、新しい見識を得ることができます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のデータ マイニングは、強力でありながら使いやすく、分析用やレポート作成用として多くの人に使用されているツールに統合されています。 データ マイニングの使用を開始するために必要な全体像を把握するには、このセクションのリンクを参照してください。  
  
## <a name="key-data-mining-features"></a>データ マイニングの主要機能  
 SQL Server では、統合データ マイニング ソリューションをサポートするために次の機能が提供されています。  
  
-   複数のデータ ソース:データ ウェアハウスやデータ マイニングを実行する OLAP キューブを作成する必要はありません。 外部プロバイダー、スプレッドシート、テキスト ファイルから、表形式のデータを使用できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で作成した OLAP キューブを簡単にマイニングすることもできます。 ただし、インメモリ データベースからのデータは使用できません。  
  
-   統合されたデータのクレンジング、データ管理、および ETL:Data Quality Services には、プロファイルとデータをクレンジングするための高度なツールが用意されています。 Integration Services を使用して、データのクレンジングおよびモデルの構築、処理、トレーニング、および更新のために、ETL プロセスを構築できます。  
  
-   複数のカスタマイズ可能なアルゴリズム:クラスタ リング、ニューラル ネットワーク、デシジョン ツリーなどのアルゴリズムを提供するだけでなく、プラットフォームでは、独自のカスタム プラグイン アルゴリズムの開発をサポートしています。  
  
-   モデル テスト用インフラストラクチャ:モデルをテストおよびデータ セットがクロス検証として重要な統計ツールを使用して、分類マトリックス、リフト チャート、散布図です。 テストおよびトレーニングのセットを容易に作成および管理できます。  
  
-   クエリおよびドリルスルー:予測クエリを作成、モデルのパターンおよび統計情報を取得し、ケース データにドリルスルーします。  
  
-   クライアント ツール:SQL Server によって提供される開発および設計スタジオ、だけでなく、作成、照会、およびモデルの参照を Excel 用データ マイニング アドインを使用できます。 Web サービスなど、カスタムのクライアントを作成することもできます。  
  
-   スクリプト言語のサポートし、マネージ API:すべてのデータ マイニング オブジェクトは、完全にプログラミングできます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]用の MDX 拡張機能、XMLA 拡張機能、または、PowerShell 拡張機能により、スクリプトの作成が可能です。 データ マイニング拡張機能 (DMX) 言語を使用すると、クエリとスクリプト作成を迅速に行うことができます。  
  
-   セキュリティと配置:ロール ベースのセキュリティを提供します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、モデルと構造データへのドリルスルーの個別のアクセス許可を含むです。 他のサーバーへのモデルの配置が容易であるため、ユーザーがパターンにアクセスし、予測を実行することが可能になります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 このセクションのトピックでは、SQL Server データ マイニングの主要機能および関連タスクについて説明します。  
  
-   [データ マイニングの概念](data-mining-concepts.md)  
  
-   [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)  
  
-   [マイニング モデル &#40;Analysis Services - データ マイニング&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)  
  
-   [データ マイニング クエリ](data-mining-queries.md)  
  
-   [データ マイニング ソリューション](data-mining-solutions.md)  
  
-   [データ マイニング ツール](data-mining-tools.md)  
  
-   [データ マイニングのアーキテクチャ](data-mining-architecture.md)  
  
-   [セキュリティの概要 &#40;データ マイニング&#41;](security-overview-data-mining.md)  
  
  
