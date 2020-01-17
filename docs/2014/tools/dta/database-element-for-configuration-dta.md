---
title: 要素をデータベースの構成 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fbca62a5d32ed6b7ec30eb5d6dba6a82a2b80c64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298350"
---
# <a name="database-element-for-configuration-dta"></a>Configuration の Database 要素 (DTA)
  データベース エンジン チューニング アドバイザーで仮想的な構成 (`Configuration` 要素で指定する構成) を評価するときの対象のデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|`Server` 要素につき 1 回以上の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Configuration の Server 要素 &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**子要素**|[Database の Name 要素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Database の Schema 要素 &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Recommendation 要素 &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **DatabaseTypecomplexType** の名前です。 この `Database` 要素を、ルートの親要素が `Server` 要素である (XML 入力ファイルの最上位に記述する) 同じ名前の要素と混同しないでください。 詳細については、「[Server の Database 要素 &#40;DTA&#41;](database-element-for-server-dta.md)」を参照してください。  
  
## <a name="example"></a>例  
 この使用例については`Database`要素を参照してください、[ユーザー指定の構成の XML 入力ファイルのサンプル&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)します。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
