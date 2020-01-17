---
title: モデル列の別名の作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1df04621d87aa028a2aea43d758fa613dcedccf2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085315"
---
# <a name="create-an-alias-for-a-model-column"></a>モデル列の別名の作成
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、モデル列の別名を作成できます。 この機能は、マイニング構造名が長すぎて扱いにくい場合や、内容またはモデル内での使い方をわかりやすくするために列名を変更する場合に便利です。 たとえば、構造列のコピーを作成して特定のモデル専用に列を分離すると、列名を変更して内容を正確に反映できます。  
  
 モデル列の別名を作成するには、 **[プロパティ]** ペインを使用し、列の [Name](https://docs.microsoft.com/bi-reference/assl/properties/name-element-assl) プロパティを設定します。  
  
 データ マイニング デザイナーの **[マイニング モデル]** タブに、列の使用法のラベルの横にかっこで囲まれて別名が表示されます。  
  
 マイニング モデルのプロパティを設定する方法については、「 [マイニング モデル列](mining-model-columns.md)」を参照してください。  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>マイニング モデル列に別名を追加するには  
  
1.  データ マイニング デザイナーの **[マイニング モデル]** タブで、変更するマイニング列のマイニング モデル内のセルを右クリックし、 **[プロパティ]** を選択します。  
  
2.  画面の右側の **[プロパティ]** ウィンドウで、Name プロパティの横のセルをクリックし、現在の値を削除します。 列の新しい名前を入力します。  
  
## <a name="see-also"></a>関連項目  
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)   
 [マイニング モデルのプロパティ](mining-model-properties.md)  
  
  
