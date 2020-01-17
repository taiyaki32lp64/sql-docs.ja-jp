---
title: ディメンション、階層、およびレベル関数を使用して |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097184"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>ディメンション関数、階層関数、およびレベル関数の使用


  ディメンション関数、階層関数、およびレベル関数は、Analysis Services で検出された多次元階層をスキャンする際に役立ちます。 通常は、ディメンション、階層、またはレベルのメンバーに関する情報を得るために、これらの関数を他の関数と共に使用します。  
  
 次の例を使用する方法を示しています、 **.Dimension** 、 **.Hierarchy** 、および **.Level** 関数。  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [Dimension&#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [Functions&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [Hierarchy&#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Level&#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
