---
title: DrilldownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: af2d52f176b67b27a29eafb662ca539ced53ebbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139098"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  2 番目に指定されたセット内に存在する、指定されたセットのメンバーをドリル ダウンします。  
  
 または、最初の組階層または必要に応じて指定した階層を使用して、関数が組のセットをドリル ダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Target_Hierarchy*  
 階層を返す有効な多次元式 (MDX) 式。  
  
 *再帰*  
 セットの再帰的な比較を示すキーワードです。  
  
 *Include_Calc_Members*  
 計算されるメンバーがドリルダウン結果に含まれるようにするキーワード。  
  
## <a name="remarks"></a>コメント  
 この関数は、階層によって順序付けられた子メンバーのセットを返しも、2 番目のセットに存在する最初のセットで指定されたメンバーが含まれています。 最初のセットに親メンバーと 1 つ以上の子が含まれている場合、親メンバーはドリル ダウンされません。 1 番目のセットの次元は任意ですが、2 番目には 1 次元のセットを指定する必要があります。 1 番目のセット内の元のメンバー間で順序を維持、それぞれの親メンバーの結果に含まれるすべての子メンバーを設定する点を除いて、関数がすぐに含まれています。 関数は、子が 2 番目のセットに存在することも、最初のセット内の各メンバーを取得して、結果セットを構築します。 場合**再帰**を指定すると、関数は、再帰的に比較が以上までは 2 つ目のセットに存在することも、結果セット内の各メンバーの子を取得する 2 番目のセットに対して結果のメンバーを設定するには2 番目のセットには、結果セットからメンバーを確認できます。  
  
 XMLA プロパティのクエリを実行する**MdpropMdxDrillFunctions**サーバーがドリル関数が提供するサポートのレベルを確認することができます表示[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)。詳細についてはします。  
  
 最初のセットは、メンバーではなく組を含めることができます。 組のドリル ダウンは OLE DB の拡張機能であり、メンバーではなく組のセットを返します。  
  
> [!IMPORTANT]  
>  メンバーがないドリルダウン場合、その子のいずれかですぐにその後にします。 ドリル ダウン * と Drillup、セット内のメンバーの順序は重要です\*関数のファミリです。  
  
## <a name="examples"></a>使用例  
 次の例では、最初のセットのメンバーであり 2 番目のセットにも存在する、Australia へのドリル ダウンを行っています。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、最初のセットのメンバーであり 2 番目のセットにも存在する、Australia へのドリル ダウンを行っています。 RECURSIVE 引数があるので、結果セットのメンバー (State-Province レベルのメンバー) を 2 番目のセットと再帰的に比較し、結果セット内にあり 2 番目のセット内にも存在する各メンバーの子 (City レベルのメンバー) を取得するという操作が、結果セットのメンバーが 2 番目のセット内で検出されなくなるまで続けて行われます。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
