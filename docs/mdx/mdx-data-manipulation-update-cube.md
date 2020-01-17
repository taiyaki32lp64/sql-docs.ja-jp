---
title: UPDATE CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f52dd59b67b42ad430df9bb1e9d00dce7ad6d697
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003531"
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX データ操作 - UPDATE CUBE


  UPDATE CUBE ステートメントは、SUM 集計によって親に対して集計を行うキューブ内の任意のセルにデータを書き戻すために使用します。 詳細な説明と例では、このブログ投稿の割り当てについて」を参照してください。[Analysis Services (ブログ) での書き戻しアプリケーションの構築](https://go.microsoft.com/fwlink/?LinkId=394977)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブの名前を指定する有効な文字列です。  
  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
 *New_Value*  
 有効な数値式です。  
  
 *Weight_Expression*  
 0 ～ 1 の範囲の 10 進値を返す有効な多次元式 (MDX) 数値式です。  
  
## <a name="remarks"></a>コメント  
 キューブ内の指定されたリーフ セルまたは非リーフ セルの値を更新できます。指定された非リーフ セルの値を、それに依存するすべてのリーフ セルに割り当てることもできます。 組式で指定したセルは、多次元領域内の任意の有効なセルを指定できます (つまり、セルがリーフ セルにする)。 ただしでのセルは集計する必要があります、[Sum](../mdx/sum-mdx.md)集計関数と、セルの識別に使用される組の中の計算されるメンバーを含めないでください。  
  
 考える可能性がある、 **UPDATE CUBE**ステートメントは、一連の指定された合計にロール アップされるリーフと非リーフ セルに個々 のセルの書き戻し操作を自動的に生成するサブルーチンです。  
  
 割り当ての方法の説明を次に示します。  
  
 **USE_EQUAL_ALLOCATION:** 更新されるセルに貢献するすべてのリーフ セルには、次の式に基づく同じの値が割り当てられます。  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** 更新されるセルに貢献するすべてのリーフ セルは、次の式に基づいて変更されます。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** 更新されるセルに貢献するすべてのリーフ セルには、次の式に基づく同じ値が割り当てられます。  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** 更新されるセルに貢献するすべてのリーフ セルは、次の式に基づいて変更されます。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Weight_expression を指定しない場合、 **UPDATE CUBE**ステートメントは暗黙的に次の式を使用します。  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Weight_expression は、ゼロ (0) ~ 1 の 10 進値として表現されなければなりません。 この値には、割り当て対象となるリーフ セルに割り当てる値の比率を指定します。 クライアント アプリケーションのプログラマは、式の割り当て値とロールアップ集計値が等しくなるように式を作成する必要があります。  
  
> [!CAUTION]  
>  クライアント アプリケーションは、不正なロールアップ値、一貫性のないデータなど、予期しない結果を回避するには、同時にすべてのディメンションの割り当てを考慮してください。  
  
 各**UPDATE CUBE**トランザクションとしてのアトミックである割り当てを考慮する必要があります。 つまり、数式のエラーやセキュリティ違反など、何かの理由でいずれかの割り当て操作が失敗すると、UPDATE CUBE 操作全体が失敗します。 個々の割り当て操作の計算が処理される前に、データのスナップショットが作成され、計算結果が正しいかどうかの確認が行われます。  
  
> [!CAUTION]  
>  整数を含むメジャーで使用すると、USE_WEIGHTED_ALLOCATION メソッドは、増分変更に丸め不正確な結果を返すことができます。  
  
> [!IMPORTANT]  
>  更新されるセルが重ならない場合は、 **Update Isolation Level** 接続文字列プロパティを使用して、UPDATE CUBE のパフォーマンスを向上させることができます。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [MDX データ操作ステートメント&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
