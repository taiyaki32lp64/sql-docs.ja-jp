---
title: Leaves (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d29c77250c23900d74d1969a6c37bc719c89cdd7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905732"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  すべての属性 (必要に応じて、特定のディメンションに属しているこれらに限定する) から成るセットを返します。 各属性 x の戻り値のセットで、x が粒度属性は、または直接または間接的に粒度属性に関連が粒度は属性 x に対して設定、スライスには影響しません。 **Leaves**関数が SCOPE ステートメント内または、代入の左辺で使用するために設計されています。  
  
## <a name="syntax"></a>構文  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Dimension_Expression*  
 ディメンションを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 リーフ メンバーは、すべての属性階層の最下位レベルのクロス結合して形成される組です。 計算されるメンバーは除外されます。  
  
-   ディメンション名が指定されている場合、**Leaves**関数は、指定されたディメンションのキー属性のリーフ メンバーを含むセットを返します。  
  
-   ディメンションの複数のメジャー グループに関連付けられている場合、現在のスコープ内のメジャーの使用されます。  
  
-   ディメンション名が指定されていない場合は、キューブ全体のリーフ メンバーで構成されるセットを返します。  
  
    > [!NOTE]  
    >  ディメンション式が、階層に解決され、階層の一意の名前は、ディメンションの一意の名前と同じかどうか (キューブ ディメンション プロパティ HierarchyUniqueNameStyle = ExcludeDimensionName であり、階層名 = ディメンション名)、ディメンションが、このオプションを使用するとします。  
  
    > [!IMPORTANT]  
    >  すべての属性は、現在のスコープ内のメジャー グループに同じ粒度をあるされていない場合、エラーが生成されます。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
