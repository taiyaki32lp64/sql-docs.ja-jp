---
title: '[モデル&lt;&gt;から] を選択します。ケース (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5f0334c37eeedafee7066f01d61745fcb82d1629
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892843"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>[モデル&lt;&gt;から] を選択します。ケース (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  ドリルスルーをサポートし、モデルのトレーニングに使用されたケースを返します。 マイニング構造とマイニング モデルについてドリルスルーを有効にした場合、ユーザーが適切な権限を持っているときは、モデルに含まれていない構造列も返すことができます。  
  
 ドリルスルーがマイニング モデルで使用可能でない場合、このステートメントは失敗します。  
  
> [!NOTE]  
>  データ マイニング拡張機能 (DMX) では、ドリルスルーはモデルの作成時にのみ可能です。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して既存のモデルにドリルスルーを追加することは可能ですが、ケースの表示またはクエリを実行する前にモデルを再処理する必要があります。  
  
 ドリルスルーを有効にする方法の詳細については、「[マイニング&#40;モデル dmx&#41;を作成](../dmx/create-mining-model-dmx.md)する」、「 [ &#40;dmx&#41;を選択](../dmx/select-into-dmx.md)する」、および「[マイニング構造&#40;dmx&#41;を変更](../dmx/alter-mining-structure-dmx.md)する」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 式のコンマ区切りのリストです。 式には、列識別子、ユーザー定義関数、UDF、VBA 関数などを含めることができます。  
  
 マイニング モデルに含まれていない構造列を含めるには、関数 `StructureColumn('<structure column name>')` を使用します。  
  
 *model*  
 モデル識別子です。  
  
 *条件式*  
 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 マイニング モデルとマイニング構造の両方についてドリルスルーを有効にした場合、そのモデルと構造に対するドリルスルー権限を持つロールのメンバー ユーザーが、マイニング モデルに含まれていないマイニング構造の列にアクセスできるようになります。 したがって、機密データや個人情報を保護するには、個人情報をマスクするデータソースビューを作成し、必要な場合にのみ、マイニング構造に対する**Allowdrillthrough スルー**権限を付与する必要があります。  
  
 タイムシリーズモデルで[lag &#40;DMX&#41; ](../dmx/lag-dmx.md)関数を使用すると、各ケースと初期時間の間のタイムラグを取得またはフィルター処理できます。  
  
 **WHERE**句[で&#40;IsInNode&#41; DMX](../dmx/isinnode-dmx.md)関数を使用すると、スキーマ行セットの NODE_UNIQUE_NAME 列によって指定されたノードに関連付けられているケースのみが返されます。  
  
## <a name="examples"></a>使用例  
 次の例は、 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データベースとそれに関連付けられているマイニングモデルに基づいた、マイニング構造を対象としたメーリングに基づいています。 詳細については、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」を参照してください。  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>例 1 : モデルケースおよび構造列へのドリルスルー  
 次の例は、Targeted Mailing モデルのテストに使用されたすべてのケースの列を返します。 モデルの基となるマイニング構造に、提示されたテスト データセットが含まれていない場合、このクエリはケースを返しません。 必要な列のみを返す式のリストを使用できます。  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>例 2:特定のノードのトレーニングケースへのドリルスルー  
 次の例は、Cluster 2 のトレーニングに使用されたケースのみを返します。 Cluster 2 のノードの NODE_UNIQUE_NAME 列の値は '002' です。 また、この例ではマイニング モデルに含まれていなかった構造列 [Customer Key] を返し、その列の別名 `CustomerID` を指定します。 構造列の名前は文字列値として渡されるので、角かっこではなく引用符で囲む必要があります。  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 構造列を返すには、マイニング モデルとマイニング構造の両方についてドリルスルー権限を有効にする必要があります。  
  
> [!NOTE]  
>  すべての種類のマイニング モデルでドリルスルーがサポートされるわけではありません。 ドリルスルーをサポートするモデルの詳細については、「[ドリルスルークエリ&#40;のデータマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SELECT&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
