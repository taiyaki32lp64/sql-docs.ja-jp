---
title: SET EXACT コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997728"
---
# <a name="set-exact-command"></a>SET EXACT コマンド
異なる長さの 2 つの文字列を比較するための規則を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 正規表現が等価である文字の文字に一致する必要がありますを指定します。 比較式の末尾の空白は無視されます。 この比較では、2 つの式のうち、小さい方が長い式の長さが一致するように空白を右側に埋め込まれます。  
  
 OFF  
 (既定値。) 、等価である、式と一致するが文字の文字の右側にある式の末尾に到達するまでを指定します。  
  
## <a name="remarks"></a>コメント  
 両方の文字列が長さが同じ場合は、正確な設定の設定を指定しても効果はありません。  
  
## <a name="string-comparisons"></a>文字列の比較  
 Visual FoxPro では、等しいかどうかをテストする 2 つのリレーショナル演算子があります。  
  
 = 演算子が同じ型の 2 つの値の比較を実行します。 この演算子は、文字、数値、日付、および論理データの比較に適しています。  
  
 ただしを含む文字式を比較するときに、= 演算子、結果がない正確に期待どおりでは。 文字式を比較左から右の右側にある式の末尾まで、その他と等しくない、式の 1 つまでの文字の文字、= (SET 正確な OFF)、演算子に達するまで、両方の式の end は、または(設定の正確な ON) に達しました。  
  
 = = 演算子は、文字データの正確な比較が必要なときに使用できます。 2 つの文字式を比較する場合、演算子の両側の式を = =、= = 演算子は等しいと見なされる空白を含め同じ文字だけを含める必要があります。 使用して文字の文字列を比較すると、正確な設定の設定は無視されます = =。  
  
 次の表では、演算子の選択と設定の正確な設定が比較に影響を示します。 (アンダー スコアは、空白を表します)。  
  
|条件式|= オフ正確です|= の正確です|正確な ON または OFF = =|  
|----------------|------------------|-----------------|--------------------------|  
|"abc"="abc"|一致|一致|一致|  
|"ab"="abc"|一致なし|一致なし|一致なし|  
|"abc"="ab"|一致|一致なし|一致なし|  
|"abc"="ab_"|一致なし|一致なし|一致なし|  
|"ab"="ab_"|一致なし|一致|一致なし|  
|"ab_"="ab"|一致|一致|一致なし|  
|"""ab"を =|一致なし|一致なし|一致なし|  
|"ab"=""|一致|一致なし|一致なし|  
|"__" = ""|一致|一致|一致なし|  
|"" = "___"|一致なし|一致|一致なし|  
|TRIM("___") =""|一致|一致|一致|  
|""TRIM("___") を =|一致|一致|一致|  
  
## <a name="see-also"></a>関連項目  
 [SET ANSI コマンド](../../odbc/microsoft/set-ansi-command.md)
