---
title: 要素をデータベース サーバー (DTA) |Microsoft Docs
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
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b23e8d7f68cca0722691863a2c5c8d5e095c33c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62661834"
---
# <a name="database-element-for-server-dta"></a>Server の Database 要素 (DTA)
  特定のサーバーにあるチューニング対象のデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|[なし] :|  
|既定値|[なし] :|  
|個数|`Server` 要素につき 1 回以上の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|親要素|[Server 要素 &#40;DTA&#41;](server-element-dta.md)|  
|子要素|[Database の Name 要素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Database の Schema 要素 &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **DatabaseDetailsTypecomplexType** の名前です。 この `Database` 要素を、ルートの親要素が `Configuration` 要素である他の要素と混同しないでください。 詳細については、「[Configuration の Database 要素 &#40;DTA&#41;](database-element-for-configuration-dta.md)」を参照してください。  
  
## <a name="example"></a>例  
 使用例については、`Database`要素を参照してください[サーバー要素&#40;DTA&#41;](server-element-dta.md)します。  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
