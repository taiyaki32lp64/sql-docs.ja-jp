---
title: 要素をデータベースのワークロード (DTA) |Microsoft Docs
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
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f5b5c233a482672a0cc225364dbf1e4f3b4b645
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185407"
---
# <a name="database-element-for-workload-dta"></a>Workload の Database 要素 (DTA)
  ワークロード トレース テーブルのあるデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|他の種類のワークロードが指定されていない場合は、1 回の出現が必要です。 `EventString` 親要素に対しては、`File`、`Database`、または `Workload` 子要素を指定する必要がありますが、使用できるのは 1 種類だけです。 たとえば、ワークロードを `Database` 要素で指定した場合、同じ XML 入力ファイル内でワークロードを `File` 要素で指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Workload 要素 &#40;DTA&#41;](workload-element-dta.md)|  
|**子要素**|[Database の Name 要素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Database の Schema 要素 &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **DatabaseDetailsTypecomplexType** の名前です。 この `Database` 要素を、ルートの親要素が `Configuration` 要素である他の要素と混同しないでください。 (「[Configuration の Database 要素 &#40;DTA&#41;](database-element-for-configuration-dta.md)」を参照)。  
  
## <a name="example"></a>例  
 この使用例については`Database`要素のコード例を参照してください。 [Workload 要素&#40;DTA&#41;](workload-element-dta.md)します。  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
