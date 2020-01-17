---
title: Analysis Services プロジェクトの作成 (基本的なデータマイニングチュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a7fcece285a17e158fcdfe77ef00004afe637541
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494028"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>Analysis Services プロジェクトの作成 (基本的なデータ マイニング チュートリアル)
  各 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトは、単一の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベース内のオブジェクトを定義します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースには、さまざまな種類のオブジェクトが含まれています。  
  
-   多次元モデル (キューブ)  
  
-   マイニング構造とマイニング モデル  
  
-   データ ソース、データ ソース ビューとカスタム アセンブリなどのサポート オブジェクト  
  
 データ マイニングを実行するうえで、キューブは **必須ではない** ことに注意してください。 既存のキューブに対してデータ マイニングを実行する必要がある場合は、キューブを作成したときに使用したのと同じプロジェクトに対して、データ マイニング モデルを追加する必要があります。 ただし、キューブが関係していない場合は、ほとんどの目的でデータ ウェアハウスなどのリレーショナル データ ソースに対してモデルを作成することができ、より高いパフォーマンスを達成できます。  
  
 このチュートリアルでは、データ ソースとして、 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]というリレーショナル データ ウェアハウスを使用します。 データ マイニングの目的のみで使用する `BasicDataMining` という名前の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに、すべてのデータ マイニング オブジェクトを配置します。  
  
 既定では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は新しいプロジェクトに対して **localhost** インスタンスを使用します。 名前付きインスタンスまたは別のサーバーを使用している場合は、まずプロジェクトを作成して開き、その後でインスタンス名を変更する必要があります。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]プロジェクトの詳細については、「 [Analysis Services プロジェクトの作成](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md)」を参照してください。  
  
### <a name="to-create-an-analysis-services-project"></a>Analysis Services プロジェクトを作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を開きます。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
3.  **[プロジェクトの種類]** ペインで、 **[ビジネス インテリジェンス プロジェクト]** が選択されていることを確認します。  
  
4.  **[テンプレート]** ペインで、 **[Analysis Services 多次元およびデータ マイニング プロジェクト]** をクリックします。  
  
5.  **[名前]** ボックスに、新しいプロジェクト`BasicDataMining`の名前を指定します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>データ マイニング オブジェクトを格納するインスタンスを変更するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の**プロジェクト**メニューの **プロパティ**です。  
  
2.  **[プロパティ ページ]** ペインの左側にある **[構成プロパティ]** で、 **[配置]** をクリックします。  
  
3.  **[プロパティ ページ]** ペインの右側にある **[対象]** で、 **[サーバー]** の名前が **localhost**になっていることを確認します。 別のインスタンスを使用する場合は、インスタンスの名前を入力します。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [データソース&#40;の作成基本的なデータマイニングチュートリアル&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services プロジェクトのビルド &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/build-analysis-services-projects-ssdt)   
 [Analysis Services プロジェクトの作成 (SSDT)](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt)  
  
  
