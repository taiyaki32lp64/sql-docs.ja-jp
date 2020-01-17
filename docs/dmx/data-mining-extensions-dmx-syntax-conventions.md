---
title: データ マイニング拡張機能 (DMX) 構文表記規則 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a260598d62a3c5fc1304e8b71b8631546731ed07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070874"
---
# <a name="data-mining-extensions-dmx-syntax-conventions"></a>データ マイニング拡張機能 (DMX) 構文表記規則
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データ マイニング拡張機能 (DMX) リファレンス ドキュメントを[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] DMX 言語を記述する次の規則を使用します。  
  
|表記|使用方法|  
|----------------|-----------|  
|**太字**|DMX のキーワードおよびテキストを正確に示すように入力する必要があります。|  
|*斜体*|ユーザーが指定する DMX 構文の引数を示します。|  
|&#124; (縦棒)|角かっこまたは中かっこで囲まれた項目を区切るために使用します。 選択できる項目は 1 つだけです。|  
|`[ ]` (角かっこ)|省略可能な構文項目を含めることができます。 角かっこは入力しません。|  
|{} (中かっこ)|必要な構文項目を含めることができます。 中かっこは入力しません。|  
|, ...|コンマは前に、の項目が何回でも繰り返されることを示します。 項目は、コンマで区切られます。|  
|\<label> ::=|構文のブロックの名前を示します。 この表記規則は、1 つのステートメント内の複数の箇所で使用できる長い構文の一部、または構文の 1 単位について、グループ化してラベルを付ける際に使用します。 構文のブロックを使用できる各場所など、不等号で囲まれたラベルで示されます\<ラベル >。|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)  
  
  

