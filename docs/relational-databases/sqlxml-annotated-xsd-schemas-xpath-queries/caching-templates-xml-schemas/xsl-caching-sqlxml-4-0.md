---
title: XSL キャッシュ (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 265ce1db6f57f378dfaa7c0818914edd121b7d30
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257331"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL のキャッシュ (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSL スタイル シートをキャッシュすると、パフォーマンスが向上します。 XSL のキャッシュを ON に設定している場合、XSL スタイル シートは初回実行時にメモリに残るので、以降の処理でパフォーマンスが向上します。 既定の設定は ON です。  
  
 XSL のキャッシュ サイズは、レジストリに次のキーを追加することで設定できます。  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 XSL のキャッシュ サイズは、使用できるメモリと使用している XSL スタイル シートの数に基づいて設定します。 **XSLCacheSize**の既定値は31です。 XSL のアクセスが遅い場合はキャッシュ サイズを増やし、メモリが少ない場合はキャッシュ サイズを減らします。  
  
 パフォーマンスを向上させるために、通常使用する XSL スタイルシートの数よりも大きい**XSLCacheSize**を設定することをお勧めします。 **XSLCacheSize**が使用している xsl スタイルシートの数より小さい場合、xsl スタイルシートの数が増えるとパフォーマンスが低下します。 **XSLCacheSize**は最大128に設定できます。  
  
 キャッシュされた XSL スタイル シートが使用されるときには、毎回 XSL ファイルの変更回数がチェックされ、更新が必要かどうかが決定されます。 これは、ディスク コピーがキャッシュ コピーより新しいためです。  
  
## <a name="see-also"></a>参照  
 [テンプレートのキャッシュ &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [スキーマキャッシュ &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
