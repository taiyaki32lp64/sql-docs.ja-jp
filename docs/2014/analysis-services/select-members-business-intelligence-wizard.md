---
title: メンバー (ビジネス インテリジェンス ウィザード) を選択します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cc66896eb1735d09991644dd49c03b5a94c208d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069428"
---
# <a name="select-members-business-intelligence-wizard"></a>[メンバーの選択] (ビジネス インテリジェンス ウィザード)
  **[メンバーの選択]** ページを使用すると、ビジネス インテリジェンス ウィザードの **[通貨換算オプションの設定]** ページで指定された通貨換算機能を適用するメンバーを指定できます。  
  
> [!NOTE]  
>  ビジネス インテリジェンス ウィザードをディメンション デザイナーから起動した場合や、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]のソリューション エクスプローラーでディメンションを右クリックして起動した場合、このページは表示されません。  
  
## <a name="options"></a>および  
 **メジャー ディメンション**  
 選択すると、キューブ内の 1 つ以上のメジャーに通貨換算機能を適用します。  
  
 このオプションを選択すると、次の表に示すオプションがグリッドに表示されます。  
  
|オプション|説明|  
|------------|-----------------|  
|**ビルトイン メジャーの種類**|選択すると、指定したメジャーに通貨換算機能を含めます。|  
|**メジャー**|レート メジャー グループから、 **[ビルトイン メジャーの種類]** で選択したメジャーを変換するときに使用する、換算レートを含むメジャーを選択します。|  
  
 **勘定科目の階層**  
 選択すると、キューブに含まれている勘定科目ディメンションの、勘定科目の階層のメンバーに通貨換算機能を適用します。 勘定科目の階層は、アカウント内の階層がディメンションの`Type`プロパティに設定されて*アカウント*します。  
  
 このオプションを選択すると、次の表に示すオプションがグリッドに表示されます。  
  
|オプション|説明|  
|------------|-----------------|  
|**勘定科目メンバー**|選択すると、勘定科目の階層の指定したメンバーに通貨換算機能を含めます。|  
|**メジャー**|レート メジャー グループから、 **[勘定科目メンバー]** で選択したメンバーのメジャーを変換するときに使用する、換算レートを含むメジャーを選択します。|  
  
 **勘定科目の階層の種類に基づく**  
 選択すると、`Type` プロパティが指定した種類の勘定科目に設定されている勘定科目の階層の属性の全メンバーに、通貨換算機能が適用されます。  
  
 このオプションを選択すると、次の表に示すオプションがグリッドに表示されます。  
  
|オプション|説明|  
|------------|-----------------|  
|**アカウントの種類**|選択すると、指定した種類の勘定科目に通貨換算機能を含めます。|  
|**メジャー**|レート メジャー グループから、 **[勘定科目の種類]** で選択した種類の勘定科目を使用して、属性のメンバーのメジャーを変換するときに使用する、換算レートを含むメジャーを選択します。|  
  
## <a name="see-also"></a>参照  
 [ビジネス インテリジェンス ウィザードの F1 ヘルプ](business-intelligence-wizard-f1-help.md)   
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [ディメンション デザイナー &#40;Analysis Services - 多次元データ&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
