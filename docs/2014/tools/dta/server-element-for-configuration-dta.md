---
title: Server 要素 (DTA) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc763d621d15f982a2670483683d3862e678c98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283676"
---
# <a name="server-element-for-configuration-dta"></a>Configuration の Server 要素 (DTA)
  データベース エンジン チューニング アドバイザーで仮想的な構成 (`Configuration` 要素で指定する構成) を評価する対象のサーバーの識別情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|必須。`Configuration` 要素につき 1 個。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Configuration 要素 &#40;DTA&#41;](configuration-element-dta.md)|  
|**子要素**|[Server の Name 要素 &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Configuration の Database 要素 &#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>コメント  
 1 つだけ指定できます`Server`の要素、`Configuration`要素。 この要素は、 **データベース エンジン チューニング アドバイザー XML スキーマ** の [ServerTypecomplexType](https://go.microsoft.com/fwlink/?linkid=43100)の名前です。 この `Server` 要素を `DTAInput` 要素の子要素と混同しないでください。 詳しくは、「[Server 要素 &#40;DTA&#41;](server-element-dta.md)」を参照してください。  
  
## <a name="example"></a>例  
 使用例については、「[ユーザー指定の構成を指定した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
