---
title: DataMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4395f0ff113c8549ec2250d5fa87d37090627b3c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892910"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  ディメンションの非リーフメンバーに関連付けられているシステムによって生成されたデータメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 この関数は、任意の階層の非リーフメンバーに対して動作し、 [UPDATE CUBE ステートメント (MDX)](../mdx/mdx-data-manipulation-update-cube.md)コマンドで使用して、リーフメンバーの子孫ではなく、非リーフメンバーに直接データを書き戻すことができます。  
  
> [!NOTE]  
>  指定されたメンバーがリーフメンバーである場合、または非リーフメンバーに関連付けられたデータメンバーがない場合は、指定されたメンバーを返します。  
  
## <a name="example"></a>例  
 次の例では、各従業員の販売ノルマを示すために、計算されるメジャーで**DataMember**関数を使用します。  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX の主な概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
