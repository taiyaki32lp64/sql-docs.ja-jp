---
title: メンバー式を使用する |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d40d6a3b6cacb65cf1463b0eeb8b29e59e079e4
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893512"
---
# <a name="using-member-expressions"></a>メンバー式の使用


  メンバー式には、メンバー識別子、メンバー関数、またはメンバーに変換できる式が含まれています。  
  
 メンバー識別子には、さまざまな形式があります。 メンバー識別子の最も単純な形式は、メンバーの名前で構成されます。 以下に例を示します。  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 ただし、異なる階層に同じ名前のメンバーが複数存在する場合、クエリが返すメンバーを決定する方法はありません。 たとえば、次のクエリでは、[CY 2004] という名前のメンバーに関するデータを要求します。 クエリ正常に実行されますが、Adventure works キューブにその名前のメンバーが少なくとも6つ存在します。  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 したがって、メンバー識別子の最も信頼性の高い形式はメンバーの一意な名前です。これにより、キューブ内の特定のメンバーが識別されるようになります。 Analysis Services は、いくつかの方法で一意の名前を生成できますが、一意の名前は常に少なくとも2つの識別子 (ディメンション名とメンバー名またはメンバーキー) で構成されます。 一意の名前の形式は次のとおりです。  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 次に、Adventure Works キューブのメンバーを表す一意の名前の例をいくつか示します。  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 MDX 関数には、メンバーを返すものが多数存在します。 完全な一覧については、「 [Mdx 関数リファレンス&#40;&#41; mdx](../mdx/mdx-function-reference-mdx.md) 」を参照してください。  
  
> [!NOTE]  
>  メンバー名とメンバーキーの詳細については、「メンバーの操作」、「[組&#41;」、および「MDX の設定&#40;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [MDX &#40;の式&#41;](../mdx/expressions-mdx.md)  
  
  
