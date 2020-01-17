---
title: FeatureSet 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9c0711dc15327cad726e61857f61539f8cadea02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034971"
---
# <a name="featureset-element-dta"></a>FeatureSet 要素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベース エンジン チューニング アドバイザーでの分析時に使用する物理設計構造 (インデックス、インデックス付きビュー) が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|[説明]|  
|--------------------|-----------------|  
|**データ型と長さ**|**string**、長さは無制限です。|  
|**指定できる値**|**IDX_IV**<br /> インデックスおよびインデックス付きビュー。<br /><br /> **IDX**<br /> インデックスのみ。<br /><br /> **IV**<br /> インデックス付きビューのみ。<br /><br /> **NCL_IDX**<br /> 非クラスター化インデックスのみ。<br /><br /> この要素では、上記の値のいずれか 1 つを使用してください。|  
|**既定値**|**IDX**|  
|**個数**|**TuningOptions** 要素につき 1 回の出現が必要です。ただし、 **DropOnlyMode** 要素を使用している場合は別です。 **DropOnlyMode** を使用している場合は、 **FeatureSet**を使用できません。 これらの要素を同時に指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[TuningOptions 要素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子要素**|[なし] :|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[XML 入力ファイルの簡単なサンプル &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
