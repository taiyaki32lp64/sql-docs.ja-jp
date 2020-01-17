---
title: データ マイニング ツール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tools [Analysis Services]
- mining models [Analysis Services], tools
- data mining [Analysis Services], tools
- data mining [Analysis Services], development
ms.assetid: 003ada6a-0bcd-4f16-8c34-1a9ffc75cd2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd0e6b696e692a9e88edd234d22f41983acbe961
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084827"
---
# <a name="data-mining-tools"></a>データ マイニング ツール
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、データ マイニング ソリューションの作成に使用できる次のツールが用意されています。  
  
-   **では、** データ マイニング ウィザード [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] によって、リレーショナル データ ソースまたはキューブの多次元データを使用して、マイニング構造およびマイニング モデルを簡単に作成できます。  
  
     このウィザードでは、使用するデータを選択してから、クラスタリング、ニューラル ネットワーク、タイム シリーズ モデルなど、特定のデータ マイニング技法を適用します。  
  
-   **と** の両方では、マイニング モデルを作成した後で調べるために [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] モデル ビューアー [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]が提供されます。  各アルゴリズムに合わせて調整されたビューアーを使用してモデルを参照したり、モデル コンテンツ ビューアーを使用して詳しい分析を行ったりすることができます。  
  
-   **と** の両方では、予測クエリを作成するために [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 予測クエリ ビルダー [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] が提供されます。 また、予約データセットまたは外部データに対してモデルの精度をテストしたり、クロス検証を使用してデータセットの品質を調査したりすることもできます。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに配置された既存のデータ マイニング ソリューションを管理するためのインターフェイスです。 構造とモデルを再処理して、データを更新することができます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データのクリーンアップ、タスク (予測の作成やモデルの更新など) の自動化、およびテキスト マイニング ソリューションの作成に使用できるツールが含まれます。  
  
 次のセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータ マイニング ツールの詳細について説明します。  
  
## <a name="data-mining-wizard"></a>では、  
 データ マイニング ウィザードを使用して、データ マイニング ソリューションの作成を開始します。 このウィザードはすぐに簡単に使用でき、データ マイニング構造および初期関連マイニング モデルを順を追って作成する方法が示されます。また、アルゴリズムの種類やデータ ソースの選択と、分析に使用されるケース データの定義も行うことができます。  
  
 **詳細情報。** [データ マイニング ウィザード (Analysis Services - データ マイニング)](data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Data Mining Designer  
 データ マイニング ウィザードを使用してマイニング構造およびマイニング モデルを作成したら、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のデータ マイニング デザイナーを使用して、既存のモデルと構造に対する操作を行うことができます。  
  
 デザイナーには次のタスクのためのツールが含まれます。  
  
-   マイニング構造のプロパティの変更、列の追加、列の別名の作成、ビン分割方法または予想される値分布の変更。  
  
-   既存の構造への新しいモデルの追加。モデルのコピー、モデル プロパティまたはメタデータの変更、またはマイニング モデルへのフィルターの定義。  
  
-   モデル内のパターンとルールの参照。関連付けまたはデシジョン ツリーの調査。 詳細な統計情報の取得。  
  
     データの分析や、データ マイニングで明らかになるパターンの調査のために、各種のモデルに対してカスタム ビューアーが提供されます。  
  
-   リフト チャートの作成またはモデルの利益曲線の分析による、モデルの検証。 分類マトリックスを使用したモデルの比較、またはクロス検証を使用したデータセットとモデルの検証。  
  
-   既存のマイニング モデルに対する予測とコンテンツ クエリの作成。 1 回限りのクエリの作成、または外部データのテーブル全体の予測を生成するクエリの設定。  
  
 **詳細情報。** [データ マイニング デザイナー](data-mining-designer.md)  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 マイニング モデルを作成してサーバーに配置したら、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、データ マイニング オブジェクトをホストする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを管理できます。 また、モデルの調査、新しいデータの処理、予測の作成など、モデルを使用するタスクの実行を続けることもできます。  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] にはクエリ エディターも含まれ、データ マイニング拡張機能 (DMX) クエリの設計と実行や、XMLA を使用するデータ マイニング オブジェクトの操作に使用できます。  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Integration Services のデータ マイニング タスクおよび変換  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、データ マイニングをサポートする多くのコンポーネントが提供されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、一般的なデータ マイニング タスク (予測、モデル作成、処理など) を自動化するためのツールが含まれます。 例 :  
  
-   新しい顧客によってデータセットが更新されるたびに自動的にモデルを更新する、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの作成。  
  
-   ケース レコードのカスタム分割またはカスタム サンプリングの実行。  
  
-   パラメーターで渡されたモデルの自動生成。  
  
 ただし、他のプロセスへの入力として、パッケージ ワークフローのデータ マイニングを使用することもできます。 以下に例を示します。  
  
-   モデルで生成された確率値の使用。テキスト マイニングまたは他の分類タスクのスコアを重み付けします。  
  
-   前のデータに基づく予測の自動生成、およびそれらの値を使用した新しいデータの有効性の調査。  
  
-   新たな顧客をリスク別にセグメント化する、ロジスティック回帰の使用。  
  
 **詳細情報。** [データ マイニング ソリューションの関連プロジェクト](data-mining-solutions.md)  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)   
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)   
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [データ マイニング ソリューション](data-mining-solutions.md)  
  
  
