---
title: カスタム メンバー式の定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- members [Analysis Services], custom
- custom rollup formulas [Analysis Services]
- MDX [Analysis Services], custom rollup formulas
- custom member formulas [Analysis Services]
ms.assetid: 258304e2-d900-4013-97e3-871f51dfdce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 969a8f11926957ae19512e92b68e02d12011dd03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077281"
---
# <a name="define-custom-member-formulas"></a>カスタム メンバー式の定義
  カスタム メンバー式と呼ばれる多次元式 (MDX) を定義すると、指定した属性のメンバーに値を指定できます。 データ ソース ビューからのテーブルの列は、属性のメンバーごとに、そのメンバーの値の指定に使用される式を提供します。  
  
 カスタム メンバー式により、メンバーに関連付けられたセル値が判別され、メジャーの集計関数がオーバーライドされます。 カスタム メンバー式は、MDX で記述します。 各カスタム メンバー式は、1 つのメンバーに適用されます。 カスタム メンバー式は、ディメンション テーブルまたはディメンション テーブルとの外部キー リレーションシップを持つ別のテーブルに格納されます。  
  
 属性の `CustomRollupColumn` プロパティは、属性のメンバーのカスタム メンバー式が含まれている列を指定します。 列の行が空の場合は、メンバーのセル値は通常どおり返されます。 列の式が有効でない場合は、メンバーを使用するセル値が取得されるたびに実行時エラーが発生します。  
  
 属性のカスタム メンバー式を指定する前に、属性が含まれているディメンション テーブル、つまり直接関連するテーブルに、カスタム メンバー式を保存するための文字列型の列があることを確認してください。 大文字と小文字の場合は、設定ができます、`CustomRollupColumn`プロパティ属性を手動でまたはビジネス インテリジェンス ウィザードのカスタム メンバー式の設定の拡張機能を使用して、属性にカスタム メンバー式を有効にします。 この拡張機能の使用方法については、「 [ディメンションの属性に対するカスタム メンバー式の設定](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)」を参照してください。  
  
## <a name="evaluating-custom-member-formulas"></a>カスタム メンバー式の評価  
 カスタム メンバー式は、計算されるメンバーとは異なります。 カスタム メンバー式は、ディメンション テーブルに存在しているメンバーに適用され、メンバーの値のみを提供します。 これに対して、計算されるメンバーはディメンション テーブルに格納されず、ディメンションまたは階層に含まれている他のメンバーのデータとメタデータの両方を定義します。  
  
 カスタム メンバー式は、メジャーに関連付けられている集計関数をオーバーライドします。 たとえば、カスタム メンバー式を指定する前に、時間ディメンションの以下のメンバーについて、`Sum` 集計関数を使用するメジャーが次の値であるとします。  
  
-   2003:2100  
  
    -   第 1 四半期700  
  
    -   第 2 四半期500  
  
    -   第 3 四半期100  
  
    -   第 4 四半期800  
  
-   2004:1500  
  
    -   第 1 四半期600  
  
    -   第 2 四半期200  
  
    -   第 3 四半期300  
  
    -   第 4 四半期400  
  
 カスタム メンバー式を使用すると、メンバーの値は代わりにカスタム ロールアップ式によって指定されます。 たとえば、次のカスタム メンバー式を使用すると、時間ディメンションの 2004 メンバーの Quarter 4 子メンバーの値を 450 に指定できます。  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 カスタム メンバー式は、ディメンション テーブルの列に格納されます。 属性の `CustomRollupColumn` プロパティを設定して、カスタム ロールアップ式を有効にします。  
  
 1 つの MDX 式を属性のすべてのメンバーに適用するには、MDX 式をリテラル文字列として返すディメンション テーブルで名前付き計算を作成します。 次に、名前付き計算を、構成する属性の `CustomRollupColumn` プロパティ設定で指定します。 名前付き計算は、SQL 式によって定義される行の値を返す、データ ソース ビュー テーブルの列です。 名前付き計算の構築方法については、「[データ ソース ビューでの名前付き計算の定義 (Analysis Services)](define-named-calculations-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
> [!NOTE]  
>  特定の属性に基づいているすべてのレベルのメンバーではなく、特定のレベルのメンバーに MDX 式を適用するには、レベルの MDX スクリプトとして式を定義できます。 詳細については、「[MDX スクリプティングの基礎 (Analysis Services)](mdx/mdx-scripting-fundamentals-analysis-services.md)」を参照してください。  
  
 計算されるメンバーと属性のメンバーのカスタム ロールアップ式の両方を使用する場合は、評価の順序に注意してください。 計算されるメンバーは、カスタム ロールアップ式が解決される前に解決されます。  
  
## <a name="see-also"></a>参照  
 [属性と属性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [ディメンションの属性に対するカスタム メンバー式の設定](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
