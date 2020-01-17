---
title: ディメンションの種類 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62728558"
---
# <a name="dimension-types"></a>ディメンションの種類
  `Type` プロパティの設定は、ディメンションの内容に関する情報をサーバーおよびクライアント アプリケーションに提供します。 `Type` の設定がクライアント アプリケーションへのガイダンスの提供のみを目的としている場合は、この設定を省略できます。 一方、`Accounts` ディメンションや `Time` ディメンションでは、ディメンションおよびその属性の `Type` プロパティの設定によって、サーバー ベースの具体的な動作が決まるため、キューブで特定の動作を実装する際に、この設定が必要になることがあります。 たとえば、ディメンションの `Type` プロパティを `Accounts` に設定すると、標準ディメンションに勘定科目属性が含まれていることがクライアント アプリケーションに示されます。 時間、アカウント、および通貨ディメンションの詳細については、次を参照してください[日付型ディメンションの作成](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md)、 [、親子型ディメンションの財務アカウントの作成](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)、および[、通貨の作成。ディメンションの入力](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)します。  
  
 ディメンションの種類の既定の設定は `Regular` です。この設定では、ディメンションの内容に関して何も想定されません。 ディメンション ウィザードを使用してディメンションを定義するときに `Time` を指定しない限り、初めてディメンションを定義する場合は、これがすべてのディメンションの既定の設定です。 また、ディメンション ウィザードの [ディメンションの種類] の一覧に適切な種類が表示されていない場合は、ディメンションの種類を `Regular` のままにしておく必要があります。  
  
## <a name="available-dimension-types"></a>使用可能なディメンションの種類  
 次の表に、ディメンションの種類で使用できる[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]します。  
  
|[ディメンションの種類]|説明|  
|--------------------|-----------------|  
|Regular|特定のディメンションの種類に設定されていない種類のディメンションです。|  
|Time|属性が年、半期、四半期、月、日などの時間間隔を表すディメンションです。|  
|Organization|属性が従業員や子会社などの組織情報を表すディメンションです。|  
|Geography|属性が市区町村や郵便番号などの地理情報を表すディメンションです。|  
|BillOfMaterials|属性が製品の部品表などの在庫情報や製造情報を表すディメンションです。|  
|Accounts|財務報告用の勘定科目一覧表を表す属性を持つディメンションです。|  
|Customers|属性が顧客情報や連絡先情報を表すディメンションです。|  
|Products|属性が製品情報を表すディメンションです。|  
|シナリオ|属性が計画的または戦略的な分析情報を表すディメンションです。|  
|Quantitative|属性が量的な情報を表すディメンションです。|  
|ユーティリティ|属性がその他の情報を表すディメンションです。|  
|通貨|この種類のディメンションには、通貨のデータとメタデータが含まれています。|  
|Rates|属性が通貨レート情報を表すディメンションです。|  
|Channel|属性がチャネル情報を表すディメンションです。|  
|Promotion|属性がマーケティング関連のプロモーション情報を表すディメンションです。|  
  
## <a name="see-also"></a>関連項目  
 [既存のテーブルを使用したディメンションを作成します。](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [ディメンション &#40;Analysis Services - 多次元データ&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
