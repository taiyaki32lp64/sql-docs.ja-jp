---
title: '[プロセス] ダイアログ ボックス (Analysis Services - 多次元データ) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32411ff5b715e15fd52b832d8047d8382a603924
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070745"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>[処理] ダイアログ ボックス (Analysis Services - 多次元データ)
  **と** の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] [処理] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ダイアログ ボックスを使用すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトを処理できます。 **で** [処理] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ダイアログ ボックスを表示するには、次の手順に従います。  
  
-   **ソリューション エクスプローラー**で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクト、キューブ、ディメンション、またはマイニング構造を右クリックし、 **[処理]** をクリックします。  
  
-   **キューブ デザイナー** の各ページ、 **ディメンション デザイナー**の各ページ、または **マイニング モデル デザイナー**の **[マイニング構造]** ページおよび **[マイニング モデル]** ページでツール バーの **[処理]** をクリックします。  
  
-   **マイニング モデル デザイナー** の **[マイニング モデル]** ページでマイニング モデルを右クリックし、 **[マイニング構造および全モデルの処理]** または **[モデルの処理]** をクリックします。  
  
 **SQL Server Management Studio** で **[処理]** ダイアログ ボックスを表示するには、次の手順に従います。  
  
-   **オブジェクト エクスプローラー**で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベース、キューブ、メジャー グループ、パーティション、ディメンション、マイニング構造、またはマイニング モデルを右クリックし、 **[処理]** を選択します。  
  
## <a name="options"></a>および  
 **[オブジェクト一覧]**  
 処理する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクト、および適用する処理オプションと設定を選択します。 このグリッドには次の列が含まれています。  
  
 **[オブジェクト名]**  
 処理するオブジェクトの名前を表示します。 名前の左にあるアイコンはオブジェクトの種類を示しています。  
  
 **型**  
 処理するオブジェクトの種類を表示します。  
  
 **[処理オプション]**  
 選択されたオブジェクトに対して実行する処理の種類を選択します。 使用可能な処理オプションの詳細については、次を参照してください。[多次元モデル オブジェクトの処理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)します。  
  
 **[設定]**  
 キューブ、メジャー グループ、またはパーティションの **[処理オプション]** で **[増分処理]** を選択するときに、 **[構成]** ハイパーリンクを表示します。 **[構成]** をクリックし、 **[増分更新]** ダイアログ ボックスを表示します。 **[増分更新]** ダイアログ ボックスの詳細については、[「[増分更新] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](incremental-update-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **[削除]**  
 **[オブジェクト一覧]** から選択された項目を削除します。  
  
 **[影響分析]**  
 **[影響分析]** ダイアログ ボックスを開き、処理タスクによって影響を受けるオブジェクトを表示します。 **[影響分析]** ダイアログ ボックスの詳細については、「[[影響分析] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](impact-analysis-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
> [!NOTE]  
>  **[設定の変更]** ダイアログ ボックスで **[影響を受けたオブジェクトを処理する]** オプションがオンの場合は、このオプションは無効です。  
  
 **[設定の変更]**  
 **[設定の変更]** ダイアログ ボックスを表示し、バッチ処理設定、書き戻し設定、およびディメンション キー エラー設定を含め、選択されたオブジェクトの処理を制御する設定を変更します。 **[設定の変更]** ダイアログ ボックスの詳細については、「[[設定の変更] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](change-settings-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **[実行]**  
 オブジェクトを処理します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [プロセスの進行状況 ダイアログ ボックス&#40;Analysis Services - 多次元データ&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  
