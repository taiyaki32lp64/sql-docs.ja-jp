---
title: 名前空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5f28b5d593524288a755f4c9455bba39554d7bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924817"
---
# <a name="namespaces"></a>名前空間
ADO での XML 永続化形式は、次の 4 つの名前空間を使用します。  
  
## <a name="remarks"></a>コメント  
 ADO での XML 永続化形式は、次の 4 つの名前空間を使用します。  
  
|Prefix|説明|  
|------------|-----------------|  
|s|要素と現在のレコード セットのスキーマを定義する属性を含む「XML データ」の名前空間を参照します。|  
|dt|データ型の定義の仕様を参照します。|  
|rs|親要素の名前空間と ADO レコード セットのプロパティに固有の属性と属性を表します。|  
|z|現在の行セットのスキーマを参照します。|  
  
 クライアント、仕様で定義された、独自のタグをこれらの名前空間に追加する必要があります。 たとえば、クライアントと名前空間を定義する必要があります"urn: スキーマ-microsoft-com:rowset"out"rs: MyOwnTag"のような記述 名前空間の詳細については、次を参照してください。、 [W3C Namespaces in XML 』](http://www.w3.org/TR/REC-xml-names/)します。  
  
> [!IMPORTANT]
>  スキーマ タグの ID は"RowsetSchema、"である必要があり。、現在の行セットのスキーマを参照するために使用する名前空間が"#RowsetSchema" をポイントする必要があります。  
  
 コロンと等号 (=) 間の部分の-名前空間のプレフィックスは任意でことに注意してください。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 ユーザーは、これをこの名前は、XML ドキュメント全体で一貫して使用する限り、任意の名前を定義できます。 ADO が常に"s、"、"rs"「dt」を書き込み、、"z"これらのプレフィックス名でないコンポーネントを読み込み中にハードコーディングします。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
