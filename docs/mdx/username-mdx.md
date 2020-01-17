---
title: UserName (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097271"
---
# <a name="username-mdx"></a>UserName (MDX)


  現在の接続のユーザー名とドメインの名前を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>コメント  
 返される値は、次の形式の文字列です。  
  
 *domain-name\user-name*  
  
## <a name="example"></a>例  
 次の例では、クエリを実行しているユーザーのUserNameを返します。  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
