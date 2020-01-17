---
title: 演算子 (MDX 構文) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5067793ae0f5533a889973e18f7b300914df9092
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892113"
---
# <a name="operators-mdx-syntax"></a>演算子 (MDX 構文)


  多次元式 (MDX) では、演算子を使用して以下の操作を実行できます。  
  
-   永続的または一時的なデータ変更  
  
-   指定した条件を満たしている値またはオブジェクトの検索  
  
-   値の間または式の間での判断  
  
-   トランザクションの開始やコミット、または特定のステートメントの実行の前に行う特定の条件に対する試験  
  
 MDX では、以下の表に示す演算子がサポートされます。  
  
|演算の種類|新しく使用する機能|  
|---------------------------------------|---------|  
|変数に値を代入するかまたは結果セット列を別名に関連付けます。|[代入演算子](../mdx/assignment-operators.md)|  
|加算、減算、乗算、除算。|[算術演算子](../mdx/arithmetic-operators.md)|  
|AND、OR、NOT、XOR などの条件が真かどうか調べます。|[ビット処理演算子](../mdx/bitwise-operators.md)|  
|値を他の値または式と比較します。|[比較演算子](../mdx/comparison-operators.md)|  
|2 つの文字列を永続的または一時的に 1 つの文字列に結合します。|[連結演算子](../mdx/concatenation-operators.md)|  
|2 つのセット式を永続的または一時的に 1 つのセットに結合します。|[セット演算子](../mdx/set-operators.md)|  
|1 つのオペランドに対して 1 つの演算を行います。|[単項演算子](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  クエリ内では、特定の種類の演算子と共に使用するキューブのデータを読み取ることができるユーザーは演算を実行できます。 ただし、データを変更するには適切な権限が必要です。  
  
 複数の演算子を使用する場合、MDX によって演算子が評価される順序は重要です。 同様に重要な点として、演算子を評価する前に、あるデータ型を別のデータ型に変換しておかなければならない場合もあります。  
  
## <a name="evaluating-complex-expressions"></a>複雑な式の評価  
 演算子を使用すると、複数の小さい式を結合して 1 つの式を作成できます。 これらの複雑な式では、によって使用される演算子の優先順位の定義[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]に基づいて、MDX によって演算子が評価されます。 MDX は、優先順位の高い演算子を、優先順位の低い演算子より先に実行します。  
  
### <a name="understanding-operator-precedence"></a>演算子の優先順位について  
 以下の一覧に、演算子を優先順位の高いものから順に示します。 同じ行に示されている演算子は優先順位が同じです。かっこによる強制的な優先がない限り、左から右の順に評価されます。  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   AND  
  
-   XOR  
  
-   OR  
  
 MDX の演算子の詳細については、「mdx [ &#40;演算子&#41;リファレンス mdx](../mdx/mdx-operator-reference-mdx.md)」を参照してください。  
  
### <a name="determining-results"></a>結果の決定  
 単純な式を結合して複雑な式を作成する場合、演算子に関する規則とデータ型の優先順位に関する規則の組み合わせによって、結果の値のデータ型が決まります。  
  
 結果が文字値または Unicode 値の場合、演算子に関する規則と照合順序の優先順位に関する規則の組み合わせによって、結果の照合順序が決まります。 照合順序の詳細については、「[言語と照合&#40;順序 Analysis Services&#41;](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services)」を参照してください。  
  
 単純式の有効桁数、小数点以下桁数、長さに基づいて結果の有効桁数、小数点以下桁数、長さを指定するルールもあります。  
  
## <a name="converting-data-types"></a>データ型の変換  
 MDX では、あるオブジェクトが別のデータ型を必要とする式の中で使用されている場合、そのオブジェクトを別のデータ型へ暗黙的に変換します。 各オブジェクトは、次の表に示す規則に従って変換されます。  
  
|元の型|必要な型|変換|  
|-------------------|-----------------|----------------|  
|Level|Set|\<Level>.members|  
|Hieararchy|Member|\<hierarchy > .defaultmember|  
|Member|Tuple|(\<Member)|  
|Tuple|Member|\<Tuple > .item(0)|  
|Tuple|Scalar|\<tuple > .value|  
  
## <a name="see-also"></a>参照  
 [MDX 演算子リファレンス&#40;mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Mdx 構文要素&#40;mdx&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
