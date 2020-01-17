---
title: データの変更 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81d1df159944b96d0945bb45d2c331922d0f46e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074231"
---
# <a name="modifying-data-mdx"></a>データの変更 (MDX)
  多次元式 (MDX) は、ディメンションやキューブのデータの取得や操作を行うためだけでなく、ディメンションやキューブのデータの更新、つまり*書き戻し*を行うためにも使用できます。 これらの更新は、推測分析または "what-if" 分析の場合のように一時的なものであることも、データ分析に基づいて変更を加える必要がある場合のように永続的なものになることもあります。  
  
 データの更新は、ディメンション レベルまたはキューブ レベルで実行できます。  
  
 **ディメンションの書き戻し**  
 書き込み可能なディメンションのデータを変更するには、 [ALTER CUBE ステートメント (MDX)](/sql/mdx/mdx-data-definition-alter-cube) を使用します。属性値の削除、作成、更新を反映するには、 [REFRESH CUBE ステートメント (MDX)](/sql/mdx/mdx-data-definition-refresh-cube) を使用します。 ALTER CUBE ステートメントを使用すると、階層内のサブツリー全体を削除したり、削除されたメンバーの子を昇格させるなど、複雑な操作を実行することもできます。  
  
 **キューブの書き戻し**  
 書き込み可能なキューブに対する更新を実行するには、 [UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) ステートメントを使用します。 UPDATE CUBE ステートメントを使用すると、特定の値で組を更新できます。 サーバーにある更新されたデータをクライアント セッションのデータに適用するには、[REFRESH CUBE ステートメント (MDX)](/sql/mdx/mdx-data-definition-refresh-cube) を使用します。  
  
 詳細については、「[キューブの書き戻しの使用 (MDX)](mdx-data-modification-using-cube-writebacks.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [MDX クエリの基礎 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
