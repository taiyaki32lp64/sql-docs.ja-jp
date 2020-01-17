---
title: 分類列 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c96ee3cbaa5ae25404d61054dccd1860c6596f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085685"
---
# <a name="classified-columns-data-mining"></a>分類済みの列 (データ マイニング)
  分類済みの列を定義する場合は、マイニング構造内の現在の列と別の列の間でリレーションシップを作成します。 マイニング構造内で分類済みの列として指定した列のデータには、その構造内の別の列の値について説明した分類情報が含まれています。  
  
 たとえば、数値データを含んだ 2 つの列があるとします。一方の列 [Yearly Purchases] には、特定の暦年における顧客ごとの年間合計購入金額が格納され、もう一方の [Standard Deviations] 列には、これらの値の標準偏差が格納されます。 この場合、[Yearly Purchases] 列を分類済みの列に指定すると、モデルはこのリレーションシップを分析で使用できるようになります。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に用意されているアルゴリズムでは、分類済みの列の使用がサポートされていません。この機能はカスタム アルゴリズムの作成用に提供されています。  
  
## <a name="defining-a-classified-column"></a>分類済みの列の定義  
 分類済みの列のデータ型は、`Long` または `Double` にする必要があります。  
  
 次の一覧では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で分類済みの列に対してサポートされているコンテンツの種類について説明します。  
  
 **PROBABILITY**  
 この列の値は、関連付けられている値の確率であり、0 から 1 までの数値です。  
  
 **VARIANCE**  
 この列の値は、関連付けられている値の分散です。  
  
 **[STDEV]**  
 この列の値は、関連付けられている値の標準偏差です。  
  
 **PROBABILITY_VARIANCE**  
 この列の値は、関連付けられている値の確率の分散です。  
  
 **PROBABILITY_STDEV**  
 この列の値は、関連付けられている値の確率の標準偏差です。  
  
 **SUPPORT**  
 この列の値は、関連付けられている値の重み (ケース レプリケーション係数) です。  
  
## <a name="see-also"></a>関連項目  
 [コンテンツの種類 &#40;データ マイニング&#41;](content-types-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [データ型 (データ マイニング)](data-types-data-mining.md)  
  
  
