---
title: MDX スクリプティングの基礎 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17cb2b326ed510a952249da6a73693b6be6ab252
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073863"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX スクリプティングの基礎 (Analysis Services)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の多次元式 (MDX) スクリプトは、計算結果をキューブに格納する 1 つまたは複数の MDX 式またはステートメントから構成されます。  
  
 MDX スクリプトはキューブの計算プロセスを定義します。 また、MDX スクリプト自体がキューブの一部分だと考えることもできます。 したがって、キューブに関連した MDX スクリプトの内容を変更すると、即座にキューブの計算プロセスが変更されることになります。  
  
 MDX スクリプトを生成するには、 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]でキューブ デザイナーを使用できます。 詳細については、「 [割り当てとその他のスクリプト コマンドの定義](../define-assignments-and-other-script-commands.md) 」および「 [Microsoft SQL Server 2005 の MDX スクリプトの紹介](https://go.microsoft.com/fwlink/?LinkId=81892)」を参照してください。  
  
 MDX クエリおよび計算に関するパフォーマンス問題については、「 [SQL Server Analysis Services パフォーマンス ガイド](https://go.microsoft.com/fwlink/p/?LinkId=399050)」の MDX 最適化のセクションを参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[基本的な MDX スクリプト &#40;MDX&#41;](the-basic-mdx-script-mdx.md)|MDX スクリプトの基礎を詳しく説明します。各キューブに付属している既定の MDX スクリプトについて、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のキューブ内で MDX スクリプトが一般的にどのように機能するかについての説明が含まれます。|  
|[スコープとコンテキストの管理 &#40;MDX&#41;](managing-scope-and-context-mdx.md)|MDX スクリプト内でコンテキストとスコープを管理するために [CALCULATE](/sql/mdx/mdx-scripting-calculate) ステートメント、 [SCOPE](/sql/mdx/mdx-scripting-scope) ステートメント、および [This](/sql/mdx/this-mdx) 関数を使用する方法について説明します。|  
|[変数とパラメーターの使用 &#40;MDX&#41;](using-variables-and-parameters-mdx.md)|MDX スクリプト内で変数やパラメーターを使用する方法について説明します。|  
|[エラー処理 &#40;MDX&#41;](error-handling-mdx.md)|MDX スクリプト内でのエラー処理について説明します。|  
|[サポートされる MDX &#40;MDX&#41;](supported-mdx-mdx.md)|MDX スクリプト内でサポートされる MDX 演算子、ステートメント、関数の一覧を示します。|  
  
## <a name="see-also"></a>参照  
 [MDX 言語リファレンス &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
