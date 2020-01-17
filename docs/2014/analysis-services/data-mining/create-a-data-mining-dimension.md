---
title: データ マイニング ディメンションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], dimensions
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b642d7a0bdf552d8944602761aa76eec1cf35306
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085497"
---
# <a name="create-a-data-mining-dimension"></a>データ マイニング ディメンションの作成
  マイニング構造が OLAP キューブに基づいている場合は、マイニング モデルのコンテンツが含まれているディメンションを作成できます。 作成したディメンションは、ソース キューブに戻すことができます。  
  
 また、ディメンションの参照、ディメンションによるモデルの結果の調査、または MDX によるディメンションに対するクエリを行うこともできます。  
  
### <a name="to-create-a-data-mining-dimension"></a>データ マイニング ディメンションを作成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]のデータ マイニング デザイナーで、 **[マイニング構造]** タブまたは **[マイニング モデル]** タブをクリックします。  
  
2.  **[マイニング モデル]** メニューの **[データ マイニング ディメンションの作成]** をクリックします。  
  
     **[データ マイニング ディメンションの作成]** ダイアログ ボックスが開きます。  
  
3.  **[データ マイニング ディメンションの作成]** ダイアログ ボックスの **[モデル名]** 一覧で、OLAP マイニング モデルを選択します。  
  
4.  **[ディメンション名]** ボックスに、新しいデータ マイニング ディメンションの名前を入力します。  
  
5.  新しいデータ マイニング ディメンションが含まれているキューブを作成するには、 **[キューブを作成する]** を選択します。 **[キューブを作成する]** を選択すると、キューブの新しい名前を入力できるようになります。  
  
6.  **[OK]** をクリックします。  
  
     データ マイニング ディメンションが作成され、ソリューション エクスプローラーの **[ディメンション]** フォルダーに追加されます。 **[キューブを作成する]** を選択した場合は、新しいキューブも作成され、 **[キューブ]** フォルダーに追加されます。  
  
## <a name="see-also"></a>参照  
 [マイニング構造のタスクと操作方法](mining-structure-tasks-and-how-tos.md)  
  
  
