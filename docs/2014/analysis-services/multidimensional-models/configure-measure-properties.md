---
title: メジャーのプロパティの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b1acd9e33865f1f60c1d1134e3173af4e4a562b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076606"
---
# <a name="configure-measure-properties"></a>メジャーのプロパティの構成
  メジャーには、メジャーの動作を定義し、メジャーがユーザーに表示される方法を制御できるプロパティがあります。  
  
 キューブまたはメジャーを作成または編集する際、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でプロパティを設定できます。 また、MDX または AMO を使用してプログラムで設定することもできます。 詳細については、「[多次元モデル内のメジャーおよびメジャー グループの作成](create-measures-and-measure-groups-in-multidimensional-models.md)」、「[CREATE MEMBER ステートメント &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)」、または「[AMO OLAP 基本オブジェクトのプログラミング](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects)」を参照してください。  
  
## <a name="measure-properties"></a>メジャーのプロパティ  
 プロパティがメジャー レベルでオーバーライドされない限り、メジャーはメンバーになっているメジャー グループから特定のプロパティを継承します。 メジャーのプロパティは、メジャーの集計方法、データ型、表示名、メジャーの表示フォルダー、書式設定文字列、メジャーの式、基になるソース列、およびユーザーに対する表示や非表示を決定します。  
  
|プロパティ|定義|  
|--------------|----------------|  
|`AggregateFunction`|必須。 メジャーの集計方法を決定します。 `Sum` は既定の集計です。 各関数の詳しい説明については、「 [集計関数の使用](use-aggregate-functions.md) 」を参照してください。|  
|`DataType`|必須。 メジャーのバインド先である、基になるファクト テーブル列のデータ型を指定します。 既定では、この値は基になる列から継承されます。|  
|`Description`|メジャーの説明を指定します。クライアント アプリケーションに表示される場合があります。|  
|`DisplayFolder`|ユーザーがキューブに接続するとメジャーが表示されるフォルダーです。 キューブに多くのメジャーがある場合、表示フォルダーを使用すると、メジャーを分類して表示を見やすく改善できます。|  
|`FormatString`|メジャーの `FormatString` プロパティを使用すると、メジャー値の表示に使用する形式を選択できます。<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]に表示形式の一覧が用意されていますが、一覧にはない追加形式を複数指定できます。 Microsoft Visual Basic で有効な名前付き形式またはユーザー定義形式を指定できます。|  
|`ID`|必須。 メジャーの一意識別子 (ID) です。 このプロパティは読み取り専用です。|  
|`MeasureExpression`|メジャーの値を定義する、制約付きの MDX 式を指定します。 式は、集計前にリーフ レベルで評価され、値の重み付けができるようになります。 たとえば、売上高が為替レートで重み付けされる通貨の換算などです。|  
|`Name`|必須。 メジャーの名前を指定します。|  
|`Source`|必須。 メジャーがバインドされるデータ ソース ビューの列を指定します。 詳細については、「[データ ソースとバインド &#40;SSAS 多次元&#41;](data-sources-and-bindings-ssas-multidimensional.md)」を参照してください。|  
|`Visible`|クライアント アプリケーションでメジャーの表示/非表示を決定します。|  
  
## <a name="see-also"></a>参照  
 [メジャー グループのプロパティの構成](configure-measure-group-properties.md)   
 [メジャーの変更](../lesson-3-1-modifying-measures.md)  
  
  
