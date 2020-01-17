---
title: コンテンツの種類 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], content types
- KEY SEQUENCE column
- content types [data mining]
- attributes [data mining]
- DISCRETIZED column
- CONTINUOUS column
- CYCLICAL column
- ORDERED column
- discretized columns [data mining]
- discrete columns [Analysis Services]
- DISCRETE column
- KEY column
- KEY TIME column
- continuous columns
- coding [Data Mining]
ms.assetid: 2dacd968-70e8-4993-88b6-a6d36024a4e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cf75c9f6fc12ea84d15aebff5c50d11dd0fd924
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085658"
---
# <a name="content-types-data-mining"></a>コンテンツの種類 (データ マイニング)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、マイニング構造の列に対して物理データ型を定義することも、モデルに使用されている列に対して論理的なコンテンツの種類を定義することもできます。  
  
 *データ型* により、マイニング モデルを作成するときにその列に含まれるデータをアルゴリズムでどのように処理するかが決定されます。 列のデータ型を定義することで、列に含まれるデータの型に関する情報と、データの処理方法がアルゴリズムに通知されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の各データ型では、データ マイニング向けに 1 つまたは複数のコンテンツの種類がサポートされます。  
  
 *コンテンツの種類* は、列に含まれるコンテンツの動作を表します。 たとえば、列のコンテンツが特定の間隔 (特定の曜日など) で繰り返される場合は、この列のコンテンツの種類を CYCLICAL として指定できます。  
  
 いくつかのアルゴリズムは、正しく機能するために特定のデータ型と特定のコンテンツの種類が必要です。 たとえば、Microsoft Naive Bayes アルゴリズムでは、連続列を入力として使用したり、連続する値を予測したりすることはできません。 Key Sequence など、一部のコンテンツの種類は、特定のアルゴリズムでのみ使用されます。 アルゴリズムの一覧と、各アルゴリズムがサポートするコンテンツの種類については、「[データ マイニング アルゴリズム (Analysis Services - データ マイニング)](data-mining-algorithms-analysis-services-data-mining.md)」を参照してください。  
  
 次の一覧は、データ マイニングで使用されるコンテンツの種類について説明し、各種類をサポートするデータ型を示しています。  
  
## <a name="discrete"></a>Discrete  
 *Discrete* は、有限の不連続な値が列に格納されることを示します。 たとえば、Gender 列は、データが特定の数のカテゴリを表すという点で、典型的な不連続の属性列です。  
  
 不連続の属性列の値には、値が数値であっても順序の意味は含まれません。 さらに、不連続列に対して使用された値は、数値であっても小数部を計算することはできません。 市外局番コードは、不連続の数値データの好例です。  
  
 コンテンツの種類 `Discrete` は、すべてのデータ マイニング データ型によってサポートされています。  
  
## <a name="continuous"></a>Continuous  
 *Continuous* は、この列に中間値が許可されるスケールの数値データを表す値が格納されることを表します。 有限の数えられるデータを表す不連続列とは異なり、連続列は無限の小数部が含まれる可能性のある計測可能な測定値を表します。 連続した属性列の例としては気温の列があります。  
  
 連続する数値データが列に含まれ、そのデータがどのように分布するかがわかっている場合は、期待される値の分布を指定することで、分析の精度を高めることができます。 列の分布は、マイニング構造レベルで指定します。 このため、設定はその構造に基づくすべてのモデルに適用されます。詳細については、「[列の分布 (データ マイニング)](column-distributions-data-mining.md)」を参照してください。  
  
 コンテンツの種類 `Continuous` は、`Date`、`Double`、および `Long` の各データ型によってサポートされています。  
  
## <a name="discretized"></a>Discretized  
 *分離* とは、連続した一連のデータの値をバケットに分割して、限定された数の可能な値を生成するプロセスです。 数値データだけを分離できます。  
  
 つまり、コンテンツの種類が *discretized* であれば、連続列から派生した値のグループ (またはバケット) を表す値が列に含まれていることを示します。 バケットは、順序付きの不連続の値として処理されます。  
  
 必要なバケットが得られるようにデータを手動で分離することも、SQL Server Analysis Services に用意されている分離メソッドを使用することもできます。 一部のアルゴリズムでは分離が自動的に実行されます。 詳細については、「 [マイニング モデルでの列の分離の変更](change-the-discretization-of-a-column-in-a-mining-model.md)」を参照してください。  
  
 コンテンツの種類 `Discretized` は、`Date`、`Double`、`Long`、および `Text` の各データ型によってサポートされています。  
  
