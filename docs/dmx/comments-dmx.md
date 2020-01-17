---
title: コメント (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 26a529d6eb15997ccb48ad25d8d4fcb11cd2ddfb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071051"
---
# <a name="comments-dmx"></a>コメント (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データ マイニング拡張機能 (DMX) でのコメントは、プログラム内のテキスト文字列のコードを[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]は実行されません。 コメントは解説とも呼ばれています。 コメントを使用すると、コードの説明を記述したり、コードの診断の際に DMX ステートメントまたはスクリプトの一部分を一時的に無効化することができます。  
  
 コメントを使用してプログラム コードの説明を記述しておくと、後でコードの維持を簡単に行うことができます。 コメントを使用して、プログラムの名前、コードを作成した開発者の名前、および主なコード変更の日付などの詳細を記録することができます。 また、複雑な計算の説明やプログラム方法の説明を記述することもできます。  
  
 コメントを記述する際の基本的なガイドラインは次のとおりです。  
  
-   コメント内には、すべての英数字や記号を使用することができます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、コメント内の文字はすべて無視されます。  
  
-   ステートメント内またはスクリプト内のコメント長には制限がありません。 1 行または複数行のコメントを作成できます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 次の種類のコメント文字をサポートしています。  
  
-   **(二重スラッシュ)。** 実行するコードと同じ行にコメントを記述する、またはコメントのみの行にコメントを記述するには、このコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメントの一部として、行の末尾に二重スラッシュからすべてを評価します。 複数行にわたってコメントを記述する場合、すべてのコメント行の先頭に二重スラッシュを使用します。 このコメント文字の詳細については、次を参照してください。[二重スラッシュ&#40;コメント&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)します。  
  
-   **-(二重ハイフン)。** 実行するコードと同じ行にコメントを記述する、またはコメントのみの行にコメントを記述するには、このコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメントの一部として、行の末尾に二重ハイフンの後ろからすべてを評価します。 複数行にわたってコメントを記述する場合、すべてのコメント行の先頭に二重ハイフンを使用します。 このコメント文字の詳細については、次を参照してください。 [--&#40;コメント&#41; &#40;DMX&#41;概要](../dmx/comment-dmx-summary.md)します。  
  
-   **/\* ...\*/(スラッシュとアスタリスク文字のペア)。** 実行コードと同じ行にコメントを記述する、コメント専用の行にコメントを記述する、または実行可能コード内にコメントを記述するには、このコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメント開始記号からすべてを評価 (/*) にコメント終了記号 (\*/)、コメントの一部として。 複数行のコメントを作成するには、コメント文字のペアでコメントを開始 (/\*)、および閉じるコメント文字のペアでコメントの終了 (\*/)。 コメント行ではそれ以外のコメント文字は使用できません。 このコメント文字の詳細については、次を参照してください。[スラッシュ スター&#40;コメント&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
