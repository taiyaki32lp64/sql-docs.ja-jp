---
title: マイニング構造列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], columns
- data sources [Analysis Services], mining structure columns
- columns [data mining], mining structure columns
ms.assetid: 20cbf433-70d1-4b61-a462-41a8435b27b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c843a74b831315c98deda9a9d6fb0c3a463bc5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083413"
---
# <a name="mining-structure-columns"></a>マイニング構造列
  マイニング構造を作成するときは、外部データの列を選択し、データをどのようにモデリングに使用するかを指定して、マイニング構造の列を定義します。 したがって、マイニング構造列は、単なるデータ ソースのデータのコピーではなく、マイニング モデルでソースのデータがどのように使用するかを定義するものです。 データの分離方法を決定するプロパティ (データ値の分布を記述するプロパティ) を割り当てることができます。  
  
 マイニング構造列は、柔軟性と拡張性を併せ持つように設計されています。これは、マイニング モデルの作成に使用する各アルゴリズムによって、構造内のさまざまな列を使用してデータが解釈される場合があるためです。 モデルごとに 1 つずつデータ セットを用意する代わりに、1 つのマイニング構造を使用し、そこに含まれる列を使用して各モデルのデータをカスタマイズできます。  
  
## <a name="defining-mining-structure-columns"></a>マイニング構造列の定義  
 構造列を定義する基本データ型およびコンテンツの種類は、構造を作成するために使用するデータ ソースから派生します。 これらの設定はマイニング構造内で変更でき、モデリング フラグの設定や連続した列の分布の設定も行うことができます。  
  
 マイニング構造列の定義には、次の情報を含める必要があります。  
  
-   **[ID]** :通常、名前と同じ列の一意の名前。 マイニング構造の作成後、名前は変更することができますが、ID は変更できません。  
  
-   **[名前]** :名前または列の別名。  
  
-   **コンテンツ**:データが不連続または連続がかどうかを説明する列挙です。  
  
-   **[種類]** :一般的なデータ型を示す列挙体。  
  
-   **配布**:予想される値の分布を表す列挙体。 分布は列が連続している場合に含まれます。  
  
-   **モデリング フラグ**:不足値などの処理方法を示す列挙体。 モデリング フラグはマイニング モデルに対して定義することもできますが、モデル フラグは構造列に使用されるフラグとは異なります。  
  
-   **バインド**:ソース データを指定するプロパティ。  
  
 サードパーティのアルゴリズムには、マイニング構造列で定義できるカスタム プロパティが含まれている場合があります。  
  
 データ マイニング構造とデータ マイニング モデル オブジェクトの詳細については、「 [マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 マイニング構造列を定義および使用する方法の詳細については、次のトピックを参照してください。  
  
|トピック|リンク|  
|-----------|-----------|  
|マイニング構造列の定義に使用できるデータ型について説明します。|[データ型 (データ マイニング)](data-types-data-mining.md)|  
|マイニング構造列に含まれるデータのそれぞれの型に対して使用できるコンテンツの種類について説明します。 コンテンツの種類はデータ型に依存します。 コンテンツの種類はモデル レベルで割り当てられ、モデルで列データを使用する方法を決定します。|[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)|  
|入れ子になったテーブルの概念を紹介し、入れ子になったテーブルをマイニング構造列としてデータ ソースに追加する方法について説明します。|[分類済みの列 (データ マイニング)](classified-columns-data-mining.md)|  
|予想される列の値の分布を指定するためにマイニング構造列に設定できる分布プロパティについて説明します。|[列の分布 (データ マイニング)](column-distributions-data-mining.md)|  
|分離 (*ビン分割*と呼ばれることもあります) の概念について説明し、連続する数値データを分離するために Analysis Services に用意されている方法について説明します。|[分離メソッド (データ マイニング)](discretization-methods-data-mining.md)|  
|マイニング構造列に設定できるモデリング フラグについて説明します。|[モデリング フラグ (データ マイニング)](modeling-flags-data-mining.md)|  
|マイニング構造列どうしを関連付けるために使用できる特殊な列である分類済みの列について説明します。|[分類済みの列 (データ マイニング)](classified-columns-data-mining.md)|  
|マイニング構造列を追加および変更する方法について説明します。|[マイニング構造のタスクと操作方法](mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>参照  
 [マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)   
 [マイニング モデル列](mining-model-columns.md)  
  
  
