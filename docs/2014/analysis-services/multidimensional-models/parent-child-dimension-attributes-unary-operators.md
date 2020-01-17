---
title: 親子ディメンションの単項演算子 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25c1acf7a1fadbc79b7781488143ce57881c81fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073445"
---
# <a name="unary-operators-in-parent-child-dimensions"></a>親子ディメンションの単項演算子
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の親子リレーションシップを含んでいるディメンションでは、親属性のすべての計算されないメンバーにカスタム ロールアップを指定する、単項 (またはカスタム ロールアップ) 演算子列を指定します。 単項演算子は、親メンバーの値が評価されるたびにメンバーに適用されます。 親属性 ( **Usage** =Parent) の**UnaryOperatorColumn**は、単項演算子を含んでいるテーブル列をデータ ソース ビューで指定します。 この列に格納されるカスタム ロールアップ演算子の値は、属性の各メンバーに適用されます。  
  
 データ ソース ビューでは、ディメンション テーブルの名前付き計算を作成し、単項演算子列として指定できます。 "+" などの単純な式は、すべてのメンバーに関して同じ演算子を返します。 ただし、すべてのメンバーに関して 1 つの演算子を返す式に限り、使用できます。  
  
 **UnaryOperatorColumn** プロパティの設定は親属性で手動で変更することも、ビジネス インテリジェンス ウィザードの [単項演算子の指定] 拡張機能を使用して、ディメンションのメンバーに関連付けられている既定の集計を置き換えることもできます。 ビジネス インテリジェンス ウィザードを使用してこの構成を実行する方法の詳細については、「 [ディメンションへのカスタム集計の追加](bi-wizard-add-a-custom-aggregation-to-a-dimension.md)」をご覧ください。  
  
 親属性の **UnaryOperatorColumn** プロパティに対する既定の設定は (none) で、カスタム ロールアップ演算子を無効にします。 次の表は、単項演算子と、レベルに適用された場合の動作を示しています。  
  
|単項演算子|説明|  
|--------------------|-----------------|  
|+ (正符号)|メンバーの値は、そのメンバーの前に出現した兄弟メンバーの集計値に加算されます。 これは、単項演算子列が属性に対して定義されていない場合の既定の演算子です。|  
|-(マイナス記号)|メンバーの値は、そのメンバーの前に出現した兄弟メンバーの集計値から減算されます。|  
|* (アスタリスク)|メンバーの値は、そのメンバーの前に出現した兄弟メンバーの集計値で乗算されます。|  
|/ (スラッシュ)|メンバーの値は、そのメンバーの前に出現した兄弟メンバーの集計値で除算されます。|  
|~ (チルダ)|メンバーの値は無視されます。|  
  
 空白の値や、テーブル内で見つからないその他の値は、正符号 (+) 単項演算子と同様に扱われます。 演算子には優先順位がないため、単項演算子列に格納されたメンバーの順序により評価の順序が決定されます。 評価の順序を変更するには、新しい属性を作成し、その **Type** プロパティを **Sequence**に設定し、評価順序に対応するシーケンス番号を **Source Column** プロパティで割り当てます。 また、その属性に基づいて属性のメンバーの順序を指定する必要もあります。 ビジネス インテリジェンス ウィザードを使用して属性のメンバーの順序を指定する方法の詳細については、「 [ディメンションの順序の定義](bi-wizard-define-the-ordering-for-a-dimension.md)」をご覧ください。  
  
 **UnaryOperatorColumn** プロパティを使用すると、単項演算子を返す名前付き計算を属性の全メンバーのリテラル文字として指定できます。 これは、名前付き計算で `'*'` などのリテラル文字を入力するだけで指定できる場合もあります。 この場合は、属性のすべてのメンバーについて、既定の演算子の正符号 (+) が乗算演算子のアスタリスク (*) で置換されます。 詳細については、「[データ ソース ビューでの名前付き計算の定義 &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)」をご覧ください。  
  
 ディメンション デザイナーの **[ブラウザー]** タブでは、階層内の各メンバーの隣に単項演算子を表示できます。 書き込み許可ディメンションを使用する場合は、単項演算子を変更することもできます。 ディメンションが書き込み可能でない場合は、データ ソースを直接変更するためのツールを使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)   
 [親子ディメンションのカスタム ロールアップ演算子](parent-child-dimension-attributes-custom-rollup-operators.md)   
 [ディメンション デザイナーでのビジネス インテリジェンス ウィザードの起動](database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
