---
title: Recommendation 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcc0a95028b1f107f15752692d3dcad090fbe8b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659585"
---
# <a name="recommendation-element-dta"></a>Recommendation 要素 (DTA)
  ユーザー指定の構成の一部である仮想インデックスについての情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|任意。 `Table` 要素につき 1 回使用できます。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Schema の Table 要素 &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**子要素**|[Create 要素 &#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` 要素。 詳細については、 [データベース エンジン チューニング アドバイザーの XML スキーマ](https://go.microsoft.com/fwlink/?linkid=43100)を参照してください。|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **RecommendationTypecomplexType** の名前です。 仮想的な構成でのインデックスを指定するために使用します。 この `Recommendation` 要素を、パーティション分割を指定するための `RecommendationPType` やビューを指定するための `RecommendationViewType` という他の種類の要素と混同しないでください。 これら他について`Recommendation`要素の型を参照してください、[データベース エンジン チューニング アドバイザー XML スキーマ](https://go.microsoft.com/fwlink/?linkid=43100)します。  
  
## <a name="example"></a>例  
 この要素の使用例については、「[ユーザー指定の構成を指定した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
