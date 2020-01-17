---
title: DTAInput 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1861b6ef4ab3617b5f12e7711fa2b895edaa55a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188118"
---
# <a name="dtainput-element-dta"></a>DTAInput 要素 (DTA)
  データベース エンジン チューニング アドバイザーに対する XML 入力の定義が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|---------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|**DTAXML** 要素につき 1 回 (省略可)。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[DTAXML 要素 &#40;DTA&#41;](dtaxml-element-dta.md)|  
|**子要素**|[Server 要素 &#40;DTA&#41;](server-element-dta.md)<br /><br /> [Workload 要素 &#40;DTA&#41;](workload-element-dta.md)<br /><br /> [TuningOptions 要素 &#40;DTA&#41;](tuningoptions-element-dta.md)<br /><br /> [Configuration 要素 &#40;DTA&#41;](configuration-element-dta.md)|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザーの入力スキーマ階層のルートです。 データベース エンジン チューニング アドバイザーへの入力としては、チューニング対象のデータベースのサーバー、ワークロード、チューニング オプション、ユーザー指定の構成などを指定した引数を使用できます。  
  
## <a name="example"></a>例  
 **DTAInput** 要素の使用例については、「[XML 入力ファイルの簡単なサンプル &#40;DTA&#41;](simple-xml-input-file-sample-dta.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
