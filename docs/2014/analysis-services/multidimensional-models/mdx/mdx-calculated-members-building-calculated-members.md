---
title: Mdx (MDX) 計算されるメンバーの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0275a071c5548de7086844e48cec7eff3bb72d31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074539"
---
# <a name="building-calculated-members-in-mdx-mdx"></a>MDX での計算されるメンバーの作成 (MDX)
  多次元式 (MDX) では、値を返す MDX 式の計算によって解決されるメンバーのことを、計算されるメンバーといいます。 これは一見なにげない定義ですが、非常に広範囲に影響を及ぼします。 MDX クエリで計算されるメンバーを作成して使用する機能によって、多次元データの操作能力が大幅に向上するからです。  
  
 計算されるメンバーは、階層内のどこにでも作成できます。 また、キューブ内の既存のメンバーだけでなく、同じ MDX 式で定義された他の計算されるメンバーにも依存するように、計算されるメンバーを作成することもできます。  
  
 計算されるメンバーの定義では、以下のいずれかのコンテキストを設定できます。  
  
-   **クエリ スコープ** MDX クエリの一部として定義する、計算されるメンバーを作成する場合 (スコープをそのクエリに限定する場合) は、WITH キーワードを使用します。 その計算されるメンバーは、MDX の SELECT ステートメントの中で使用できます。 この方法では、WITH キーワードを使用して作成した計算されるメンバーを、SELECT ステートメントを修正せずに変更できます。  
  
     WITH キーワードを使用して計算されるメンバーを作成する方法の詳細については、「[クエリ スコープの計算されるメンバーの作成 &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md)」を参照してください。  
  
-   **セッション スコープ** クエリのコンテキストよりも広いスコープを設定して計算されるメンバーを作成する場合 (スコープを MDX セッションの有効期間全体とする場合) は、CREATE MEMBER ステートメントを使用します。 CREATE MEMBER ステートメントで定義した計算されるメンバーは、そのセッションのすべての MDX クエリで使用できます。 CREATE MEMBER ステートメントを使用する方法は、たとえば、さまざまなクエリで同じセットを使い回すクライアント アプリケーションで役立ちます。  
  
     CREATE MEMBER ステートメントを使用してセッションでの計算されるメンバーを作成する方法の詳細については、「[セッション スコープの計算されるメンバーの作成 &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE MEMBER ステートメント &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [MDX 関数リファレンス &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT ステートメント &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
