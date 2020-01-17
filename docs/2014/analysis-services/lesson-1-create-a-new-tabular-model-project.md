---
title: レッスン 1:新しい表形式モデル プロジェクトの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb9ca011cdbbe32ebd6c71cb9ca64967cfbccb9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079305"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>レッスン 1:新しいテーブル モデル プロジェクトの作成
  このレッスンでは、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に新しい空のテーブル モデル プロジェクトを作成します。 新しいプロジェクトが作成されたら、テーブルのインポート ウィザードを使用して、データの追加を開始できます。 新規プロジェクトの作成に加え、このレッスンでは、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] のテーブル モデル作成環境についても概説します。  
  
 テーブル モデル プロジェクトの種類については、「[テーブル モデル プロジェクト (SSAS テーブル)](tabular-models/tabular-model-projects-ssas-tabular.md)」を参照してください。 表形式モデル オーサリング環境についての詳細についてを参照してください。 [Tabular Model Designer &#40;SSAS 表形式&#41;](tabular-model-designer-ssas-tabular.md)します。  
  
 このレッスンを完了するまでに時間を推定するには。**10 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックは、テーブル モデル作成チュートリアルの最初のレッスンです。 このレッスンを完了するには、SQL Server インスタンス上に AdventureWorksDW データベースがインストールされている必要があります。 詳しくは、「[テーブル モデリング (Adventure Works チュートリアル)](tabular-modeling-adventure-works-tutorial.md)」を参照してください。  
  
## <a name="create-a-new-tabular-model-project"></a>新しいテーブル モデル プロジェクトの作成  
  
#### <a name="to-create-a-new-tabular-model-project"></a>新しいテーブル モデル プロジェクトを作成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]の **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
2.  **新しいプロジェクト**ダイアログ ボックスで、**インストールされたテンプレート**、 をクリックして**Business Intelligence**、 をクリックし、 **Analysis Services**とクリックして**Analysis Services 表形式プロジェクト**します。  
  
3.  **名前**、型`AW Internet Sales Tabular Model`、プロジェクト ファイルの場所を指定します。  
  
     既定では、 **[ソリューション名]** はプロジェクト名と同じですが、別のソリューション名を入力することもできます。  
  
4.  **[OK]** をクリックします。  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>SQL Server データ ツールのテーブル モデル作成環境について  
 表形式のモデル作成環境を少し探ってみましょう新しい表形式モデル プロジェクトを作成するので、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 以降)。  
  
 プロジェクトを作成すると、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]が開きます。 モデル デザイナーに空のモデルが表示され、 **[ソリューション エクスプローラー]** ウィンドウで **Model.bim** ファイルが選択されます。 データを追加すると、デザイナーにテーブルと列が表示されます。 (空のウィンドウと Model.bim タブ)、デザイナーが表示されない場合**ソリューション エクスプ ローラー** `AW Internet Sales Tabular Model`、ダブルクリック、 **Model.bim**ファイル。  
  
 プロジェクトの基本プロパティは、 **[プロパティ]** ウィンドウで確認できます。 **ソリューション エクスプ ローラー**、 をクリック`AW Internet Sales Tabular Model`します。 **[プロパティ]** ウィンドウの **[プロジェクト ファイル]** に、 **AW Internet Sales Tabular Model.smproj**と表示されます。 これがプロジェクト ファイル名で、 **[プロジェクト フォルダー]** には、プロジェクト ファイルの場所が表示されます。  
  
 **ソリューション エクスプ ローラー**を右クリックし、`AW Internet Sales Tabular Model`プロジェクトをクリックして**プロパティ**します。 **[AW Internet Sales Tabular Model プロパティ ページ]** ダイアログ ボックスが表示されます。 これらはプロジェクトの詳細なプロパティです。 後で、モデルを配置する準備ができたら、これらのプロパティの一部を設定します。  
  
 ここで、モデルのプロパティを見てみましょう。 **[ソリューション エクスプローラー]** で、 **[Model.bim]** をクリックします。 **[プロパティ]** ウィンドウにモデルのプロパティが表示されます。特に重要なのは、 **DirectQuery Mode** プロパティです。 このプロパティは、モデルがインメモリ モード (オフ) と DirectQuery モード (オン) のどちらで配置されるかを指定します。 このチュートリアルでは、インメモリ モードでモデルを作成し、展開します。  
  
 新しいモデルを作成すると、データ モデリング設定 ([ツール] メニューから開く [オプション] ダイアログ ボックスで指定できます) に応じて、特定のモデル プロパティが自動的に設定されます。 データ バックアップ、ワークスペースの保有期間、およびワークスペース サーバーの各プロパティは、ワークスペース データベース (モデル作成データベース) をバックアップ、メモリ内保持、および構築するための方法と場所を指定します。 これらの設定は後で必要に応じて変更できますが、ここではそのままにしておきます。  
  
 Visual Studio 環境には、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]をインストールした際に、いくつかの新しいメニュー項目が追加されています。 テーブル モデルの作成に固有の新しいメニュー項目を見てみましょう。 **[モデル]** メニューをクリックしてください。 ここから、テーブルのインポート ウィザードを起動したり、既存の接続を編集したり、ワークスペース データを更新したり、"Excel で分析" 機能を使用してモデルを [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel で参照したり、パースペクティブとロールを作成したり、モデル ビューを選択したり、計算オプションを設定したりできます。  
  
 **[テーブル]** メニューをクリックしてください。 ここでは、テーブル間のリレーションシップを作成および管理したり、date テーブル設定を指定したり、パーティションを作成したり、テーブル プロパティを編集したりできます。  
  
 **[列]** メニューをクリックしてください。 ここでは、テーブル内の列を追加および削除したり、列を固定したり、並べ替え順を指定したりできます。 オート SUM 機能を使用して、選択された列に対する標準集計測定を行うこともできます。 その他のツール バー ボタンは、よく使用される機能やコマンドにすばやくアクセスするために用意されています。  
  
 いくつかのダイアログや場所を表示して、テーブル モデルの作成に関連する各種の機能を調べてみてください。 まだアクティブにならない項目もありますが、テーブル モデル作成環境の使用感を確認できます。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 2:データを追加する](lesson-2-add-data.md)します。  
  
  
