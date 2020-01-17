---
title: エラー (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 91d07c6bbb4eb4731c9a802e47cd8f4c71aa5aeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031229"
---
# <a name="error-mdx"></a>Error (MDX)


  必要に応じて指定したエラー メッセージを提供するエラーが発生します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>引数  
 *Error_Text*  
 返すエラー メッセージを格納した有効な文字列式です。  
  
## <a name="examples"></a>使用例  
 次のクエリを使用する方法を示しています、**エラー**計算されるメジャー内の関数。  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
