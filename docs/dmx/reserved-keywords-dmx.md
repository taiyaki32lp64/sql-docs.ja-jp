---
title: 予約済みキーワード (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa17a4fb673ad6508fbfc70d5bab39e398d6c3aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928454"
---
# <a name="reserved-keywords-dmx"></a>予約されているキーワード (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] 特定のキーワードを排他的に使用を予約します。 これらのキーワードを任意の場所を除く、位置でのデータ マイニング拡張機能 (DMX) ステートメントで使用できませんを[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]DMX 言語リファレンスで定義します。 これらの制限された DMX キーワードには次のメンバーがあります。  
  
-   すべてのデータ定義ステートメント、トピックに記載[DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)します。  
  
-   すべてのデータ マイニング クエリ関数が、トピックに記載[DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)します。  
  
-   すべての演算子、トピックに記載[DMX 演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)します。  
  
-   多次元式 (MDX) クエリ言語で定義され、DMX ステートメントの一部として含まれているキーワード  
  
-   OLE DB for Data Mining 仕様で定義され、DMX ステートメントの一部として含まれているキーワード  
  
 データベースのオブジェクトに名前を付ける場合、予約されたキーワードを使用しない名前付け規則の使用を推奨します。  
  
 データベースに予約されたキーワードと一致する名前が含まれている場合、これらのオブジェクトを参照するときに区切られた識別子を使用する必要があります。 詳細については、次を参照してください。[識別子&#40;DMX&#41;](../dmx/identifiers-dmx.md)します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
