---
title: 親子ディメンションのカスタム ロールアップ演算子 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 20f25474b15ecf58c45383a8290bb13f956a5db8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073463"
---
# <a name="custom-rollup-operators-in-parent-child-dimensions"></a>親子ディメンションのカスタム ロールアップ演算子
  カスタム ロールアップ演算子を使用すると、親子階層でメンバーの値を親の値にロール アップする方法を簡単に制御できます。 親子リレーションシップを含んでいるディメンションでは、親属性のすべての計算されないメンバーのロールアップを指定する単項演算子を含んでいる列を指定します。 単項演算子は、親メンバーの値が評価されるたびにメンバーに適用されます。  
  
 単項演算子は、親属性の `UnaryOperatorColumn` プロパティで定義した列に保存され、属性の各メンバーに適用されます。 このプロパティで指定する列は、ディメンション テーブルに存在するか、ディメンション テーブル内の外部キーによってそのディメンション テーブルに関連付けられているテーブルに存在する可能性があります。  
  
 カスタム ロールアップ演算子の機能は、カスタム メンバー式に似ていますが、それよりも簡単です。 カスタム メンバー式では、多次元式 (MDX) を使用して、メンバーのロール アップ方法を決定します。 これに対し、カスタム ロールアップ演算子では、単純な単項演算子を使用して、メンバーの値が親に与える影響を決定します。 ディメンション内の前のレベルのカスタム メンバー式は、レベルのカスタム ロールアップ演算子をオーバーライドします。  
  
## <a name="custom-rollup-precedence"></a>カスタム ロールアップの優先順位  
 優先順位の面では、階層内のレベルのソース属性のカスタム ロールアップ演算子は、前のレベルのカスタム メンバー式をオーバーライドします。 ただし、前のレベルのカスタムメンバー式は、レベルのカスタム ロールアップ演算子をオーバーライドします。  
  
## <a name="see-also"></a>参照  
 [カスタム メンバー式の定義](attribute-properties-define-custom-member-formulas.md)   
 [親子ディメンションの単項演算子](parent-child-dimension-attributes-unary-operators.md)  
  
  
