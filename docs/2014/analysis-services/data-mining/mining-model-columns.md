---
title: マイニング モデル列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f99a2dc218543faa4d862fa7520c1618ec307ba7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083704"
---
# <a name="mining-model-columns"></a>マイニング モデル列
  データ マイニング モデルは、マイニング構造によって表されるデータにマイニング モデル アルゴリズムを適用します。 マイニング構造と同様に、マイニング モデルには列が含まれています。 マイニング モデルはマイニング構造内に含まれ、マイニング構造によって定義されるプロパティのすべての値を継承します。 マイニング モデルは、マイニング構造に含まれているすべての列またはその一部を使用することができます。  
  
 マイニング モデル列には、使用法とモデリング フラグという 2 つの追加情報を定義できます。  
  
-   **使用法** は、モデルで列がどのように使用されるかを定義するプロパティです。 列は、入力列、キー列、または予測可能列として使用できます。  
  
-   **モデリング フラグ** では、アルゴリズムがより正確なモデルを作成できるように、ケース テーブルに定義されているデータに関する追加情報をアルゴリズムに提供します。 モデリング フラグは、データ マイニング拡張機能 (DMX) 言語を使用してプログラムで定義するか、または **の** データ マイニング デザイナー [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で定義できます。  
  
 次に、マイニング モデル列で定義できるモデリング フラグを示します。  
  
 `MODEL_EXISTENCE_ONLY`  
 属性の存在が属性列の値よりも重要であることを示します。 たとえば、特定の顧客に関連付けられている発注品目の一覧が含まれたケース テーブルについて考えてみます。 テーブル データには、各発注品目の製品タイプ、ID、およびコストが含まれています。 モデリングには、顧客が特定の発注品目を購入したという事実の方が、発注品目そのもののコストよりも重要な場合があります。 この場合は、コスト列を `MODEL_EXISTENCE_ONLY` として設定します。  
  
 `REGRESSOR`  
 アルゴリズムが、指定した列を回帰アルゴリズムの回帰式に使用できることを示します。 このフラグは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリーと [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムでサポートされています。  
  
 使用法プロパティの設定と、DMX を使用したプログラムによるモデリング フラグの定義について詳しくは、「[CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)」をご覧ください。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] での使用法プロパティの設定およびモデリング フラグの定義について詳しくは、「[データ マイニング オブジェクトの移動](moving-data-mining-objects.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [マイニング モデルのプロパティの変更](change-the-properties-of-a-mining-model.md)   
 [マイニング モデルからの列の除外](exclude-a-column-from-a-mining-model.md)   
 [マイニング構造列](mining-structure-columns.md)  
  
  
