---
title: データ型 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc810f56d552fa17cb027598a25bde114a696375
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084797"
---
# <a name="data-types-data-mining"></a>データ型 (データ マイニング)
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でマイニング モデルまたはマイニング構造を作成する場合は、マイニング構造のそれぞれの列に対してデータ型を定義する必要があります。 データ マイニング エンジンは、データ型に基づいて、データ ソース内のデータが数値とテキストのどちらであるか、およびデータをどのように処理するかを判断します。 たとえば、ソース データに数値データが含まれる場合、数値を整数として扱うかまたは小数点を使用して扱うかを指定できます。  
  
 各データ型では、1 つまたは複数のコンテンツの種類がサポートされます。 コンテンツの種類を設定することで、マイニング モデルで列のデータをどのように処理または計算するかをカスタマイズできます。  
  
 たとえば、列に数値データが含まれる場合、数値データ型またはテキスト データ型のどちらとしてそのデータを処理するかを選択できます。 数値データ型を選択した場合は、いくつかの異なるコンテンツの種類を設定できます。数値を分離することも、連続値として処理することもできます。 すべてのコンテンツの種類の一覧については、「 [コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」を参照してください。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、では、マイニング構造列に対して次のデータ型がサポートされています。  
  
|データ型|サポートされているコンテンツの種類|  
|---------------|-----------------------------|  
|`Text`|Cyclical、Discrete、Discretized、Key Sequence、Ordered、Sequence|  
|`Long`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> 分類済み|  
|`Boolean`|Cyclical、Discrete、Ordered|  
|`Double`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> 分類済み|  
|`Date`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered|  
  
> [!NOTE]  
>  コンテンツの種類のうち Time および Sequence は、サード パーティのアルゴリズムでのみサポートされています。 コンテンツの種類 Cyclical および Ordered はサポートされますが、多くのアルゴリズムはこれらを不連続の値として扱い、特別な処理は行いません。  
  
## <a name="specifying-a-data-type"></a>データ型の指定  
 データ マイニング拡張機能 (DMX) を使用してマイニング モデルを直接作成する場合は、モデルを定義するときにそれぞれの列のデータ型を定義できます。Analysis Services は、指定されたデータ型を持つ対応するマイニング構造を同時に作成します。 ウィザードを使用してマイニング モデルまたはマイニング構造を作成する場合は、Analysis Services によってデータ型が提案されます。一覧からデータ型を選択することもできます。  
  
## <a name="changing-a-data-type"></a>データ型の変更  
 列のデータ型を変更する場合は、マイニング構造およびその構造に基づくすべてのマイニング モデルを必ず再処理する必要があります。 データ型を変更する場合、特定のモデルでその列を使用できない場合があります。 その場合、Analysis Services は、モデルの再処理時にエラーを発生するか、またはその特定の列を除外してモデルを処理します。  
  
## <a name="see-also"></a>参照  
 [コンテンツの種類 &#40;です。 データ マイニング&#41;](content-types-data-mining.md)   
 [コンテンツの種類 &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [データ型 &#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [マイニング モデル列](mining-model-columns.md)   
 [マイニング構造列](mining-structure-columns.md)  
  
  
