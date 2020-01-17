---
title: StructureColumn (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7b6b436527aa36fb8f048a3b3c8fc55b970ef284
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065395"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定したケースに対応する構造列の値、または指定したケースの入れ子になったテーブルのテーブル値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>引数  
 structure-column-name。  
 ケースまたは入れ子になったテーブルのマイニング構造列の名前。  
  
## <a name="result-type"></a>結果の種類  
 返される型で参照されている列の型によって異なります、\<構造の列名 > パラメーター。 たとえば、参照されるマイニング構造列がスカラー値を含む場合、関数はスカラー値を返します。  
  
 参照されるマイニング構造列が入れ子になったテーブルである場合、関数はテーブル値を返します。 返されたテーブル値は、サブ SELECT ステートメントの FROM 句に使用できます。  
  
## <a name="remarks"></a>コメント  
 この関数はポリモーフィックで、SELECT 式リスト、WHERE 条件式、ORDER BY 式など、式を使用できるステートメント内の任意の場所で使用できます。  
  
 マイニング構造内の列の名前は文字列値とそのため、単一引用符で囲む必要があります。 たとえば、 `StructureColumn('`**列 1**`')`。 同じ名前を持つ列が複数ある場合、名前は SELECT ステートメントが含まれるコンテキスト内で解決されます。  
  
 使用してクエリから返された結果、 **StructureColumn**関数は、モデルに対するフィルターの存在を受けます。 つまり、モデル フィルターは、マイニング モデルに含まれるケースを制御します。 したがって、構造列上のクエリは、マイニング モデルに使用されたケースのみを返します。 ケース テーブルと入れ子になったテーブルの両方に対するマイニング モデル フィルターの影響を示すコード例については、このトピックの「例」のセクションを参照してください。  
  
 DMX SELECT ステートメントでこの関数を使用する方法の詳細については、次を参照してください。 [SELECT FROM&#60;モデル&#62;します。ケース&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)または[SELECT FROM&#60;構造&#62;します。ケース](../dmx/select-from-structure-cases.md)します。  
  
## <a name="error-messages"></a>エラー メッセージ  
 次のセキュリティ エラーは、親のマイニング構造に対するドリルスルー権限がユーザーに与えられていない場合に発生します。  
  
 ' % {ユーザー/}' の親マイニング構造にドリルスルーする権限がユーザーにありません、' % {model/}' マイニング モデルです。  
  
 次のエラー メッセージは、無効な構造列名が指定された場合に表示されます。  
  
 ' % {構造列名/}' にマイニング構造列が見つかりません、' % {構造/}'、現在のコンテキスト内のマイニング構造の親 (行 % {行/}、列 % {列/})。  
  
## <a name="examples"></a>使用例  
 ここに示す例では、次のマイニング構造を使用します。 マイニング構造には、2 つの入れ子になったテーブル列 `Products` および `Hobbies` が含まれます。 `Hobbies` 列の入れ子になったテーブルには、入れ子になったテーブルのキーとして使用される単一列があります。 `Products` 列の入れ子になったテーブルは、入力に使用されるキー列およびその他の列の両方を持つ、複雑な入れ子になったテーブルです。 次の例は、モデルですべての列を使用しない可能性があっても、多くの異なる列を組み込んでデータ マイニング構造を設計する方法を示しています。 これらの列の一部は、モデル レベルでパターンの汎用化に役立たない可能性がありますが、ドリルスルーには非常に有効です。  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 次に、以下のコード例で、作成した構造に基づいてマイニング モデルを作成します。  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>サンプル クエリ 1:マイニング構造から列を返す  
 次のサンプル クエリでは、マイニング モデルの一部として定義されている列 `CustomerName` および `Age` が返されます。 ただし、このクエリでは、構造の一部であってもマイニング モデルの一部ではない `Age` 列も返されます。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 年齢が 30 歳を超える顧客にケースを制限する行のフィルター処理は、モデルのレベルで実行されます。 したがって、この式は、構造データに含まれているが、モデルから使用されないケースを返しません。 モデル (`EXISTS (Products)`) の作成に使用するフィルター条件は、製品を購入した顧客のみにケースを制限するため、このクエリによって返されないケースが構造内にある可能性もあります。  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>サンプル クエリ 2:構造列にフィルターを適用します。  
 次のサンプル クエリは、モデル列 `CustomerName` および `Age`、および入れ子になったテーブル `Products` を返すだけでなく、モデルの一部ではない、入れ子になったテーブル内の列 `Quantity` の値も返します。  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 この例でフィルターが適用するは、職業が Architect の顧客にケースを制限する構造の列に注意してください (`WHERE StructureColumn('Occupation') = 'Architect'`)。 モデル フィルター条件はモデルの作成時に必ずケースに適用されるため、`Products` テーブル内に条件を満たす行が少なくとも 1 つあるケースのみが、モデル ケースに入れられます。 したがって、入れ子になったテーブル `Products` のフィルターとケース `('Occupation')` のフィルターの両方が適用されます。  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>サンプル クエリ 3:入れ子になったテーブルから列を選択  
 次のサンプル クエリでは、トレーニング ケースとして使用された顧客の名前がモデルから返されます。 顧客ごとに、購入の詳細を含む入れ子になったテーブルも返されます。 モデルが含まれますが、`ProductName`列、モデルの値を使用していない、`ProductName`列。 モデルだけが確認では、通常、製品を購入したかどうか (`NOT``OnSale`) 価格。 このクエリでは、製品名だけでなく、モデルには含まれていない購入した数量も返されます。  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 マイニング モデルでドリルスルーが有効でない限り、`ProductName` 列または `Quantity` 列を返すことはできません。  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>サンプル クエリ 4:フィルターと入れ子になったテーブルの列を返す  
 次のサンプル クエリは、マイニング構造に含まれるがモデルに含まれない、ケースおよび入れ子になったテーブル列を返します。 モデルは既に `OnSale` 製品が存在するかどうかでフィルター処理されていますが、このクエリはマイニング構造列 `Quantity` にフィルターを追加します。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
