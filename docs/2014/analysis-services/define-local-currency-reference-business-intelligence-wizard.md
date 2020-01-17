---
title: 定義の現地の通貨参照 (ビジネス インテリジェンス ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 558e2c7d62edcb9fb314b49d41fd7bd15413218d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082176"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>現地の通貨参照の定義 (ビジネス インテリジェンス ウィザード)
  **[現地の通貨参照の定義]** ページを使用すると、 **[換算の種類の選択]** ページで指定された多対多または多対一の変換を実行する通貨の換算機能のための現地通貨を定義できます。 現地通貨とは、 **[メジャーの選択]** ページで選択されたメジャーのトランザクションが保存される通貨です。  
  
> [!NOTE]  
>  ビジネス インテリジェンス ウィザードをディメンション デザイナーから起動した場合や、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] のソリューション エクスプローラーでディメンションを右クリックして起動した場合、このページは表示されません。 また、このページは、 **[換算の種類の選択]** ページで **[一対多]** を選択した場合にも表示されません。  
  
## <a name="options"></a>および  
 **ファクト テーブルの識別子**  
 選択すると、 **[メジャーの選択]** ページで選択されたメジャーを格納するファクト テーブルから参照される、通貨ディメンションの現地通貨の通貨識別子を表す属性を指定できます (のいずれかでディメンションを通貨`Type`プロパティに設定されて*通貨*)。  
  
 このオプションは、トランザクションでそのトランザクション自体の現地通貨を決定する場合に使用します。 たとえば、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]サンプル データベース-[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]、Internet Sales メジャー グループが、通貨ディメンションに対する通常のディメンション リレーションシップ。 このメジャー グループのファクト テーブルは、このディメンションのディメンション テーブル内の通貨識別子を参照する外部キー列を格納します。  
  
 **通貨ディメンションとファクト データによって参照される属性**  
 通貨ディメンションのメンバーが現地通貨の通貨識別子を表す、その通貨ディメンション内の通貨属性を選択します。 (通貨属性が 1 つ持つ`Type`プロパティに設定されて*通貨*)。  
  
> [!NOTE]  
>  **[ファクト テーブルの識別子]** オプションが選択されていない場合は、このオプションを利用できません。  
  
 **ディメンション テーブルの属性**  
 選択すると、現地通貨の通貨識別子を格納するメジャー グループに関連したディメンションから属性を指定できます。  
  
 このオプションは、トランザクションと他のビジネス エンティティ (たとえば場所) とのリレーションシップによって、そのトランザクションの現地通貨が決定される場合に使用します。 たとえば、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]サンプル データベースの[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]、Financial Reporting メジャー グループが、組織ディメンションを介して、通貨ディメンションに対する参照ディメンション リレーションシップ。 つまり、[Financial Reporting] メジャー グループのファクト テーブルには、組織ディメンションのディメンション テーブル内のメンバーを参照する外部キー列があります。 さらに、組織ディメンションのディメンション テーブルには、通貨ディメンションのディメンション テーブル内の通貨識別子を参照する外部キー列があります。  
  
 **通貨を参照するディメンションの属性**  
 ディメンションのメンバーが現地通貨の通貨識別子を参照する、そのディメンション内の属性を選択します。  
  
> [!NOTE]  
>  **[ディメンション テーブルの属性]** オプションが選択されていない場合は、このオプションを利用できません。  
  
## <a name="see-also"></a>参照  
 [ビジネス インテリジェンス ウィザードの F1 ヘルプ](business-intelligence-wizard-f1-help.md)   
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [ディメンション デザイナー &#40;Analysis Services - 多次元データ&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
