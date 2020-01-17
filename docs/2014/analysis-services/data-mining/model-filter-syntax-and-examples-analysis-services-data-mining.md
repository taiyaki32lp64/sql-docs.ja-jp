---
title: モデル フィルターの構文と例 (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e8fea8d2a7b92ccca9b139b62d429fafe3a9bc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083364"
---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>モデル フィルターの構文と例 (Analysis Services - データ マイニング)
  ここでは、モデル フィルターの構文について詳しく説明し、サンプル式を示します。  
  
 
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 一般に、フィルター式は WHERE 句の内容に相当します。 `AND`、`OR`、および `NOT` の論理演算子を使用すると、複数の条件を結合できます。  
  
 入れ子になったテーブルでは、`EXISTS` 演算子と `NOT EXISTS` 演算子も使用できます。 サブクエリから少なくとも 1 行が返される場合、`EXISTS` 条件が `true` と評価されます。 これは、入れ子になったテーブルに特定の値があるケース (ある品目を少なくとも 1 回購入した顧客など) のみをモデルで使用する場合に役立ちます。  
  
 サブクエリに指定した条件が存在しない場合、`NOT EXISTS` 条件が `true` と評価されます。 特定の品目を購入したことがない顧客のみをモデルで使用する場合などに役立ちます。  
  
 一般的な構文は次のとおりです。  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *フィルター (filter)*  
 論理演算子で結合された 1 つ以上の述語が含まれます。  
  
 *predicate list*  
 論理演算子で区切られた 1 つ以上の有効なフィルター式です。  
  
 *columnName*  
 マイニング構造列の名前です。  
  
 logical operator  
 `AND`、 `OR`、 `NOT`  
  
 *avPredicate*  
 スカラー マイニング構造列にのみ適用できるフィルター式です。 *avPredicate* 式は、モデル フィルターと入れ子になったテーブルのフィルターの両方で使用できます。  
  
 次のいずれかの演算子を使用する式は、連続列にのみ適用できます。 :  
  
-   **\<** (より小さい)  
  
-   **>** (より大きい)  
  
-   **>=** (以上)  
  
-   **\<=** (以下)  
  
> [!NOTE]  
>  データ型にかかわらず、`Discrete`、`Discretized`、または `Key` の型の列にこれらの演算子を適用することはできません。  
  
 次のいずれかの演算子を使用する式は、連続列、不連続列、離散化列、またはキー列に適用できます。  
  
-   **=** (等しい)  
  
-   **!=** (等しくない)  
  
-   **IS NULL**  
  
 *avPredicate*を離散化列に適用する場合、フィルターに使用される値は、特定のバケット内の任意の値です。  
  
 つまり、 `AgeDisc = '25-35'`などの条件を定義する代わりに、その範囲の値を計算して使用します。  
  
 たとえば  `AgeDisc = 27`  は、27 と同じ範囲 (ここでは 25 ～ 35) 内の任意の値を意味します。  
  
 *nestedTablePredicate*  
 入れ子になったテーブルに適用するフィルター式です。 モデル フィルターでのみ使用できます。  
  
 *nestedTablePredicate*のサブクエリの引数は、テーブルのマイニング構造列にのみ適用できます。  
  
 サブクエリ  
 SELECT ステートメントの後に有効な述語または述語の一覧を指定します。  
  
 すべての述語が *avPredicates*で示される型である必要があります。 また、述語で、 *columnName*引数を指定して参照できるのは、現在の入れ子になったテーブルに含まれている列だけです。  
  
### <a name="limitations-on-filter-syntax"></a>フィルター構文に関する制限事項  
 フィルターには次の制限が適用されます。  
  
-   フィルターに指定できるのは、単純な述語だけです。 これらには、算術演算子、スカラー、および列名が含まれます。  
  
-   フィルター構文では、ユーザー定義関数がサポートされていません。  
  
-   フィルター構文では、ブール型以外の演算子 (プラス記号やマイナス記号など) がサポートされていません。  
  
## <a name="examples-of-filters"></a>フィルターの例  
 次の例は、マイニング モデルに適用するフィルターの使用方法を示しています。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を使用してフィルター式を作成する場合、 **[プロパティ]** ウィンドウや、フィルターのダイアログ ボックスの **[式]** ペインには、WITH FILTER キーワードより後の文字列だけが表示されます。 ここでは、列の型と使用法をわかりやすくするため、マイニング構造の定義も示します。  
  
###  <a name="bkmk_Ex1"></a> 例 1: 一般的なケースレベルのフィルター処理  
 次の例は、モデルに使用するケースを、職業が Architect で 31 歳以上の顧客だけに制限するための、単純なフィルターです。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation='Architect')  
