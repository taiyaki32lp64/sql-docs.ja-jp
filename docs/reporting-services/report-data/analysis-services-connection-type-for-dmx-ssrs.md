---
title: DMX のための Analysis Services の接続の種類 (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7fb5f444625f6098ba73a82b1cdf94195319ac59
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892508"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>DMX のための Analysis Services の接続の種類 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースを使用してデータセットを作成した場合、レポート デザイナーで有効なキューブが検出されると、多次元式 (MDX) クエリ デザイナーが表示されます。 キューブは検出されなくても、データ マイニング モデルが使用可能な場合、レポート デザイナーではデータ マイニング拡張機能 (DMX) クエリ デザイナーが表示されます。 MDX と DMX デザイナーを切り替えるには、ツール バーの **[コマンドの種類 DMX]** (![DMX クエリ言語ビューに変更](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Change to DMX query language view")) ボタンをクリックします。 DMX クエリ デザイナーを使用すると、グラフィカルな要素を使用して対話的に DMX クエリを作成できます。 DMX クエリ デザイナーを使用するには、指定するデータ ソースが、データを提供するデータ マイニング モデルを既に備えている必要があります。 クエリ結果は、レポートで使用できるようにフラットな行セットに変換されます。  
  
> [!NOTE]  
>  レポートをデザインする前に、モデルのトレーニングを行う必要があります。 詳細については、「 [データ マイニング ソリューション](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)」を参照してください。  
  
## <a name="design-mode"></a>デザイン モード  
 DMX クエリ デザイナーは、デザイン モードで開きます。 デザイン モードには、単一のデータ マイニング モデルと入力テーブルを選択するためのグラフィカルなデザイン画面、および予測クエリを指定するためのグリッドが含まれています。 DMX クエリ デザイナーには、この他に、クエリ モードと結果モードの 2 つのモードがあります。 クエリ モードでは、デザインモードのグリッドがクエリ ペインに置き換えられ、これを使用して DMX クエリを入力することができます。 結果モードでは、クエリによって返された結果セットがデータ グリッドに表示されます。  
  
 DMX クエリ デザイナーのモードを変更するには、クエリのデザイン画面を右クリックし、 **[デザイン]** 、 **[クエリ]** 、または **[結果]** をクリックします。 詳細については、「[Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)」および「[データ マイニング モデル (DMX) からデータを取得する (SSRS)](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)」を参照してください。  
  
## <a name="designing-a-prediction-query"></a>予測クエリのデザイン  
 デザイン モードのクエリ デザイン ペインには、 **[マイニング モデル]** と **[入力テーブルの選択]** の 2 つのウィンドウがあります。 **[マイニング モデル]** ウィンドウでは、クエリで使用するマイニング モデルを選択します。 **[入力テーブルの選択]** ウィンドウでは、予測の基盤とするテーブルを選択します。 入力テーブルではなく、単一クエリを使用する場合は、クエリ デザイン ペインで右クリックし、 **[単一クエリ]** をクリックします。 **[入力テーブルの選択]** ウィンドウは、 **[単一クエリ入力]** ウィンドウに置き換えられます。  
  
 デザイン モードで、 **[マイニング モデル]** ウィンドウおよび **[入力テーブルの選択]** ウィンドウから、グリッド ペインの **[フィールド]** 列にフィールドをドラッグします。 また、残りの列に値を設定することによって、別名を指定したり、結果にフィールドを表示したり、複数のフィールドをグループにまとめたり、演算子を指定して特定の条件または引数でフィールド値を制限したりすることができます。 クエリ モードでは、フィールドをクエリ ペインにドラッグして DMX クエリを作成できます。  
  
## <a name="using-parameters"></a>パラメーターの使用  
 レポート パラメーターを DMX クエリ パラメーターに渡すことができます。 このためには、DMX クエリにパラメーターを追加し、 **[クエリ パラメーター]** ダイアログ ボックスでクエリ パラメーターを定義して、関連付けられたレポート パラメーターを変更します。 クエリ パラメーターを定義するには、ツール バーの **[クエリ パラメーター]** (![[クエリ パラメーター] ダイアログ ボックスのアイコン](../../reporting-services/report-data/media/iconqueryparameter.gif "Icon for the Query Parameters dialog box")) ボタンをクリックします。 DMX クエリでのパラメーターの定義については、「[Analysis Services の MDX クエリ デザイナーでのパラメーターの定義 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)」を参照してください。  
  
 レポート パラメーターとクエリ パラメーターの関係を管理する方法の詳細については、「[クエリ パラメーターのレポート パラメーターへの関連付け (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)」を参照してください。 パラメーターの詳細については、「[レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング ソリューション](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)   
 [クエリ デザイン ツール (SSRS)](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [データ接続、データ ソース、および接続文字列 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
