---
title: タプル |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5025d76d439933f7392d55661ca52d3f33992db8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073766"
---
# <a name="tuples"></a>Tuples
  組はキューブからデータのスライスを一意に識別します。 組は、同じ階層に属するメンバーが複数存在しない限り、ディメンション メンバーを組み合わせて作成されます。  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>組の暗黙的または既定の属性メンバー  
 MDX クエリまたは式で組を定義する際に、すべての属性階層の属性メンバーを明示的に含める必要はありません。 属性階層のメンバーをクエリまたは式に明示的に含めなかった場合、その属性階層の既定のメンバーが暗黙的に組に含められます。 (All) メンバーが存在する場合、キューブで他に明示的に定義されていない限り、(All) メンバーがすべての属性階層の既定のメンバーになります。 属性階層に (All) メンバーが存在しない場合、属性階層の最上位のメンバーが既定のメンバーになります。 既定のメジャーを明示的に定義している場合を除き、キューブ内で指定された最初のメジャーが既定のメジャーになります。 詳細については、「[既定メンバーの定義](../attribute-properties-define-a-default-member.md)」および「[DefaultMember (MDX)](/sql/mdx/defaultmember-mdx)」を参照してください。  
  
 たとえば、次の組はメジャー ディメンションの単一のメンバーのみを明示的に定義することで、Adventure Works データベースの 1 つのセルを識別しています。  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 上記の例は、メジャー ディメンションの Reseller Sales Amount メンバーとキューブに所属するすべての属性階層の既定のメンバーから構成されるセルを一意に識別します。 Destination Currency 属性階層を除くすべての属性階層の既定のメンバーは (All) メンバーです。 Destination Currency 階層の既定のメンバーは US Dollar メンバーです (この既定のメンバーは Adventure Works キューブの MDX スクリプトで定義されています)。  
  
 次のクエリは、上記の例で指定した組が参照するセルの値 ($80,450.596.98) を返します。  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  クエリでセット (ここでは、1 つの組から構成されます) の軸を指定するときは、行の軸のセットを指定する前に列の軸のセットを指定する必要があります。 列の軸は、*axis(0)* 、または単に *0* とも表現できます。 MDX クエリの詳細については、「[MDX の基本的なクエリ (MDX)](mdx-query-the-basic-query.md)」を参照してください。  
  
### <a name="tuples-as-values-or-member-references"></a>値またはメンバー参照としての組  
 上記の例のように、クエリで組を使用して、その組が参照しているセルの値を取得できます。 また、式で組を使用して、組で指定されているメンバーを明示的に参照できます。 組を取得または使用する関数をクエリまたは式で使用できます。 組を使用して、組で指定されているセルの値を参照できます。また、関数内で使用する場合はメンバーの組み合わせを指定できます。  
  
### <a name="tuple-dimensionality"></a>組の次元  
 組の中のメンバーの並びまたは順序を組の *次元* といいます。 暗黙的なメンバーの出現順序は常に変わらないので、通常は組の中で明示的に定義されているメンバーについて次元を考えます。 組のメンバーの順序は、組のセットを定義するときに重要です。 次の例では、列の軸となる組で 2 つのメンバーが使用されています。  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  複数のディメンションから構成される組のメンバーを明示的に指定するときは、組全体をかっこで囲む必要があります。 組のメンバー 1 つのみを指定する場合、かっこの使用は任意です。  
  
 上記の例のクエリで使用している組は、メジャー ディメンションの Reseller Sales Amount メジャーと Date ディメンションの Calendar Year 属性階層の CY 2004 メンバーが交差するキューブ セルを返すよう指定しています。  
  
> [!NOTE]  
>  属性メンバーは、メンバー名またはメンバー キーで参照できます。 上記の例で、[CY 2004] への参照を &[2004] としてもかまいません。  
  
## <a name="see-also"></a>関連項目  
 [MDX の主な概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)   
 [キューブ空間](cube-space.md)   
 [Autoexists](autoexists.md)   
 [メンバー、組、およびセットの操作 (MDX)](working-with-members-tuples-and-sets-mdx.md)  
  
  