```  
  

  
###  <a name="bkmk_Ex2"></a> 例 2: ケース レベルの入れ子になったテーブルの属性を使用してフィルター処理  
 入れ子になったテーブルがマイニング構造に含まれている場合は、入れ子になったテーブルに値が存在するかどうかに基づいてフィルター処理することも、特定の値を含む入れ子になったテーブル行に基づいてフィルター処理することもできます。 次の例では、モデルに使用するケースを、Milk を購入したことがある 31 歳以上の顧客だけに制限します。  
  
 この例からわかるとおり、フィルターには、モデルに含まれている列のみを使用する必要はありません。 入れ子になったテーブル **Products** はマイニング構造の一部ですが、マイニング モデルには含まれていません。 それでも、この入れ子になったテーブル内の値や属性に基づいてフィルター処理を行うことができます。 これらのケースの詳細を表示するには、ドリルスルーを有効にする必要があります。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk')  
)  
```  
  
 
  
###  <a name="bkmk_Ex3"></a> 例 3:ケース レベルの入れ子になったテーブルの複数の属性にフィルター処理  
 次の例では、3 つの部分から成るフィルターを示します。ケース テーブルに適用する条件、入れ子になったテーブルの属性に対する条件、入れ子になったテーブル列の特定の値に対する条件の 3 つです。  
  
 フィルターの最初の条件 `Age > 30`は、ケース テーブル内の列に適用されます。 残りの条件は、入れ子になったテーブルに適用されます。  
  
 2 番目の条件 `EXISTS (SELECT * FROM Products WHERE ProductName='Milk'`では、入れ子になったテーブル内に、Milk を含む購入が 1 回以上存在するかどうかを調べます。 3 番目の条件 `Quantity>=2`は、顧客が 2 単位以上の Milk を一度に購入している必要があることを意味します。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity >= 2)   
)  
```  
  

  
###  <a name="bkmk_Ex4"></a> 例 4:ケース レベルの入れ子になったテーブルの属性がない場合にフィルター処理  
 次の例では、入れ子になったテーブル内に属性が存在しないケースをフィルター選択することで、特定の品目を購入しなかった顧客のケースに制限する方法を示します。 この場合、Milk を購入したことがない 31 歳以上の顧客を使用して、モデルのトレーニングが行われます。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName='Milk') )  
```  
  

  
###  <a name="bkmk_Ex5"></a> 例 5:入れ子になったテーブルの複数の値に対するフィルター処理  
 次の例では、入れ子になったテーブルのフィルター処理について説明します。 入れ子になったテーブルのフィルターは、ケース フィルターの後に適用され、入れ子になったテーブル行だけを制限します。  
  
 EXISTS を指定していないため、このモデルには、空の入れ子になったテーブルを持つケースが複数含まれる場合があります。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