## <a name="key"></a>キー  
 コンテンツの種類 *key* は、この列が行を一意に識別することを表します。 ケース テーブルの場合、通常、キー列は数値またはテキストの識別子です。 コンテンツの種類を `key` に設定すると、分析には使用しない、レコードの追跡専用の列であることが示されます。  
  
 入れ子になったテーブルにもキーはありますが、入れ子になったテーブルのキーは使い方が多少異なります。 入れ子になったテーブルでコンテンツの種類を `key` に設定するのは、その列が分析する属性である場合です。 入れ子になったテーブルのキーの値は各ケースで一意である必要がありますが、ケースのセット全体では重複していてもかまいません。  
  
 たとえば、顧客が購入する製品を分析する場合は、ケース テーブルの **CustomerID** 列のコンテンツの種類を key に設定し、入れ子になったテーブルの **PurchasedProducts** 列のコンテンツの種類も key に設定します。  
  
> [!NOTE]  
>  入れ子になったテーブルを使用できるのは、Analysis Services のデータ ソース ビューとして定義されている外部データ ソースのデータを使用する場合だけです。  
  
 このコンテンツの種類は、`Date`、`Double`、`Long`、および `Text` の各データ型によってサポートされています。  
  
## <a name="key-sequence"></a>Key Sequence  
 コンテンツの種類 *key sequence* は、シーケンス クラスター モデルでのみ使用できます。 コンテンツの種類を `key sequence` に設定すると、一連のイベントを表す値を格納する列であることが示されます。 値は順序付けされていますが、互いに等間隔である必要はありません。  
  
 このコンテンツの種類は、`Double`、`Long`、`Text`、および `Date` の各データ型によってサポートされています。  
  
## <a name="key-time"></a>[キー時刻]  
 コンテンツの種類 *key time* は、時系列モデルでのみ使用できます。 コンテンツの種類を `key time` に設定すると、値が順序付きであり時系列を表す値であることが示されます。  
  
 このコンテンツの種類は、`Double`、`Long`、および `Date` の各データ型によってサポートされています。  
  
## <a name="table"></a>テーブル  
 コンテンツの種類 *table* は、1 つ以上の列と 1 つ以上の行を持つ別のデータ テーブルが列に含まれることを示します。 ケース テーブルの特定の行では、この列に、すべて親ケース レコードに関係する複数の値を含めることができます。 たとえば、メインのケース テーブルに顧客の一覧が含まれている場合に、その顧客が過去に購入した製品の一覧から成る入れ子になったテーブルを含む **ProductsPurchased** 列や、顧客の関心の一覧から成る **Hobbies** 列など、入れ子になったテーブルを含む複数の列を使用できます。  
  
 この列のデータ型は常に `Table` です。  
  
## <a name="cyclical"></a>Cyclical  
 コンテンツの種類 *cyclical* は、循環的な順序付きセットを表す値が列に含まれることを示します。 たとえば、曜日 1 が曜日 7 の後に続くので、番号付きの曜日は循環的な順序付きセットです。  
  
 循環的な列は、コンテンツの種類としては順序付きかつ不連続と見なされます。  
  
 このコンテンツの種類は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のすべてのデータ マイニング データ型によってサポートされています。 ただし、多くのアルゴリズムは cyclical の値を不連続の値として扱い、特別な処理は行いません。  
  
## <a name="ordered"></a>Ordered  
 コンテンツの種類 *Ordered* は、並びまたは順序を定義する値が列に含まれることを示します。 ただし、このコンテンツの種類で順序付けに使用される値は、他の値との距離や大きさの関係を表すわけではありません。 たとえば、順序付き属性列に 1 ～ 5 というランクのスキル レベルに関する情報が含まれている場合、各スキル レベル間の距離に関する情報は示されません。つまり、5 というスキル レベルが 1 というスキル レベルより必ずしも 5 倍優れているわけではありません。  
  
 順序付き属性列は、コンテンツの種類としては不連続と見なされます。  
  
 このコンテンツの種類は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のすべてのデータ マイニング データ型によってサポートされています。 ただし、多くのアルゴリズムは ordered の値を不連続の値として扱い、特別な処理は行いません。  
  
## <a name="classified"></a>分類済み  
 すべてのモデルで共通して使用される上記のコンテンツの種類の他にも、分類済みの列を使用して、一部のデータ型に対してコンテンツの種類を定義できます。 分類済みの列の詳細については、「[分類済みの列 (データ マイニング)](classified-columns-data-mining.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [コンテンツの種類 (DMX)](/sql/dmx/content-types-dmx)   
 [データ型 (データ マイニング)](data-types-data-mining.md)   
 [データ型 &#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [マイニング構造のプロパティの変更](change-the-properties-of-a-mining-structure.md)   
 [マイニング構造列](mining-structure-columns.md)  
  
  
