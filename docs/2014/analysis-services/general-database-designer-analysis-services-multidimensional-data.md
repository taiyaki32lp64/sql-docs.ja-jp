---
title: '[全般] (データベース デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf87f2441488810286523a75137a3285aabc1956
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081082"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>[全般] (データベース デザイナー) (Analysis Services - 多次元データ)
  **[全般]** タブを使用して、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースのプロパティを変更します。  
  
 **[全般] タブを表示するには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを右クリックし、 **[データベースの編集]** をクリックして、 **[全般]** タブをクリックします。  
  
## <a name="basic-options"></a>[基本] オプション  
 **[基本]** セクションを拡張して、データベースに関する基本情報を変更します。 ここでは、次のオプションについて説明します。  
  
 **データベース名**  
 データベースの名前が表示されます。  
  
> [!NOTE]  
>  データベースの名前を変更するには、 **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[プロパティ]** をクリックします。 データベースの **[プロパティ ページ]** ダイアログ ボックスの **[配置]** ページで、 **[データベース]** プロパティの値を新しいデータベース名に変更します。  
  
 **[説明]**  
 データベースの説明を入力します。  
  
## <a name="translations-options"></a>[翻訳] オプション  
 **[翻訳]** セクションを拡張して、データベースのキャプションと説明の翻訳を作成、変更します。 ここでは、次の列を持つグリッドについて説明します。  
  
 **言語**  
 指定したトランザクションの言語を選択します。  
  
 新しい翻訳をグリッドに追加するには、クリックして **\<新しい翻訳の追加 >** します。  
  
 **キャプションの翻訳**  
 データベースのキャプションを適切な翻訳言語で入力します。 空白の場合は、データベースの既定のキャプションが使用されます。  
  
 **説明の翻訳**  
 データベースの説明を適切な翻訳言語で入力します。 空白の場合は、データベースの既定の説明が使用されます。  
  
## <a name="account-type-mapping-options"></a>[勘定科目の種類のマッピング] オプション  
 **[勘定科目の種類のマッピング]** セクションを拡張して、選択されたデータベースで各勘定科目の **種類** に関連付けられた既定の集計関数を変更します。  
  
> [!NOTE]  
>  このオプションは、1 つまたは複数のメジャーが *ByAccount* 集計関数を使用するキューブに対してのみ適用可能です。  
  
 ここでは、次の列を持つグリッドについて説明します。  
  
 **名前**  
 勘定科目の種類の名前を入力します。  
  
 新しいアカウントの種類を追加するには、クリックして **\<新しいアカウントの種類の追加 >** します。  
  
 **[エイリアス]**  
 ビジネス インテリジェンス ウィザードで使用するための、勘定科目の種類の既定名を設定します。 この列を空にすると、 **[名前]** 列での既定の設定が使用されます。  
  
 **集計関数**  
 選択された勘定科目の種類に使用される集計関数を選択します。  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多次元モデル データベース&#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [警告&#40;データベース デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  
