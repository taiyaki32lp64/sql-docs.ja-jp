---
title: クエリ軸とスライサー軸 (MDX) によるクエリの制限 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3290bc5892280cda5e8042de79ff581b305e8ec3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074040"
---
# <a name="restricting-the-query-with-query-and-slicer-axes-mdx"></a>クエリ軸とスライサー軸によるクエリの制限 (MDX)
  多次元式 (MDX) の SELECT ステートメントを作成する場合、アプリケーションでは通常、キューブを調べ、階層のセットを以下の 2 つのサブセットに分けます。  
  
-   **クエリ軸**-複数のメンバーのデータの取得元の階層のセット。 クエリ軸の詳細については、「[クエリ軸の内容の指定 &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)」を参照してください。  
  
-   **スライサー軸**-単一のメンバーのデータの取得元の階層のセット。 スライサー軸の詳細については、「[スライサー軸の内容の指定 &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)」を参照してください。  
  
 クエリ軸とスライサー軸は、クエリの実行対象であるキューブの複数の階層で構成できるため、これらの用語によって、クエリの実行対象であるキューブで使用される階層と、MDX クエリで返されたキューブで作成される階層とを区別しています。  
  
 クエリ軸のスライサー軸を使用する単純な例については、「[Using Query and Slicer Axes in a Simple Example &#40;MDX&#41;](mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md)」(クエリ軸とスライサー軸を使用する簡単な例) を参照してください。  
  
## <a name="see-also"></a>参照  
 [メンバー、組、およびセットの操作 &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [MDX クエリの基礎 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
