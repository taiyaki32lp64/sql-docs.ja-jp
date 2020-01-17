---
title: 列の分布 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db71b5a94285f8ae63afeb65bec3f9807f8da27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085711"
---
# <a name="column-distributions-data-mining"></a>列の分布 (データ マイニング)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、マイニング構造内の列の分布を定義して、マイニング モデルの作成時にこれらの列のデータがアルゴリズムによってどのように処理されるかを指定できます。 いくつかのアルゴリズムは、列が値の一般的な分布を含むことが認識された場合、モデルを処理する前にすべての連続列の分布を定義するために使用されます。 分布が定義されない場合、アルゴリズムが持つデータを解釈するための情報が少ないため、分布が定義されたときよりも、マイニング モデルの結果が実際の予測より小さくなる場合があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で使用できるアルゴリズムでは、次の分布の種類がサポートされています。  
  
 `Normal`  
 連続列の値は、正規分布のヒストグラムを形成します。  
  
 ![正規分布のヒストグラム](../media/normal-distribution.gif "正規分布のヒストグラム")  
  
 `Log Normal`  
 連続列の値は、曲線が上端で長くなり、下端に向かってスキューされるヒストグラムを形成します。  
  
 ![対数正規分布のヒストグラム](../media/log-normal-distribution.gif "対数正規分布のヒストグラム")  
  
 `Uniform`  
 連続列の値はフラット曲線を形成し、すべての値が等しくなります。  
  
 ![一様分布のヒストグラム](../media/uniform-distribution.gif "一様分布のヒストグラム")  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が提供するアルゴリズムの詳細については、「[データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [コンテンツの種類 &#40;データ マイニング&#41;](content-types-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [分離メソッド &#40;データ マイニング&#41;](discretization-methods-data-mining.md)   
 [分布 &#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [マイニング構造列](mining-structure-columns.md)  
  
  
