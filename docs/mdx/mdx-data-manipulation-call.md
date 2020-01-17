---
title: CALL ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: de74590ac4c43a9141c0ab2092babf41ffd23ba5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106299"
---
# <a name="mdx-data-manipulation---call"></a>MDX データ操作 - CALL


  現在のスコープ内、または指定されたキューブで必要に応じて、void を返すストアド プロシージャを実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>引数  
 *SP_Name*  
 ストアド プロシージャの名前を指定する有効な文字列式です。  
  
 *SP_Argument*  
 呼び出したストアド プロシージャに渡す引数を指定する有効な文字列式です。  
  
 *Cube_Expression*  
 キューブの名前を指定する有効な文字列キューブ式です。  
  
## <a name="remarks"></a>コメント  
 **呼び出す**ステートメントを指定した登録されているストアド プロシージャを実行、指定したストアド プロシージャの 1 つまたは複数の引数を含めることもできます。 **呼び出す**ステートメントは白い隙間を返すストアド プロシージャでのみ使用されます。 MDX 式の中でこのステートメントと他の関数や演算子を併用することはできません。 値を返す登録済みのストアド プロシージャについては、MDX 式の中で直接呼び出すことも、MDX の他の関数や演算子と併用することも可能です。  
  
 キューブが指定されていない場合、ステートメントでは、現在のキューブでのストアド プロシージャが実行されます。  
  
> [!NOTE]  
>  クライアントでは、ストアド プロシージャが登録されていない場合、**呼び出す**ステートメントのインスタンスからストアド プロシージャを呼び出すしよう[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。  
  
## <a name="see-also"></a>関連項目  
 [MDX データ操作ステートメント &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [ストアド プロシージャの使用 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
