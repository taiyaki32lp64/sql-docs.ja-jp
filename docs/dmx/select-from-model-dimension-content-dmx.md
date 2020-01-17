---
title: SELECT FROM&lt;モデル&gt;します。DIMENSION_CONTENT (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7fac89454cd31c1334e41d4c2367143f31476e20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928367"
---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM&lt;モデル&gt;します。DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  マイニング モデルは、OLAP キューブのディメンションとして使用できます。このとき、モデルの各ノードは、ディメンションのメンバーとして表されます。 **SELECT FROM\<モデル >。Dimension_CONTENT**ステートメントは、ディメンションとしての使用に関連するモデルの内容を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式リスト*  
 コンテンツ スキーマ行セットから派生する、関連する列識別子のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子です。  
  
 *条件式*  
 任意。 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 アルゴリズム プロバイダーでは、コンテンツが返され、それを整理する方法を定義します。 たとえば、プロバイダーはディメンション コンテンツに示されるノード数を制限する場合があります。  
  
 次の表は、ディメンション コンテンツのためにクエリできる列と、各列がデータ マイニング ディメンションとして実行する関数について示しています。  
  
|CONTENT 行セット列|データ マイニング ディメンションの関数|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|メンバー プロパティです。|  
|NODE_NAME|メンバー プロパティです。|  
|NODE_UNIQUE_NAME|キー属性です。|  
|NODE_TYPE|メンバー プロパティです。|  
|NODE_CAPTION|CaptionColumn**キー**属性。|  
|CHILDREN_CARDINALITY|メンバー プロパティです。|  
|PARENT_UNIQUE_NAME|RelatedAttribute**キー**属性 (親子階層の ParentAttribute)。|  
|NODE_DESCRIPTION|メンバー プロパティです。|  
|NODE_RULE|メンバー プロパティです。|  
|MARGINAL_RULE|メンバー プロパティです。|  
|NODE_PROBABILITY|メンバー プロパティです。|  
|MARGINAL_PROBABILITY|メンバー プロパティです。|  
|NODE_SUPPORT|メンバー プロパティです。|  
  
## <a name="examples"></a>使用例  
  
### <a name="description"></a>説明  
 次の例は、ディメンションとしてのモデルの使用に関する、`[TM Decision Tree]` モデル コンテンツのすべての列を選択します。  
  
### <a name="code"></a>コード  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>関連項目  
 [選択&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
