---
title: EventString 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30e46515fda5bf03a96e9f1168b470f635698d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211114"
---
# <a name="eventstring-element-dta"></a>EventString 要素 (DTA)
  [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ワークロードを XML 入力ファイルで直接指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>要素の属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Weight`|任意。 対象のイベントに関するクエリの重み係数 (重要度の係数) を指定します。 重み係数の指定には、`float` データ型を使用します。 たとえば、`Weight`="100.01" のようにします。 `Weight` に指定できる最小値は「0」です。|  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|`string`、長さは制限されます。|  
|**既定値**|[なし] :|  
|**個数**|他の種類のワークロードが指定されていない場合は、1 回の出現が必要です。 `EventString` 親要素に対しては、`File`、`Database`、または `Workload` 子要素を指定する必要がありますが、使用できるのは 1 種類だけです。 たとえば、`EventString` 要素を使用してワークロードを指定した場合は、同じ XML 入力ファイル内でワークロードを `File` 要素で指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Workload 要素 &#40;DTA&#41;](workload-element-dta.md)|  
|**子要素**|[なし] :|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[インライン ワークロードを使用した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
