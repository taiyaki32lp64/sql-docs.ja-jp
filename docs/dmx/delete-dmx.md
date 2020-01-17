---
title: 削除 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1c75a6ff18b26bee65365acbc068de87678a9c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070762"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用するデータ マイニング拡張機能 (DMX) 句に従って、マイニング モデル、マイニング構造、またはマイニング構造とそれに関連するすべてのマイニング モデルが削除されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子です。  
  
 *構造体*  
 構造識別子です。  
  
## <a name="remarks"></a>コメント  
 指定しない場合**マイニング モデルの**または**マイニング構造の**、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]名前に基づいてオブジェクトの種類を検索し、正しいオブジェクトを処理します。 サーバーが同じ名前のマイニング構造とマイニング モデルを持つ場合、エラーが返されます。  
  
 次の表は、異なる形式の構文を使用した場合の結果について示しています。  
  
|ステートメントから削除してください。|結果|  
|---------------|------------|  
|マイニング構造から削除 *\<構造体 >*<br /><br /> または<br /><br /> マイニング構造から削除 *\<構造 >* します。コンテンツ|マイニング構造に対して ProcessClear を実行します。 すべての内容がマイニング構造および関連するマイニング モデルから削除されます。|  
|マイニング構造から削除 *\<構造 >* します。場合|マイニング構造に対して ProcessClearStructureOnly を実行します。 関連するマイニング モデルは保存したまま、すべての内容がマイニング構造から削除されます。 マイニング構造が削除された後では、関連するマイニング モデルでのドリルスルーは失敗します。|  
|マイニング モデルから削除 *\<モデル >*<br /><br /> または<br /><br /> マイニング モデルから削除 *\<モデル >* します。コンテンツ|マイニング モデルに ProcessClear を実行しますが、状態の値をそのまま残されます。 状態値は、その列で使用できる状態を表します。 たとえば、性別の列の状態値は、男性と女性です。|  
  
 処理の種類の詳細については、次を参照してください。 [Type 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)します。  
  
## <a name="examples"></a>使用例  
 次の例では、すべての内容が NB_Sample モデルから削除されます。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
