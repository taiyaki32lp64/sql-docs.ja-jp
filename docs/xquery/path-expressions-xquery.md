---
title: パス式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 9be2fb8752f27164e0e6dbc59e499f4b048d8979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946392"
---
# <a name="path-expressions-xquery"></a>パス式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery パス式では、ドキュメントの要素、属性、およびテキスト ノードなど、ノードを見つけます。 パス式の結果は常に、結果シーケンス内でノードが重複することなく、ドキュメント順で生成されます。 パスを指定するのには、省略と省略しない構文を使用できます。 以下の説明では、主に省略しない構文を取り上げます。 省略構文については、このトピックの後半で説明します。  
  
> [!NOTE]  
>  に対してこのトピックのサンプル クエリを指定するため、 **xml**種類の列、 **CatalogDescription**と**指示**の**ProductModel**テーブルが理解しておく内容とこれらの列に格納された XML ドキュメントの構造を使用します。  
  
 相対パスまたは絶対パス式ができます。 これらの両方の説明を次に示します。  
  
-   1 つまたは 2 つのスラッシュ記号で区切られた 1 つまたは複数のステップの相対パス式から成る (/または//)。 たとえば、`child::Features`は相対パス式では、場所`Child`コンテキスト ノードの子ノードのみを参照します。 これは、現在処理されているノードです。 式を取得、\<機能 > コンテキスト ノードの子要素ノード。  
  
-   絶対パス式が 1 つまたは 2 つのスラッシュ記号で始まる (/または//)、その後に、必要に応じて相対パス。 たとえば、式 `/child::ProductDescription` の先頭のスラッシュ記号は、この式が絶対パス式であることを示しています。 式の先頭のスラッシュ記号は、コンテキスト ノードのドキュメントのルート ノードを返すため、すべてを返します、式、 \<ProductDescription > ドキュメントのルートの子要素ノード。  
  
     絶対パスが 1 つのスラッシュ記号で始まる場合は可能性があります。 または相対パスによって従わないことがあります。 1 つのスラッシュ記号のみを指定すると、式はコンテキスト ノードのルート ノードを返します。 XML データ型の場合、これはドキュメント ノードになります。  
  
 パス式は、通常、ステップで構成されます。 たとえば、絶対パス式`/child::ProductDescription/child::Summary`、スラッシュ記号で区切られた 2 つの手順が含まれています。  
  
-   最初の手順の取得、 \<ProductDescription > ドキュメントのルートの子要素ノード。  
  
-   2 番目の手順の取得、\<概要 > 要素ノードの取得された各子\<ProductDescription > 要素ノードは、コンテキスト ノードになります。  
  
 パス式のステップには、軸ステップまたは汎用ステップを指定できます。  
  
## <a name="axis-step"></a>軸ステップ  
 パス式の軸ステップは、次の部分です。  
  
 [axis](../xquery/path-expressions-specifying-axis.md)  
 移動の方向を定義します。 これらは軸で指定した方向で到達可能なノードにコンテキスト ノードから開始し、移動するパス式での軸ステップ。  
  
 [ノード テスト](../xquery/path-expressions-specifying-node-test.md)  
 選択するノードの型またはノード名を指定します。  
  
 0 個以上の省略可能な述語  
 いくつかを選択して、他のユーザーの破棄によって、ノードをフィルター処理します。  
  
 次の例を使用して、 **axisstep**パス式で。  
  
-   絶対パス式`/child::ProductDescription`、1 つのステップが含まれています。 これは、軸 (`child`) とノード テスト (`ProductDescription`) を指定しています。  
  
-   相対パス式 `child::ProductDescription/child::Features` には、1 つのスラッシュ記号で区切られた 2 つのステップがあります。 両方の手順では、child 軸を指定します。 ProductDescription と Features はノード テストです。  
  
-   相対パス式では、 `child::root/child::Location[attribute::LocationID=10]`、スラッシュ記号で区切られた 2 つの手順が含まれています。 最初の手順を軸を指定します (`child`) とノード テスト (`root`)。 2 番目のステップは、軸ステップの 3 種類のコンポーネントをすべて指定しています。つまり、軸 (child)、ノード テスト (`Location`)、および述語 (`[attribute::LocationID=10]`) です。  
  
 軸ステップの詳細については、コンポーネントは、次を参照してください[パス式のステップで軸を指定する](../xquery/path-expressions-specifying-axis.md)、[パス式のステップでノード テストを指定する](../xquery/path-expressions-specifying-node-test.md)、および[で述語の指定、。パス式のステップ](../xquery/path-expressions-specifying-predicates.md)します。  
  
## <a name="general-step"></a>一般的な手順  
 汎用ステップは、評価結果がノードのシーケンスになる必要のある式です。  
  
 SQL Server で実装された XQuery では、パス式の最初のステップとして汎用ステップをサポートします。 一般的な手順を使用するパス式の例を次に示します。  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Id 関数」を参照の詳細については[id 関数&#40;XQuery&#41;](../xquery/functions-on-sequences-id.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [パス式のステップで軸を指定します。](../xquery/path-expressions-specifying-axis.md)  
 パス式での軸ステップの操作について説明します。  
  
 [パス式のステップでノード テストの指定](../xquery/path-expressions-specifying-node-test.md)  
 パス式でノード テストを使用した作業をについて説明します。  
  
 [パス式のステップで述語の指定](../xquery/path-expressions-specifying-predicates.md)  
 パス式で述語の使い方について説明します。  
  
 [パス式での省略構文の使用](../xquery/path-expressions-using-abbreviated-syntax.md)  
 パス式での省略構文の使い方について説明します。  
  
  
