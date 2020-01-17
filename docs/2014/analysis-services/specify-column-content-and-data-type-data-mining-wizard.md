---
title: 指定の列のコンテンツおよびデータ型 (データ マイニング ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d224a321ed78f89a798966bd28c0ff7f16d55134
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068466"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>[列のコンテンツおよびデータ型の指定] (データ マイニング ウィザード)
  **[列のコンテンツおよびデータ型の指定]** ページを使用すると、ウィザードの前のページで選択した各列に対し、使用法とデータ型を指定できます。 列を無視するには、 **[戻る]** をクリックして **[トレーニング データの指定]** ページに戻り、すべてのチェック ボックスをオフにします。  
  
 列の使用法は、モデルにおけるデータの使用方法を表します。 シリーズを特定するキー、分析に使用する入力値、または予測する値として、列を使用できます。 列は、予測と入力の両方に使用できます。  
  
 データ型では、列に格納されるデータの型に関する追加の詳細と、そのデータがトレーニング中にどのように使用されるかを指定します。 コンテンツの種類によっては特定のデータ型が必要とされることも、この逆の場合もあります。 マイニング モデルの作成時に使用するアルゴリズムによっては、特定のデータ型を指定する必要が生じる場合もあります。 マイニング モデルとマイニング構造におけるコンテンツの種類とデータ型については、「[コンテンツの種類 (データ マイニング)](data-mining/content-types-data-mining.md)」を参照してください。  
  
 **詳細情報。** [マイニング構造&#40;Analysis Services - データ マイニング&#41;](data-mining/mining-structures-analysis-services-data-mining.md)、[マイニング モデル列](data-mining/mining-model-columns.md)、[データ マイニング ウィザード&#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)、 [リレーショナル マイニング構造を作成します。](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>および  
 **マイニング モデルの構造**  
 ウィザードの前のページで選択した、ビューおよび入れ子になったテーブルの列を表示します。  
  
 **[列]**  
 列を一覧表示します。  
  
 **コンテンツの種類**  
 列のコンテンツの種類を指定します。 ウィザードの前のページで列をキーとして指定した場合、使用できる値は以下のとおりです。  
  
|オプション|説明|  
|------------|-----------------|  
|キー|ケース シリーズの一意の識別子を列に格納することを指定します。|  
|Key Sequence|シーケンス ID を列に格納することを指定します。|  
|[キー時刻]|日付またはタイム シリーズを識別するための、日付など、一意の連続する数値を列に格納することを指定します。|  
  
 列をキー以外の列として選択した場合、使用できる値は以下のとおりで、データ型に応じて異なります。  
  
|オプション|説明|  
|------------|-----------------|  
|Continuous|連続する数値を列に格納することを指定します。|  
|Discretized|分離された数値か、不連続値として処理可能な数値を列に格納することを指定します。|  
|Discrete|テキストなど数値以外の値を列に格納することを指定します。|  
  
 **データ型**  
 列のデータ型を指定します。  
  
 次の値を指定できます。  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **検出**  
 すべての数値列でデータのサンプルを分析します。 指定した **[コンテンツの種類]** 値を、推奨されるコンテンツの種類に置換します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング ウィザードの F1 ヘルプ&#40;Analysis Services - データ マイニング&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [関連列の提示&#40;データ マイニング ウィザード&#41;](suggest-related-columns-data-mining-wizard.md)   
 [テーブル型を指定&#40;データ マイニング ウィザード&#41;](specify-table-types-data-mining-wizard.md)   
 [列のコンテンツおよびデータ型の指定&#40;データ マイニング ウィザード&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
