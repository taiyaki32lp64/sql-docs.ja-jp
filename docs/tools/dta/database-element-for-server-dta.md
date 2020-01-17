---
title: Server の Database 要素 (DTA) |Microsoft Docs
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
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5817a6d32ff94aaba7e4c0a573e6cd6a5fd586dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116931"
---
# <a name="database-element-for-server-dta"></a>Server の Database 要素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  特定のサーバーにあるチューニング対象のデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|[説明]|  
|--------------------|-----------------|  
|データ型と長さ|[なし] :|  
|既定値|[なし] :|  
|個数|**Server** 要素につき 1 回以上の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|親要素|[Server 要素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|子要素|[Database の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Database の Schema 要素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **DatabaseDetailsTypecomplexType** の名前です。 この **Database** 要素を、ルートの親要素が **Configuration** 要素である他の要素と混同しないでください。 詳細については、「[Configuration の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)」を参照してください。  
  
## <a name="example"></a>例  
 **Database** 要素の使用例については、「[Server 要素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
