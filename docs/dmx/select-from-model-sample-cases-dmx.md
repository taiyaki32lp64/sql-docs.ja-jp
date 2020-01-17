---
title: SELECT FROM&lt;model&gt;.SAMPLE_CASES (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0838c688b0518bf1fc7ed6c5d65c3ef03d0a7aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928317"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>SELECT FROM&lt;model&gt;.SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データ マイニング モデルの学習に使用されるケースを表すサンプル ケースを返します。  
  
 このステートメントを使用して、マイニング モデルを作成するときにドリルスルーを有効する必要があります。 ドリルスルーを有効にする方法の詳細については、次を参照してください[CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md)、 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)、および[ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式リスト*  
 関連付けられた列識別子のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子です。  
  
 *条件の一覧*  
 任意。 列の一覧から返される値を制限する条件。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 サンプル ケースは可能性がありますが生成され、トレーニング データに実際に存在しません。 返されたケースは、指定されたコンテンツ ノードを表します。  
  
 ですが、[!INCLUDE[msCoName](../includes/msconame-md.md)]シーケンス クラスター アルゴリズムは、唯一[!INCLUDE[msCoName](../includes/msconame-md.md)]選択から使用をサポートするアルゴリズム\<モデル >。SAMPLE_CASES、サード パーティのアルゴリズム可能性がありますもサポートします。  
  
## <a name="examples"></a>使用例  
 次の例では、Target Mail マイニング モデルの学習に使用されるサンプル ケースを返しています。 使用して、 [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md)で機能、**WHERE**句は 000000003 ノードに関連付けられているケースのみを返します。 ノード文字列は、スキーマ行セットの NODE_UNIQUE_NAME 列にあります。  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>関連項目  
 [SELECT&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
