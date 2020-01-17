---
title: PredictSequence (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6828b77af36b5dbbc50fbca0210961a7f2ed20c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041923"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定された一連のシーケンス データに対して予測される将来のシーケンス値です。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>戻り値の型  
 A\<テーブル式 >。  
  
## <a name="remarks"></a>コメント  
 場合、 *n*パラメーターを指定すると、次の値を返します。  
  
-   場合*n*が 0 の場合、次に、最も可能性の高いシーケンス値より大きい*n*手順を実行します。  
  
-   両方*n 開始*と*n エンド*指定すると、シーケンスの値から*n 開始*に*n エンド*します。  
  
## <a name="examples"></a>使用例  
 次の例は、顧客が購入する可能性が高い 5 つの製品のシーケンスを返します、 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] Sequence Clustering マイニング モデルに基づいてデータベース。  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
