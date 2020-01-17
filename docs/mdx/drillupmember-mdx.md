---
title: DrillupMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5dfdec16d20173639cc92a80b1ca546f44b70334
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049191"
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)


  2 番目に指定されたセット内のメンバーの子孫ではないが、指定されたセット メンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **DrillupMember**関数は、2 番目のセット内のメンバーの子孫である最初のセットで指定されたメンバーに基づくメンバーのセットを返します。 1 番目のセットの次元は任意ですが、2 番目には 1 次元のセットを指定する必要があります。 順序は、最初のセット内の元のメンバー間で保持されます。 関数では、2 番目のセット内のメンバーの直接の子孫である 1 番目のセット内のメンバーのみを含めることによって、セットを構築します。 最初のセット内のメンバーの直接の先祖が 2 番目のセットに存在しない場合は、この関数によって返されたセットの最初のセットに含まれるメンバーが含まれます。 2 番目のセットに親メンバーの前にある最初のセット内の子孫も含まれます。  
  
 最初のセットは、メンバーではなく組を含めることができます。 組のドリル ダウンでは、OLE DB の拡張機能し、メンバーではなく組のセットを返します。  
  
> [!IMPORTANT]  
>  メンバーのドリルアップは、直後に子または子孫が続く場合のみ行われます。 両方のドリル ダウン、セット内のメンバーの順序は重要です\*と Drillup\*関数のファミリです。 使用を検討して、 **Hierarchize**最初のセットのメンバーの適切に順序付けする関数。  
  
## <a name="example"></a>例  
 次の 3 つの例は、2 番目のセットを除いて同一です。 最初の例では、2 番目のセットは United States です。 その結果、Colorado は結果セットから除外されます。 United States の子孫になります。  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 2 つの例のメンバーの順序の重要性が表示されます。 **DrillupMember**のみ最初のセット内の子孫の直前に置かそれらのメンバーのドリル アップ、それをドリル アップしません、Canada メンバーです。 カナダは米国および Colorado によって子孫から分離します。 あるようにカナダ アルバータ州のすぐ上のメンバーの順序を変更する場合、Alberta と Brunswick の両方から除外されます、行セット。  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 3 つの例に示す方法の使用**Hierarchize** Canada メンバーに対するメンバーの順序、およびドリル アップの影響を軽減することができます。  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
