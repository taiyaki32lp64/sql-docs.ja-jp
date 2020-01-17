---
title: データ マイニング拡張機能 (DMX) ステートメント リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a7a9c18599d13c4db510793a1d75c85bbb7a829
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070862"
---
# <a name="data-mining-extensions-dmx-statements"></a>データ マイニング拡張機能 (DMX) ステートメント
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データ マイニング モデルの操作[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]次の主なタスクが含まれます。  
  
-   マイニング構造とマイニング モデルを作成します。  
  
-   マイニング構造とマイニング モデルの処理  
  
-   マイニング構造またはマイニング モデルの削除あるいはドロップ  
  
-   マイニング モデルのコピー  
  
-   マイニング モデルの参照  
  
-   マイニング モデルに対して予測を行う  
  
 データ マイニング拡張機能 (DMX) ステートメントを使用して、これらの各タスクをプログラムで実行することができます。  
  
 マイニング構造とマイニング モデルを作成します。  
 使用して、 [CREATE MINING STRUCTURE &#40;DMX&#41; ](../dmx/create-mining-structure-dmx.md)をデータベースに新しいマイニング構造を追加するステートメント。 使用することができますし、 [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md)マイニング構造にマイニング モデルを追加するステートメント。  
  
 使用して、 [CREATE MINING MODEL &#40;DMX&#41; ](../dmx/create-mining-model-dmx.md)ステートメントを新しいマイニング モデルと関連付けられているマイニング構造を構築します。  
  
 マイニング構造とマイニング モデルの処理  
 使用して、 [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md)マイニング構造とマイニング モデルを処理するステートメント。  
  
 マイニング構造またはマイニング モデルの削除あるいはドロップ  
 使用して、[削除&#40;DMX&#41; ](../dmx/delete-dmx.md)マイニング モデルまたはマイニング構造からトレーニング済みのすべてのデータを削除するステートメント。 使用して、 [DROP MINING STRUCTURE &#40;DMX&#41; ](../dmx/drop-mining-structure-dmx.md)または[DROP MINING MODEL &#40;DMX&#41; ](../dmx/drop-mining-model-dmx.md)ステートメント、マイニング構造またはマイニング モデルをデータベースから完全に削除します。  
  
 マイニング モデルのコピー  
 使用して、 [SELECT INTO &#40;DMX&#41; ](../dmx/select-into-dmx.md)ステートメントに新しいマイニング モデルを既存のマイニング モデルの構造をコピーして、同じデータで新しいモデルをトレーニングします。  
  
 マイニング モデルの参照  
 使用して、[選択&#40;DMX&#41; ](../dmx/select-dmx.md)データ マイニング アルゴリズムを計算し、モデルのトレーニング中に、データ マイニング モデルに格納される情報を参照するステートメント。 同様に[!INCLUDE[tsql](../includes/tsql-md.md)]、その機能を拡張、SELECT ステートメントをいくつかの句を使用することができます。 これらの句を含める[DISTINCT FROM\<モデル >](../dmx/select-distinct-from-model-dmx.md)、 [FROM\<モデル >。ケース](../dmx/select-from-model-cases-dmx.md)、 [FROM\<モデル >。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)、 [FROM\<モデル >。コンテンツ](../dmx/select-from-model-content-dmx.md)と[FROM\<モデル >。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)します。  
  
 マイニング モデルに対して予測を行う  
 使用して、 [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)既存のマイニング モデルに基づく予測を作成する SELECT ステートメントの句。  
  
 インポートおよびを使用してモデルをエクスポートすることも、[インポート&#40;DMX&#41; ](../dmx/import-dmx.md)と[エクスポート&#40;DMX&#41; ](../dmx/export-dmx.md)ステートメント。  
  
 これらのタスクは、次の表に示す、データ定義ステートメントとデータ操作ステートメントの 2 つのカテゴリに分類されます。  
  
|トピック|説明|  
|-----------|-----------------|  
|[データ マイニング拡張機能 (DMX) データ定義ステートメント](../dmx/dmx-statements-data-definition.md)|データ定義言語 (DDL) の一部です。 新しいマイニング モデルの定義 (学習を含む)、またはデータベースからの既存のマイニング モデルのドロップに使用されます。|  
|[データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)|データ操作言語 (DML) の一部です。 モデルの参照または予測の作成を含む、既存のマイニング モデルでの作業に使用されます。|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
