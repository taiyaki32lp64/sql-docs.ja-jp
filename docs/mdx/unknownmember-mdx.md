---
title: UnknownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0332b200a74044dcd4e7d8d308923cc4b759738
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097283"
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)


  レベルまたはメンバーに関連付けられた不明なメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式。  
  
## <a name="remarks"></a>コメント  
 Analysis Services は、階層が不明の場合に、ファクト テーブルのデータを階層に関連付けるに不明なメンバーを作成します。 不明なメンバーは、次のレベルのいずれかで指定できます。  
  
-   集計されない属性階層の場合、最上位レベル。  
  
-   最初のレベル以下で、**すべて**自然階層のレベル。  
  
-   不自然階層の場合、任意のレベル。  
  
 メンバー式が指定されている場合、 **UnknownMember**関数は、指定されたメンバーの不明なメンバーの子を返します。 指定されたメンバーが存在しない場合、関数は NULL を返します。  
  
 階層式が指定されている場合、 **UnknownMember**関数が存在する場合、最上位レベルで不明なメンバーを返します。  
  
 不明なメンバーはレベルまたはメンバーが存在しない場合、 **UnknownMember**関数 null のメンバーを作成します。  
  
> [!NOTE]  
>  その階層またはメンバーに不明なメンバーが存在しない場合、エラーが生成されます。  
  
## <a name="examples"></a>使用例  
 次の例では、メジャー ディメンションのすべてのメンバー、Product 属性階層の All Products メンバーの不明なメンバーを返します。  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 次の例では、Product Categories 階層は、メジャー ディメンションのすべてのメンバーの不明なメンバーを返します。  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
