---
title: Create 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ec9ad9569326e4a9b3e890af4b5f909e36e5c5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149489"
---
# <a name="create-element-dta"></a>Create 要素 (DTA)
  ユーザー指定の構成内のインデックス、統計、ヒープ構造に関する情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|物理デザイン構造の各種類 (インデックス、統計、ヒープ構造) につき 1 回の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Recommendation 要素 &#40;DTA&#41;](recommendation-element-dta.md)|  
|**子要素**|[Index 要素 &#40;DTA&#41;](index-element-dta.md)<br /><br /> `Statistics` 要素 (を参照してください[データベース エンジン チューニング アドバイザー XML スキーマ](https://schemas.microsoft.com/sqlserver/)について)<br /><br /> `Heap` 要素 (を参照してください[データベース エンジン チューニング アドバイザー XML スキーマ](https://schemas.microsoft.com/sqlserver/)について)|  
  
## <a name="remarks"></a>コメント  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **CreateTypecomplexType** の名前です。 ユーザー指定の構成でインデックス、統計、ヒープ構造を作成するために使用します。 この `Create` 要素を、ビューを作成するための `CreateViewType` やパーティション分割を作成するための `CreatePType` という他の種類の要素と混同しないでください。 参照してください、[データベース エンジン チューニング アドバイザー XML スキーマ](https://schemas.microsoft.com/sqlserver/)これら他について`Create`要素の型。  
  
## <a name="example"></a>例  
 この要素の使用例については、「[ユーザー指定の構成を指定した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
