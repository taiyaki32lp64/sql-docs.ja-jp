---
title: 指定のディメンションの種類 (ディメンション ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de1b056942673d358cec4768c6854a6966d139e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068373"
---
# <a name="specify-dimension-type-dimension-wizard"></a>[ディメンションの種類を指定] (ディメンション ウィザード)
  **[ディメンションの種類を指定]** ページを使用すると、ディメンションの種類を定義し、選択したディメンションの種類に関連付けられている特殊な属性の型をディメンションに追加できます。  
  
> [!NOTE]  
>  このページは、 **[ディメンションの種類の選択]** ページで **[標準ディメンション]** を選択した場合にのみ表示されます。  
  
## <a name="options"></a>および  
 **ディメンションの種類**  
 そのディメンションの種類を選択します。 次の表に、選択できるディメンションの種類を示します。  
  
|値|説明|  
|-----------|-----------------|  
|**Accounts**|勘定科目ディメンションには、勘定科目の一覧を表すデータとメタデータが収められています。<br /><br /> 勘定科目ディメンションの詳細については、「 [親子型ディメンションの財務アカウントの作成](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)」を参照してください。|  
|**BillOfMaterials**|部品表 (または BOM) ディメンションは、製品の部品表など、在庫情報や製造情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Channel**|チャネル ディメンションは、チャネル情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Currency**|通貨ディメンションには、通貨情報を表すデータとメタデータが収められます。<br /><br /> 通貨ディメンションの詳細については、「 [通貨ディメンションの作成](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)」を参照してください。|  
|**Customers**|顧客ディメンションは、顧客情報や連絡先情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Geography**|地理ディメンションは、市区町村や郵便番号などの地理情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**組織**|組織ディメンションは、従業員や系列会社などの組織情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**製品**|製品ディメンションは、製品情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Promotion**|プロモーション ディメンションは、マーケティングや販売促進の情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Quantitative**|数量ディメンションは、量的な情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**料金**|レート ディメンションには、換算レートと通貨変換の情報を表すデータとメタデータが収められます。|  
|**Regular**|標準ディメンションは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]で最も一般的に使用されるディメンションの種類です。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**Scenario**|シナリオ ディメンションは、計画的または戦略的な分析の情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
|**[時刻]**|時間ディメンションには、時刻に関するデータとメタデータが収められます。<br /><br /> 時間ディメンションの詳細については、「 [日付型ディメンションの作成](multidimensional-models/database-dimensions-create-a-date-type-dimension.md)」を参照してください。|  
|**Utility**|ユーティリティ ディメンションは、他のディメンションの種類に当てはまらない情報を表すデータとメタデータが収められる標準ディメンションです。<br /><br /> 標準ディメンションの詳細については、 [「ディメンションの種類」](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)を参照してください。|  
  
## <a name="dimension-attributes-options"></a>ディメンションの属性のオプション  
  
> [!NOTE]  
>  ここで説明するオプションは、 **[ディメンションの種類]** で選択したディメンションの種類に特殊な属性の型が関連付けられている場合にのみ指定できます。 すべてのディメンションの種類に特殊な属性の型が関連付けられているとは限りません。  
  
 **含まれます**  
 選択すると、その属性の型がディメンションに追加されます。  
  
 **属性の型**  
 **[ディメンションの種類]** で選択したディメンションの種類に関連付けられている属性の型が表示されます。 属性の種類の詳細については、[「Type 要素 (DimensionAttribute) (ASSL)」](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl) を参照してください。  
  
 **ディメンションの属性**  
 **[属性の型]** に表示された特殊な属性の型を、ディメンション ウィザードが割り当てるディメンションの属性を選択します。  
  
## <a name="see-also"></a>参照  
 [ディメンション ウィザードの F1 ヘルプ](dimension-wizard-f1-help.md)   
 [ディメンション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
