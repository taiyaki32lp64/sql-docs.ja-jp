---
title: EXISTING キーワード (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6c5e8dbe3e1b1ad44286bcbb79132010cad618a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073966"
---
# <a name="existing-keyword-mdx"></a>EXISTING キーワード (MDX)
  指定されたセットを現在のコンテキストで評価するように設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 有効な多次元式 (MDX) セット式です。  
  
## <a name="remarks"></a>コメント  
 既定では、セットの評価は、そのセットのメンバーを含むキューブのコンテキストで実行されます。 `Existing` キーワードを指定すると、指定されているセットの評価が現在のコンテキストで行われます。  
  
## <a name="example"></a>例  
 次の例では、`Aggregate`  関数を使用して評価された、ユーザー選択の State-Province メンバー値に基づいて、1 つ前の期よりも売上が減少した再販業者の数を返します。 Product ディメンションに含まれる製品カテゴリに関して減少した売上の値を返すために、 [Hierarchize (MDX)](/sql/mdx/hierarchize-mdx) 関数および [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) 関数を使用しています。 `Existing`キーワードのセットを強制する、 `Filter` State-province 属性階層の Washington および Oregon メンバーには、現在のコンテキストで評価する関数。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>参照  
 [Count (セット) (MDX)](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers (MDX)](/sql/mdx/addcalculatedmembers-mdx)   
 [Aggregate (MDX)](/sql/mdx/aggregate-mdx)   
 [Filter (MDX)](/sql/mdx/filter-mdx)   
 [Properties (MDX)](/sql/mdx/properties-mdx)   
 [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize (MDX)](/sql/mdx/hierarchize-mdx)   
 [MDX 関数リファレンス (MDX)](/sql/mdx/mdx-function-reference-mdx)  
  
  
