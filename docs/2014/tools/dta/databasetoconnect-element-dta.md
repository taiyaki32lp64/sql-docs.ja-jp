---
title: DatabaseToConnect 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185415"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect 要素 (DTA)
  データベース エンジン チューニング アドバイザーがワークロードのチューニング時に最初に接続するデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|`string`、長さは無制限です。|  
|**既定値**|[なし] :|  
|**個数**|任意。 `TuningOptions` 要素につき 1 回使用できます。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[TuningOptions 要素 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子要素**|なし|  
  
## <a name="remarks"></a>コメント  
 `DatabaseToConnect` は、データベース エンジン チューニング アドバイザーがチューニング セッションの開始時に最初に接続するデータベースの名前を指定するために使用します。 この要素では、データベースを 1 つだけ指定できます。 複数のデータベース名が指定されていると、データベース エンジン チューニング アドバイザーはエラーを返します。  
  
## <a name="example"></a>例  
 使用例については、「[インライン ワークロードを指定した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
