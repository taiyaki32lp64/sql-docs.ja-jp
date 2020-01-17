---
title: (ビジネス インテリジェンス ウィザード) の通貨換算の定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.existingscriptpage.f1
ms.assetid: 37dd65b7-9d8d-44ad-b316-96a92c622472
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b463363e2e239c348c626cf1ef1d61e621877814
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082148"
---
# <a name="define-currency-conversion-business-intelligence-wizard"></a>[通貨換算の定義] (ビジネス インテリジェンス ウィザード)
  **[通貨換算の定義]** ページを使用すると、ビジネス インテリジェンス ウィザードで生成された通貨変換機能を含む多次元式 (MDX) スクリプトを確認できます。 ウィザードによって生成された MDX スクリプトを使用して、以前にキューブの MDX スクリプトに定義された通貨変換機能を上書きしたり、追加したりできます。  
  
> [!NOTE]  
>  このページは、キューブの MDX スクリプトに 1 つ以上の通貨変換機能があらかじめ定義されていることが検出された場合にのみ表示されます。 キューブの MDX スクリプトでは、通貨変換は次のコメントで囲まれています。  
>   
>  `//<Currency conversion>`  
>   
>  `...`  
>   
>  `[MDX statements for the currency conversion]`  
>   
>  `...`  
>   
>  `//</Currency conversion>`  
>   
>  このコメントを変更または削除すると、以前に定義された通貨変換が検出できなくなる場合があります。  
  
## <a name="options"></a>および  
 **新しい通貨換算スクリプト**  
 現在のビジネス インテリジェンス ウィザードのセッションで生成された MDX スクリプトが表示されます。  
  
 **既存の通貨換算スクリプトを上書き**  
 選択すると、 **[既存の通貨換算スクリプト]** に表示されている MDX スクリプトを **[新しい通貨換算スクリプト]** に表示されている MDX スクリプトで上書きします。  
  
 **後に追加します。**  
 選択すると、 **[既存の通貨換算スクリプト]** に表示されている MDX スクリプトの末尾に、 **[新しい通貨換算スクリプト]** に表示されている MDX スクリプトを追加します。 追加されたスクリプトは、新しいセクションになります。  
  
 **既存の通貨換算スクリプト**  
 上書きまたは追加の対象となる、以前に定義された通貨換算機能が含まれた、既存の通貨換算スクリプトのセクションを選択します。  
  
## <a name="see-also"></a>参照  
 [ビジネス インテリジェンス ウィザードの F1 ヘルプ](business-intelligence-wizard-f1-help.md)   
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [ディメンション デザイナー &#40;Analysis Services - 多次元データ&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
