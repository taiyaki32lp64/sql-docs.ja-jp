---
title: Visio 用データ マイニング図形 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ebe206d4f4942e9a9456ba10b00d33514ef6212
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086397"
---
# <a name="data-mining-shapes-for-visio"></a>Visio 用のデータ マイニング図形
  Visio 用データ マイニング図形は、データ マイニング モデルを表示するためにカスタマイズされたテンプレートです。 これらのテンプレートを使用すると、作成したモデルに接続し、インタラクティブなプレゼンテーションを作成してデータ マイニングの結果を示すことができます。  
  
 テンプレートは静的グラフの多くの利点を提供し、画面のキャプチャ - は、Analysis Services のインスタンスに格納されている、基になるデータ マイニング モデルを操作し、マイニング モデルのパターンの表示方法をカスタマイズすることができます。 ツリー モデルはレベルの折りたたみと展開ができ、データ ノードに対して、または属性別にフィルター処理を実行できるほか、確率や係数などのモデル統計を表示することもできます。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio テンプレートには、以下のウィザードが含まれています:  
  
-   **依存関係ネットワーク ダイアグラム:** このウィザードを使用すると、デシジョン ツリーとニューラル ネットワークのグラフを作成します。  
  
-   **デシジョン ツリー ダイアグラム:** このウィザードを使用すると、意思決定ポイントとデシジョン ツリー モデルに関連付けられている数式を示すダイアグラムを作成します。 このダイアグラムは、回帰モデルでも使用できます。  
  
-   **クラスター ダイアグラム:** このウィザードを使用すると、分割モデルに対応するカラフルなグラフを作成します。 属性の識別、プロファイル、依存関係などのビューを切り替え、クラスターの外観をカスタマイズすることができます。  
  
## <a name="installation"></a>インストール  
 Visio 用データ マイニング テンプレートをインストールするときに既定では、次のファイルにインストールされます\<ドライブ > \Program Files\Microsoft SQL Server 2012 DM Add-ins (または\<ドライブ > \ または Program Files (x86) \Microsoft SQL Server 2012 DMAdd-Ins)。  
  
-   **Microsoft Data Mining.vst**このテンプレートには、デザイン済みの書式設定、レイアウト、およびデータ マイニングの図形を操作するためのウィザードが含まれています。  
  
-   **Microsoft Data Mining Shape Studio.vss**このステンシル ファイルには、テンプレートに関連付けられた図形が含まれています。  
  
## <a name="how-to-use-the-templates"></a>テンプレートの使用方法  
 テンプレートを開くには、図形ファイルをダブルクリックするか、Visio を開いてから図形テンプレートを開きます。  
  
1.  Visio データ マイニング図形をステンシルから新しいページにドロップします。  
  
2.  ウィザードが起動したら、表示するデータ マイニング モデルがあるサーバーに接続します。  
  
3.  データ マイニング モデルを選択して、モデルの種類を視覚化の種類と一致させます。  
  
4.  データの表示オプションと書式設定オプションを設定します。  
  
5.  完了した後、**データ マイニング図形ウィザード**Visio の機能を使用して拡張機能および変更できる図があります。  
  
 操作および Visio のモデル ダイアグラムを強化する方法の詳細については、次を参照してください[を表示するデータ マイニング モデルを Visio で&#40;データ マイニング アドイン。&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>必要条件  
  
-   テンプレートを使用するには、最初に [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスへの接続を作成する必要があります。  
  
     ウィザードに従って、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サーバーを選択し、マイニング モデルが格納されているデータベースを指定します。  
  
     接続を作成する方法については、次を参照してください。[ソース データへの接続&#40;Excel 用データ マイニング クライアント&#41;](connect-to-source-data-data-mining-client-for-excel.md)します。  
  
-   テーブル分析ツールを使用している場合、モデルを保存する確認、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]サーバー、および一時的なモデルを使用しないでください。  
  
-   モデルは、サポートされているアルゴリズム (クラスタリング、デシジョン ツリー、ニューラル ネットワーク、Naïve Bayes、またはロジスティック回帰) を使用して作成されている必要があります。  
  
  
