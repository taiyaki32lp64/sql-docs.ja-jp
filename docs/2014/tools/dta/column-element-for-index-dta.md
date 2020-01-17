---
title: Column 要素 (DTA) のインデックスの |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef7972014dff498172b9c016b3a7debb79a054fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149852"
---
# <a name="column-element-for-index-dta"></a>Index の Column 要素 (DTA)
  ユーザー指定の構成で、インデックスを作成する列を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>要素の属性  
  
|Column の属性|説明|  
|----------------------|-----------------|  
|`Type`|任意。 インデックスの列の種類を指定します。 この属性を指定するには **string** データ型を使用します。指定できる値は次のいずれかです。<br /><br /> `KeyColumn`:<br />                  列がインデックス キーによって参照されていることを指定します。 この属性を設定するには、以下の構文を使用します。<br />`<Column Type="KeyColumn">`<br />キー列の詳細については、「 [クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)」を参照してください。<br /><br /> `IncludedColumn`:列がキー列ではなく、付加列であることを指定します。 この属性を設定するには、以下の構文を使用します。<br />`<Column Type="IncludedColumn">`<br />付加列の詳細については、「 [付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。|  
|`SortOrder`|任意。 列の並べ替え順を指定します。 **string** データ型を使用して、 **"Ascending"** または **"Descending"** の並べ替え順のいずれかを以下のように指定します。<br /><br /> `<Column SortOrder="Ascending">`|  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|`Index` 要素につき 1024 列まで指定できます。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Index 要素 &#40;DTA&#41;](index-element-dta.md)|  
|**子要素**|[Column の Name 要素 &#40;DTA&#41;](name-element-for-column-dta.md)|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[ユーザー指定の構成を指定した XML 入力ファイルのサンプル &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
