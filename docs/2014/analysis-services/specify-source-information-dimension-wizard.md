---
title: ソース情報 (ディメンション ウィザード) を指定します |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30234275a724dddce95cdad66e5e37a382a25e62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068180"
---
# <a name="specify-source-information-dimension-wizard"></a>[基になる情報の指定] (ディメンション ウィザード)
  **[メイン ディメンション テーブルの選択]** ページを使用すると、作成するディメンションのデータ ソース ビュー、メイン ディメンション テーブル、キー列、およびメンバー名列を選択できます。  
  
 **ディメンション ウィザードを開く**  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の **ソリューション エクスプローラー**で、 **プロジェクトの** [ディメンション] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] フォルダーを右クリックし、 **[新しいディメンション]** をクリックします。  
  
## <a name="options"></a>および  
 **データ ソース ビュー**  
 データ ソース ビューを選択します。  
  
 **メイン テーブル**  
 選択したデータ ソース ビューから、ディメンションのメイン テーブルとして使用するテーブルを選択します。  
  
 **キー列**  
 **[メイン テーブル]** で指定したテーブルから、ディメンションのキー属性に使用するキー列を選択します。  
  
> [!NOTE]  
>  列は 1 つ以上選択できます。 テーブルに複合主キーが含まれている場合は、複合主キーに含まれる列をすべて選択します。 キー列の順序は重要です。  
  
 **[名前] 列**  
 **[メイン テーブル]** で指定したテーブルから、ディメンションのメンバー名を含んでいる列を選択します。 名前列は、複合キーを使用する場合に指定する必要があります。 複合キーの名前列を作成するには、指定されたキー列を連結する名前付き計算をデータ ソース ビューで作成することをお勧めします。 1 つのキーを使用する場合、名前列は省略可能です。  
  
## <a name="see-also"></a>参照  
 [ディメンション ウィザードの F1 ヘルプ](dimension-wizard-f1-help.md)   
 [ディメンション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
