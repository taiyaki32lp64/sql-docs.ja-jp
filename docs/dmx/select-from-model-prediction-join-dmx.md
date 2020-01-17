---
title: SELECT FROM&lt;モデル&gt;PREDICTION JOIN (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b592aef0ba3831c5513e039ee4552d826468e819
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928328"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM&lt;モデル&gt;PREDICTION JOIN (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  外部データ ソース内の列の状態を予測するのにマイニング モデルを使用します。 **PREDICTION JOIN**ステートメントをモデルに、ソース クエリからは、各ケースに一致します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *select 式リスト*  
 マイニング モデルから派生する、列の識別子と式のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子です。  
  
 *サブ選択します。*  
 埋め込まれた select ステートメント。  
  
 *ソース データ クエリ*  
 ソース クエリです。  
  
 *マッピングのリストを結合*  
 任意。 ソース クエリから列をモデルから列を比較する論理式。  
  
 *条件式*  
 任意。 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 ON 句では、ソース クエリから列とマイニング モデルからの列間のマッピングを定義します。 このマッピングは、列は、予測を作成する入力として使用できるように、マイニング モデル内の列に、ソース クエリから列を出力するために使用されます。 内の列、 \<*マッピングのリストを結合*> 次の例に示すように、等号 (=) を使用して関連します。  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 入れ子になったテーブルを ON 句にバインドする場合、入れ子になった列のレコードが所属するケースをアルゴリズムが正しく識別できるように、キー列をすべての非キー列とバインドします。  
  
 予測結合のソース クエリは、テーブルまたは単一クエリのどちらかにできます。  
  
 テーブル式を返さない予測関数を指定することができます、 \< *select 式リスト*> と\<*条件式*>。  
  
 **NATURAL PREDICTION JOIN**まとめて、モデル内の列名に一致するソース クエリから列名が自動的にマップします。 使用する場合**自然予測**ON 句を省略することができます。  
  
 WHERE 条件は、予測可能なにのみ適用される列または関連する列を指定できます。  
  
 ORDER by 句は、引数として 1 つの列のみを受け入れることができます。つまり、1 つ以上の列を並べ替えることはできません。  
  
## <a name="example-1-singleton-query"></a>例 1 : 単一クエリ  
 次の例では、特定の人が実際に自転車を購入するかどうかを予測するクエリを作成する方法を示します。 このクエリでは、データはテーブルまたはその他のデータ ソースに格納されませんが、クエリに直接入力されます。 クエリ内の人物は、次の特徴を持ちます。  
  
-   35 才  
  
-   持ち家所有  
  
-   2 台の自家用車を所有  
  
-   自宅で動作している 2 つの子を持つ  
  
 人がによって返される、表形式の値のセットと、自転車を購入したかどうかを示すブール値を返します、クエリの TM Decision Tree マイニング モデルとサブジェクトに関する既知の特徴を使用して、 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)関数、予測が行われた方法について説明します。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>例 2:OPENQUERY の使用  
 次の例では、外部データセットに格納されている潜在顧客のリストを使用してバッチ予測クエリを作成する方法を示します。 インスタンスで定義されているデータ ソース ビューの一部であるため、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、クエリで使用できる[OPENQUERY](../dmx/source-data-query-openquery.md)データを取得します。 テーブル内の列の名前は、マイニング モデルで異なるため、 **ON**句を使用して、モデル内の列に、テーブル内の列をマップする必要があります。  
  
 クエリでは、表に、各人物が、0 は「おそらくは自転車を購入しない」、1 は"probably will buy 自転車"自転車を購入する可能性があるかどうかを示すブール型の列と共にで各ユーザーの姓と名を返します。 最後の列には、予測結果の確率が含まれます。  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 データ セットを顧客名で、自転車を購入し、一覧の並べ替えに予測された顧客のみを制限するには、WHERE 句と ORDER BY 句を前の例に追加できます。  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>例 3: アソシエーションの予測  
 次の例は、[!INCLUDE[msCoName](../includes/msconame-md.md)] アソシエーション アルゴリズムから作成したモデルを使用して予測を作成する方法を示します。 関連する製品を推奨するアソシエーション モデルに対する予測を使用できます。 たとえば、次のクエリでは、一緒に購入される可能性が最も高い 3 つの製品が返されます。  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 [Predict &#40;DMX&#41; ](../dmx/predict-dmx.md)関数はポリモーフィックでありすべての種類のモデルで使用できます。 関数に引数として値 3 を使用して、クエリによって返される項目の数を制限します。 **選択**NATURAL PREDICTION JOIN 句を次の一覧は、予測の入力として使用する値を提供します。  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 例の結果を次に示します。  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 予測可能な属性を含む列`[v Assoc Seq Line Items]`テーブルの列は、クエリは入れ子になったテーブルを含む 1 つの列を返します。 既定では、入れ子になったテーブル列の名前は`Expression`します。 プロバイダーが階層的な行セットをサポートしていない場合は使用できます、 **FLATTENED**キーワードに結果を見やすくこの例で示すようにします。  
  
## <a name="see-also"></a>関連項目  
 [選択&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
