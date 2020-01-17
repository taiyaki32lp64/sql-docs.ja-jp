---
title: 返される XML を構造化する際の AUTO モード ヒューリスティック | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91fa97c61734f378163fdac9adf1918caefabc7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288912"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>返される XML を構造化する際の AUTO モード ヒューリスティック
  AUTO モードでは、返される XML の構造はクエリに基づいて決定されます。 要素を入れ子にする方法を決定するとき、AUTO モード ヒューリスティックによって、隣接する行の列値が比較されます。 **ntext**型、 **text**型、 **image**型、および **xml**型を除くすべての型の列が比較されます。 **(n)varchar(max)** 型と **varbinary(max)** 型の列は比較されます。  
  
 次の例では、生成される XML の構造を決定する AUTO モード ヒューリスティックを示します。  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
```  
  
 テーブル T1 のキーが指定されていない場合は、新しい <`T1`> 要素の開始位置を決定するために、**ntext** 型、**text** 型、**image** 型、および **xml** 型を除く T1 の列のすべての値が比較されます。 次に、**Name** 列が **nvarchar(40)** 型で、SELECT ステートメントから次の行セットが返されるとします。  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 AUTO モード ヒューリスティックにより、テーブル T1 のすべての値 (Id 列と Name 列) が比較されます。 最初の 2 行の Id 列と Name 列の値は同じなので、2 つの \<T2> 子要素を持っている 1 つの \<T1> 要素が結果に追加されます。  
  
 次に、返される XML を示します。  
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 ここで、Name 列は **text** 型であるとします。 この型の値は、AUTO モード ヒューリスティックによって比較されません。 この場合、値が異なると想定されます。 この結果、次に示すように XML が生成されます。  
  
```  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>参照  
 [FOR XML での AUTO モードの使用](use-auto-mode-with-for-xml.md)  
  
  