WITH DRILLTHROUGH  
```  
  

  
###  <a name="bkmk_Ex6"></a> 例 6:入れ子になったテーブルの属性および EXISTS にフィルター処理  
 次の例では、入れ子になったテーブルに対するフィルターで、Milk か bottled water のいずれかを含む行に制限します。 さらに、`EXISTS` ステートメントを使用してモデル内のケースを制限します。 これにより、入れ子になったテーブルが空にならないようにします。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
FILTER (EXISTS (Products))  
```  
  

  
###  <a name="bkmk_Ex7"></a> 例 7:複雑なフィルターの組み合わせ  
 次のモデルのシナリオは例 4 と似ていますが、はるかに複雑です。 入れ子になったテーブル、 **ProductsOnSale**、フィルター条件を持つ`(OnSale)`の値を意味する **[onsale]** 必要があります`true`で製品に対する**ProductName**. この **[OnSale]** は構造列です。  
  
 フィルターの 2 番目の部分の**ProductsNotOnSale**、構文の繰り返しが、フィルター処理、ある製品の値**OnSale**は`not true``(!OnSale)`します。  
  
 最後にこれらの条件を組み合わせ、ケース テーブルに対する制限をさらに 1 つ追加します。 その結果、25 歳以上のすべての顧客を対象として、 **[ProductsOnSale]** の一覧内のケースに基づき、 **[ProductsNotOnSale]** の一覧内の製品の購入が予測されます。  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
  
###  <a name="bkmk_Ex8"></a> 例 8:日付でフィルター処理  
 他のデータと同様に、日付に基づいて入力列をフィルター処理することができます。 日付/時刻の型の列に含まれる日付は連続値です。そのため、大なり (>) や小なり (<) などの演算子を使用して、日付範囲を指定することができます。 データ ソースの日付が連続するデータ型で表されず、不連続値またはテキスト値として表されている場合は、日付範囲に基づいてフィルター処理を行うことはできず、個々の不連続値を指定する必要があります。  
  
 ただし、フィルターに使用されている日付列がモデルのキー列でもある場合は、時系列モデルの日付列に基づくフィルターを作成できません。 これは、時系列モデルおよびシーケンス クラスター モデルでは、日付列が `KeyTime` 型または `KeySequence` 型として処理される場合があるためです。  
  
 時系列モデルで連続する日付に対してフィルター処理を行う必要がある場合は、マイニング構造で列のコピーを作成し、新しい列に基づいてモデルをフィルター処理することができます。  
  
 たとえば、次の式は、Forecasting モデルに追加された、`Continuous` 型の日付列に対するフィルターを表しています。  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  モデルに列を追加すると、結果に影響を及ぼす場合があることに注意してください。 そのため、系列の計算に列を使用しない場合は、マイニング構造のみに列を追加し、モデルには追加しないでください。 列のモデル フラグを `PredictOnly` または `Ignore` に設定することもできます。 詳細については、「[モデリング フラグ &#40;データ マイニング&#41;](modeling-flags-data-mining.md)」を参照してください。  
  
 その他のモデルの種類では、他の列の場合と同様に、入力条件やフィルター条件として日付を使用することができます。 ただし、`Continuous` データ型でサポートされていない、特定のレベルの粒度を使用する必要がある場合は、複数の式を使用してフィルター処理と分析で使用する単位を抽出することで、データ ソースの派生値を作成できます。  
  
> [!WARNING]  
>  フィルター条件として日付を指定する場合は、現在の OS の日付の形式に関係なく、 `mm/dd/yyyy`という形式を使用する必要があります。 他の形式では、エラーが発生します。  
  
 たとえば、コール センターの結果にフィルターを適用して週末のみを表示する場合、データ ソース ビューに各日付の曜日名を抽出する式を作成して、その曜日名の値を入力に使用したり、フィルター処理で不連続値として使用したりすることができます。 繰り返し値はモデルに影響を及ぼす可能性があるため、日付列と不連続値ではなく、1 列のみを使用する必要があることを忘れないでください。  
  
 
  
## <a name="see-also"></a>参照  
 [マイニング モデルのフィルター &#40;Analysis Services - データ マイニング&#41;](mining-models-analysis-services-data-mining.md)   
 [テストおよび検証 &#40;データ マイニング&#41;](testing-and-validation-data-mining.md)  
  
  
