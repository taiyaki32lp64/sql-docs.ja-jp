---
title: マイニング モデルのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- Data Mining Designer
- properties [data mining]
ms.assetid: c5194619-8b31-42be-a95f-585711462945
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 030ebd318b310b2c7ca4f85d1f736d168a7adda8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083510"
---
# <a name="mining-model-properties"></a>マイニング モデルのプロパティ
  マイニング モデルには、次の種類のプロパティがあります。  
  
-   モデルによって使用されるデータのデータ型および内容を定義するマイニング構造から継承されたプロパティ。  
  
-   カスタム パラメーターなど、マイニング モデルの作成に使用されるアルゴリズムに関連するプロパティ。  
  
-   モデルのトレーニングに使用するモデルに対するフィルターを定義するプロパティ。  
  
 マイニング モデルのプロパティは、モデルを作成するときに最初に定義されます。ただし、アルゴリズム パラメーター、フィルター、および列の使用法のプロパティなど、ほとんどのプロパティは後で変更できます。 プロパティの変更には、データ マイニング デザイナーの **[マイニング モデル]** タブを使用するか、AMO または XMLA を使用します。  
  
 モデルのいずれかのプロパティを変更した後は、モデルを再処理して、変更内容をモデルに反映させる必要があります。 列の別名や説明の追加など、変更がメタデータのみに関連する場合でも、再処理が必要です。  
  
## <a name="properties-of-models"></a>モデルのプロパティ  
 次の表で、マイニング モデルに固有のプロパティについて説明します。 また、マイニング モデルの個々の列に設定できるプロパティもあります。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**アルゴリズム**|マイニング モデルのアルゴリズムの種類を設定します。|  
|**AlgorithmParameters**|アルゴリズムの各種類で使用可能なアルゴリズム パラメーターの値を設定します。|  
|**[フィルター]**|マイニング モデルのトレーニングとテストに使用するデータに適用するフィルターを設定します。 フィルター定義はモデルと共に格納され、予測クエリの作成時やモデル精度のテスト時に必要に応じて使用できます。<br /><br /> モデルのトレーニング時には、モデルのフィルターは省略できません。|  
|**名前**|マイニング モデルの名前を設定します。|  
|**AllowDrillThrough**|マイニング モデルでドリルスルーを有効にするかどうかを指定します。|  
  
## <a name="properties-of-model-columns"></a>モデル列のプロパティ  
 マイニング モデルの各列に対して、次のデータ マイニング固有のプロパティを設定できます。 これらのプロパティには、マイニング構造内のマイニング モデルごとに異なる値を設定できます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**[説明]**|マイニング列の目的について説明します。|  
|**名前**|マイニング モデル列の名前を設定します。 新しい名前を入力し、マイニング モデル列に別名を指定できます。|  
|**ModelingFlags**|列に対してアルゴリズム固有のフラグを設定します。|  
|**SourceColumnID**|モデル列の基になるマイニング構造列の名前を示します。<br /><br /> このプロパティは読み取り専用です。|  
|**使用方法**|マイニング モデルによる列の使用方法を設定します。|  
  
## <a name="see-also"></a>参照  
 [マイニング モデル列](mining-model-columns.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)   
 [マイニング モデルのプロパティの変更](change-the-properties-of-a-mining-model.md)   
 [データ マイニング ツール](data-mining-tools.md)   
 [リレーショナル マイニング構造の作成](create-a-relational-mining-structure.md)   
 [モデル列の別名の作成](create-an-alias-for-a-model-column.md)  
  
  
