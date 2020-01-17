---
title: 式の優先順位制約を追加する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 68455f23f5d05895af8f0cfb4d7b1e12e3d65b16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061902"
---
# <a name="add-expressions-to-precedence-constraints"></a>優先順位制約に式を追加する
  優先順位制約では、優先順位付き実行可能ファイルと、制約付き実行可能ファイルの 2 つの実行可能ファイル間の制約を定義するために、式を使用できます。 これらの実行可能ファイルには、タスクまたはコンテナーを設定できます。 式は単独で使用することも、優先順位付き実行可能ファイルの実行結果と組み合わせて使用することもできます。 実行可能ファイルの実行結果は、成功または失敗のどちらかです。 優先順位制約の実行結果を構成する場合、実行結果を `Success`、`Failure`、または `Completion` に設定できます。 `Success` に設定した場合、優先順位付き実行可能ファイルは成功する必要があります。`Failure` に設定した場合、優先順位付き実行可能ファイルは失敗する必要があります。`Completion` は、優先順位付きタスクの成功または失敗にかかわらず、制約つき実行可能ファイルが実行されることを示します。 優先順位制約の詳細については、「 [優先順位制約](control-flow/precedence-constraints.md)」を参照してください。  
  
 式は `True` または `False` に評価される、有効な [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 式である必要があります。 式では、リテラル、システム変数とカスタム変数、および [!INCLUDE[ssIS](../includes/ssis-md.md)] の式文法で用意されている関数と演算子を使用できます。 たとえば、式 `@Count == SQRT(144) + 10` では、変数 `Count`、SQRT 関数、等号 (==) 演算子、および加算 (+) 演算子が使用されています。 詳細については、「 [Integration Services (SSIS) 式](expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
 次の図では、実行結果と式を使用する優先順位制約によって、タスク A とタスク B がリンクされています。 制約値は `Success` に設定され、式は `@X >== @Z` です。 タスク B は制約付きタスクで、タスク A が正常に完了し、変数 `X` の値が変数 `Z` の値以上の場合にのみ実行されます。  
  
 ![2 つのタスク間の優先順位制約](media/mw-dts-03.gif "2 つのタスク間の優先順位制約")  
  
 異なる式が含まれる複数の優先順位制約を使用して、実行ファイルをリンクすることもできます。 たとえば、次の図では、実行結果と式を使用する優先順位制約によって、タスク B およびタスク C がタスク A にリンクされています。 制約値は両方とも `Success.` に設定されています。1 つの優先順位制約には式 `@X >== @Z` が含まれ、もう 1 つの優先順位制約には式 `@X < @Z` が含まれています。 変数 `X` と変数 `Z` の値に応じて、タスク C とタスク B のどちらかが実行されます。  
  
 ![優先順位制約の式](media/mw-dts-04.gif "優先順位制約の式")  
  
 式を追加または変更するには、 **デザイナーの** [優先順位制約エディター] [!INCLUDE[ssIS](../includes/ssis-md.md)] と [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で用意されている [プロパティ] ウィンドウを使用します。 ただし、[プロパティ] ウィンドウには、式の構文を検証する機能は用意されていません。  
  
 優先順位制約に式が含まれる場合、 **[制御フロー]** タブのデザイン画面で、優先順位制約の隣にアイコンが表示され、アイコン上のツールヒントには式が表示されます。  
  
## <a name="combining-execution-values-and-expressions"></a>実行値と式の結合  
 次の表では、実行値制約と優先順位制約の式を結合した場合の結果について説明します。  
  
|[評価操作]|制約の評価|式の評価|制約付き実行可能ファイルの実行|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|制約|True|なし|True|  
|制約|False|なし|False|  
|式|なし|True|True|  
|式|なし|False|False|  
|制約と式の両方|True|True|True|  
|制約と式の両方|True|False|False|  
|制約と式の両方|False|True|False|  
|制約と式の両方|False|False|False|  
|制約または式のいずれか|True|True|True|  
|制約または式のいずれか|True|False|True|  
|制約または式のいずれか|False|True|True|  
|制約または式のいずれか|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>優先順位制約に式を追加するには  
  
-   [優先順位制約で式を使用する](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [優先順位制約のプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>外部リソース  
 social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
## <a name="see-also"></a>関連項目  
 [複数の優先順位制約](../../2014/integration-services/multiple-precedence-constraints.md)   
 [優先順位制約](control-flow/precedence-constraints.md)  
  
  
